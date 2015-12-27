title: "在XML布局里给View设置点击事件"
categories:
  - Android
tags:
  - android
  - xml
  - 点击事件
comments: true
date: 2015-12-23 00:00:00
layout:
link:
clearReading:
metaAlignment:
thumbnailImage:  http://7xih5c.com1.z0.glb.clouddn.com/15-12-27/38510906.jpg
coverSize:
coverCaption:
coverMeta:
photos:

---

Android开发中，可以在Java代码里给View设置点击事件，也可以直接在XML布局里通过`android:onClick`属性设置回调，这篇日志注意是从源码角度分析后者的实现方式。
<!--more-->

给一个View设置监听点击事件是再普通不过的事情，比如
``` java
    view.setOnClickListener(onClickListener);
```

另外一种做法是直接在XML布局里面指定View点击时候的回调方法，首先需要在Activity中编写用于回调的方法，比如
``` java
    public void onClickView(View view){
		// do something
	}
```
然后在XML设置View的`android:onClick`属性
``` xml
    <View
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:onClick="onClickView" />
```

有的时候从XML布局里直接设定点击事件会比较方便（特别是在写DEMO项目的时候），这种做法平时用的人并不多，从使用方式上大致能猜出来，View应该是在运行的时候，使用反射的方式从Activity找到“onClickView”方法并调用，因为这种做法并没有用到任何接口。

接下来，我们可以从源码中分析出View是怎么触发回调方法的。

![](http://7xih5c.com1.z0.glb.clouddn.com/15-12-22/30732155.jpg)
View有5个构造方法，第一个是内部使用的，平时在Java代码中直接创建View实例用的是第二种方法，而从XML布局渲染出来的View实例最后都是要调用第五种方法。

``` java
public View(Context context, @Nullable AttributeSet attrs, int defStyleAttr, int defStyleRes) {
        this(context);

        final TypedArray a = context.obtainStyledAttributes(
                attrs, com.android.internal.R.styleable.View, defStyleAttr, defStyleRes);
                
        for (int i = 0; i < N; i++) {
            int attr = a.getIndex(i);
            switch (attr) {
                ……
                // 处理onClick属性
                case R.styleable.View_onClick:
                    if (context.isRestricted()) {
                        throw new IllegalStateException("The android:onClick attribute cannot "
                                + "be used within a restricted context");
                    }

                    final String handlerName = a.getString(attr);
                    if (handlerName != null) {
                        // 给当前View实例设置一个DeclaredOnClickListener监听器
                        setOnClickListener(new DeclaredOnClickListener(this, handlerName));
                    }
                    break;
                }
        }
}
```
处理onClick属性的时候，先判断View的Context是否isRestricted，如果是就抛出一个IllegalStateException异常。看看isRestricted方法
``` java
    /**
     * Indicates whether this Context is restricted.
     *
     * @return {@code true} if this Context is restricted, {@code false} otherwise.
     *
     * @see #CONTEXT_RESTRICTED
     */
    public boolean isRestricted() {
        return false;
    }
```
isRestricted是用于判断当前的Context实例是否出于被限制的状态，按照官方的解释，处限制状态的Context，会忽略某些特点的功能，比如XML的某些属性，很明显，我们在研究的`android:onClick`属性也会被忽略。

> a restricted context may disable specific features. For instance, a View associated with a restricted context would ignore particular XML attributes.

不过isRestricted方法是Context中为数不多的有具体实现的方法（其余基本是抽象方法），这里直接返回false，而且这个方法只有在ContextWrapper和MockContext中有重写
![](http://7xih5c.com1.z0.glb.clouddn.com/15-12-22/51841820.jpg)
``` java
public class ContextWrapper extends Context {
    Context mBase;
    @Override
    public boolean isRestricted() {
        return mBase.isRestricted();
    }
}

public class MockContext extends Context {
    @Override
    public boolean isRestricted() {
        throw new UnsupportedOperationException();
    }
}
```
ContextWrapper中也只是代理调用mBase的isRestricted，而MockContext是写单元测试的时候才会用到，所以这里的isRestricted基本只会返回false，除非使用了自定义的ContextWrapper并重写了isRestricted。
回到View，接着的`final String handlerName = a.getString(attr);`其实就是拿到了`android:onClick="onClickView"`中的“onClickView”这个字符串，接着使用了当前View的实例和“onClickView”创建了一个DeclaredOnClickListener实例，并设置为当前View的点击监听器。

``` java
/**
     * An implementation of OnClickListener that attempts to lazily load a
     * named click handling method from a parent or ancestor context.
     */
private static class DeclaredOnClickListener implements OnClickListener {
        private final View mHostView;
        private final String mMethodName;

        private Method mMethod;

        public DeclaredOnClickListener(@NonNull View hostView, @NonNull String methodName) {
            mHostView = hostView;
            mMethodName = methodName;
        }

        @Override
        public void onClick(@NonNull View v) {
            if (mMethod == null) {
                mMethod = resolveMethod(mHostView.getContext(), mMethodName);
            }

            try {
                mMethod.invoke(mHostView.getContext(), v);
            } catch (IllegalAccessException e) {
                throw new IllegalStateException(
                        "Could not execute non-public method for android:onClick", e);
            } catch (InvocationTargetException e) {
                throw new IllegalStateException(
                        "Could not execute method for android:onClick", e);
            }
        }

        @NonNull
        private Method resolveMethod(@Nullable Context context, @NonNull String name) {
            while (context != null) {
                try {
                    if (!context.isRestricted()) {
                        return context.getClass().getMethod(mMethodName, View.class);
                    }
                } catch (NoSuchMethodException e) {
                    // Failed to find method, keep searching up the hierarchy.
                }

                if (context instanceof ContextWrapper) {
                    context = ((ContextWrapper) context).getBaseContext();
                } else {
                    // Can't search up the hierarchy, null out and fail.
                    context = null;
                }
            }

            final int id = mHostView.getId();
            final String idText = id == NO_ID ? "" : " with id '"
                    + mHostView.getContext().getResources().getResourceEntryName(id) + "'";
            throw new IllegalStateException("Could not find method " + mMethodName
                    + "(View) in a parent or ancestor Context for android:onClick "
                    + "attribute defined on view " + mHostView.getClass() + idText);
        }
}
```
到这里就清楚了，当点击View的时候，DeclaredOnClickListener实例的“onClick”方法会被调用，接着会调用“resolveMethod”方法，使用反射的方式从View的Context中找一个叫“onClickView”方法，这个方法有一个View类型的参数，最后再使用反射调用该方法。要注意的是，“onClickView”方法必须是public类型的，不然反射调用时会抛出IllegalAccessException异常。

同时从源码也能看出，使用`android:onClick`设置点击事件的方式是从Context里面查找回调方法的，所以如果对于在Fragment的XML里创建的View，是无法通过这种方式绑定Fragment中的回调方法的，因为Fragment自身并不是一个Context，这里的View的Context其实是FragmentActivity，这也意味着使用这种方式能够快速地从Fragment中回调到FragmentActivity。

此外，从DeclaredOnClickListener类的注释也能看出`android:onClick`的功能，**主要是起到懒加载的作用**，只有到点击View的时候，才会知道哪个方法是用于点击回调的。

最后，特别需要补充说明的是，使用`android:onClick`给View设置点击事件，就意味着要在Activity里添加一个非接口的public方法。现在Android的开发趋势是“不要把业务逻辑写在Activity类里面”，这样做有利于项目的维护，防止Activity爆炸，所以尽量不要在Activity里出现非接口、非生命周期的public方法。因此，贸然使用`android:onClick`可能会“污染”Activity。



