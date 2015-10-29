title: "Android MVP模式 简单易懂的介绍方式"
categories:
  - Android
tags:
  - android
  - mvp
  - design pattern
comments: true
date: 2015-10-11 14:29:48
layout:
link:
clearReading:
metaAlignment:
thumbnailImage: http://7xih5c.com1.z0.glb.clouddn.com/15-10-11/76327834.jpg
coverImage:
coverSize:
coverCaption:
coverMeta:
photos:

---
Android **MVP模式**<sup>\[1\]</sup>也不是什么新鲜的东西了，我在自己的项目里也普遍地使用了这个设计模式。当项目越来越庞大、复杂，参与的研发人员越来越多的时候，**MVP模式**的优势就充分显示出来了。
<!-- more -->
*导读：MVP模式是MVC模式在Android上的一种变体，要介绍MVP就得先介绍MVC。在MVC模式中，Activity应该是属于View这一层。而实质上，它既承担了View，同时也包含一些Controller的东西在里面。这对于开发与维护来说不太友好，耦合度大高了。把Activity的View和Controller抽离出来就变成了View和Presenter，这就是MVP模式。*
<!-- toc -->

## 基本信息

- 作者：[Kaede Akatsuki](http://kaedea.com)
- 项目：[Android-MVP-Pattern](https://github.com/kaedea/Android-MVP-Pattern)
- 出处：[Android MVP模式 简单易懂的介绍方式](http://kaedea.com/2015/10/11/android-mvp-pattern)


MVP模式（Model-View-Presenter）可以说是MVC模式（Model-View-Controller）在Android开发上的一种变种、进化模式。后者大家可能比较熟悉，就算不熟悉也可能或多或少地在自己的项目中用到过。要介绍MVP模式，就不得不先说说MVC模式。

## MVC模式
MVC模式的结构分为三部分，实体层的Model，视图层的View，以及控制层的Controller。

![MVC结构](http://7xih5c.com1.z0.glb.clouddn.com/15-10-11/13126761.jpg "MVC结构")

- 其中View层其实就是程序的UI界面，用于向用户展示数据以及接收用户的输入
- 而Model层就是JavaBean实体类，用于保存实例数据
- Controller控制器用于更新UI界面和数据实例

例如，View层接受用户的输入，然后通过Controller修改对应的Model实例；同时，当Model实例的数据发生变化的时候，需要修改UI界面，可以通过Controller更新界面。（View层也可以直接更新Model实例的数据，而不用每次都通过Controller，这样对于一些简单的数据更新工作会变得方便许多。）

举个简单的例子，现在要实现一个飘雪的动态壁纸，可以给雪花定义一个实体类Snow，里面存放XY轴坐标数据，View层当然就是SurfaceView（或者其他视图），为了实现雪花飘的效果，可以启动一个后台线程，在线程里不断更新Snow实例里的坐标值，这部分就是Controller的工作了，Controller里还要定时更新SurfaceView上面的雪花。进一步的话，可以在SurfaceView上监听用户的点击，如果用户点击，只通过Controller对触摸点周围的Snow的坐标值进行调整，从而实现雪花在用户点击后出现弹开等效果。具体的MVC模式请自行Google。

## MVP模式
在Android项目中，Activity和Fragment占据了大部分的开发工作。如果有一种设计模式（或者说代码结构）专门是为优化Activity和Fragment的代码而产生的，你说这种模式重要不？这就是MVP设计模式。

按照MVC的分层，Activity和Fragment（后面只说Activity）应该属于View层，用于展示UI界面，以及接收用户的输入，此外还要承担一些生命周期的工作。Activity是在Android开发中充当非常重要的角色，特别是TA的生命周期的功能，所以开发的时候我们经常把一些业务逻辑直接写在Activity里面，这非常直观方便，代价就是Activity会越来越臃肿，超过1000行代码是常有的事，而且如果是一些可以通用的业务逻辑（比如用户登录），写在具体的Activity里就意味着这个逻辑不能复用了。如果有进行代码重构经验的人，看到1000+行的类肯定会有所顾虑。因此，Activity不仅承担了View的角色，还承担了一部分的Controller角色，这样一来V和C就耦合在一起了，虽然这样写方便，但是如果业务调整的话，要维护起来就难了，而且在一个臃肿的Activity类查找业务逻辑的代码也会非常蛋疼，所以看起来有必要在Activity中，把View和Controller抽离开来，而这就是MVP模式的工作了。

![MVP结构](http://7xih5c.com1.z0.glb.clouddn.com/15-10-11/2114527.jpg "MVP结构")

MVP模式的核心思想
>**MVP把Activity中的UI逻辑抽象成View接口，把业务逻辑抽象成Presenter接口，Model类还是原来的Model**。

这就是MVP模式，现在这样的话，Activity的工作的简单了，只用来响应生命周期，其他工作都丢到Presenter中去完成。从上图可以看出，Presenter是Model和View之间的桥梁，为了让结构变得更加简单，View并不能直接对Model进行操作，这也是MVP与MVC最大的不同之处。

## MVP模式的作用
MVP的好处都有啥，谁说对了就给他 KIRA!!(<ゝω·)☆

- 分离了视图逻辑和业务逻辑，降低了耦合
- Activity只处理生命周期的任务，代码变得更加简洁
- 视图逻辑和业务逻辑分别抽象到了View和Presenter的接口中去，提高代码的可阅读性
- Presenter被抽象成接口，可以有多种具体的实现，所以方便进行单元测试
- 把业务逻辑抽到Presenter中去，避免后台线程引用着Activity导致Activity的资源无法被系统回收从而引起内存泄露和OOM

其中最重要的有三点
### Activity 代码变得更加简洁
相信很多人阅读代码的时候，都是从Activity开始的，对着一个1000+行代码的Activity，看了都觉得难受。

使用MVP之后，Activity就能瘦身许多了，基本上只有FindView、SetListener以及Init的代码。其他的就是对Presenter的调用，还有对View接口的实现。这种情形下阅读代码就容易多了，而且你只要看Presenter的接口，就能明白这个模块都有哪些业务，很快就能定位到具体代码。Activity变得容易看懂，容易维护，以后要调整业务、删减功能也就变得简单许多。

### 方便进行单元测试
一般单元测试都是用来测试某些新加的业务逻辑有没有问题，如果采用传统的代码风格（习惯性上叫做MV模式，少了P），我们可能要先在Activity里写一段测试代码，测试完了再把测试代码删掉换成正式代码，这时如果发现业务有问题又得换回测试代码，咦，测试代码已经删掉了！好吧重新写吧……

MVP中，由于业务逻辑都在Presenter里，我们完全可以写一个PresenterTest的实现类继承Presenter的接口，现在只要在Activity里把Presenter的创建换成PresenterTest，就能进行单元测试了，测试完再换回来即可。万一发现还得进行测试，那就再换成PresenterTest吧。

### 避免 Activity 的内存泄露
Android APP 发生OOM的最大原因就是出现内存泄露造成APP的内存不够用，而造成内存泄露的两大原因之一就是Activity泄露（Activity Leak）（另一个原因是Bitmap泄露（Bitmap Leak））。
>Java一个强大的功能就是其虚拟机的内存回收机制，这个功能使得Java用户在设计代码的时候，不用像C++用户那样考虑对象的回收问题。然而，Java用户总是喜欢随便写一大堆对象，然后幻想着虚拟机能帮他们处理好内存的回收工作。可是虚拟机在回收内存的时候，只会回收那些没有被引用的对象，被引用着的对象因为还可能会被调用，所以不能回收。

Activity是有生命周期的，用户随时可能切换Activity，当APP的内存不够用的时候，系统会回收处于后台的Activity的资源以避免OOM。

采用传统的MV模式，一大堆异步任务和对UI的操作都放在Activity里面，比如你可能从网络下载一张图片，在下载成功的回调里把图片加载到 Activity 的 ImageView 里面，所以异步任务保留着对Activity的引用。这样一来，即使Activity已经被切换到后台（onDestroy已经执行），这些异步任务仍然保留着对Activity实例的引用，所以系统就无法回收这个Activity实例了，结果就是Activity Leak。Android的组件中，Activity对象往往是在堆（Java Heap）里占最多内存的，所以系统会优先回收Activity对象，如果有Activity Leak，APP很容易因为内存不够而OOM。

采用MVP模式，只要在当前的Activity的onDestroy里，分离异步任务对Activity的引用，就能避免 Activity Leak。


说了这么多，没看懂？好吧，我自己都没看懂自己写的，我们还是直接看代码吧。

## MVP模式的使用
![简单MVP的UML](http://7xih5c.com1.z0.glb.clouddn.com/15-10-12/94032090.jpg "简单MVP的UML")

上面一张简单的MVP模式的UML图，从图中可以看出，使用MVP，至少需要经历以下步骤：

 1. 创建IPresenter接口，把所有业务逻辑的接口都放在这里，并创建它的实现PresenterCompl（在这里可以方便地查看业务功能，由于接口可以有多种实现所以也方便写单元测试）
 2. 创建IView接口，把所有视图逻辑的接口都放在这里，其实现类是当前的Activity/Fragment
 3. 由UML图可以看出，Activity里包含了一个IPresenter，而PresenterCompl里又包含了一个IView并且依赖了Model。Activity里只保留对IPresenter的调用，其它工作全部留到PresenterCompl中实现
 4. Model并不是必须有的，但是一定会有View和Presenter

通过上面的介绍，MVP的主要特点就是把Activity里的许多逻辑都抽离到View和Presenter接口中去，并由具体的实现类来完成。这种写法多了许多IView和IPresenter的接口，在某种程度上加大了开发的工作量，刚开始使用MVP的小伙伴可能会觉得这种写法比较别扭，而且难以记住。其实一开始想太多也没有什么卵用，只要在具体项目中多写几次，就能熟悉MVP模式的写法，理解TA的意图，以及享♂受其带来的好处。

扯了这么多，但是好像并没有什么卵用，毕竟
>Talk is cheap, let me show you the code!

所以还是来写一下实际的项目吧。

## MVP模式简单实例
![Login](http://7xih5c.com1.z0.glb.clouddn.com/15-10-12/87960424.jpg)

一个简单的登录界面（实在想不到别的了╮(￣▽￣")╭），点击LOGIN则进行账号密码验证，点击CLEAR则重置输入。

![Login代码结构](http://7xih5c.com1.z0.glb.clouddn.com/15-10-12/63555794.jpg)

项目结构看起来像是这个样子的，MVP的分层还是很清晰的。我的习惯是先按模块分Package，在模块下面再去创建**model、view、presenter**的子Package，当然也可以用**model、view、presenter**作为顶级的Package，然后把所有的模块的model、view、presenter类都到这三个顶级Package中，就好像有人喜欢把项目里所有的Activity、Fragment、Adapter都放在一起一样。

首先来看看LoginActivity
{% codeblock LoginActivity.java https://github.com/kaedea GitHub %}
public class LoginActivity extends ActionBarActivity implements ILoginView, View.OnClickListener {

	private EditText editUser;
	private EditText editPass;
	private Button   btnLogin;
	private Button   btnClear;
	ILoginPresenter loginPresenter;
	private ProgressBar progressBar;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);

		//find view
		editUser = (EditText) this.findViewById(R.id.et_login_username);
		editPass = (EditText) this.findViewById(R.id.et_login_password);
		btnLogin = (Button) this.findViewById(R.id.btn_login_login);
		btnClear = (Button) this.findViewById(R.id.btn_login_clear);
		progressBar = (ProgressBar) this.findViewById(R.id.progress_login);

		//set listener
		btnLogin.setOnClickListener(this);
		btnClear.setOnClickListener(this);

		//init
		loginPresenter = new LoginPresenterCompl(this);
		loginPresenter.setProgressBarVisiblity(View.INVISIBLE);
	}

	@Override
	public void onClick(View v) {
		switch (v.getId()){
			case R.id.btn_login_clear:
				loginPresenter.clear();
				break;
			case R.id.btn_login_login:
				loginPresenter.setProgressBarVisiblity(View.VISIBLE);
				btnLogin.setEnabled(false);
				btnClear.setEnabled(false);
				loginPresenter.doLogin(editUser.getText().toString(), editPass.getText().toString());
				break;
		}
	}

	@Override
	public void onClearText() {
		editUser.setText("");
		editPass.setText("");
	}

	@Override
	public void onLoginResult(Boolean result, int code) {
		loginPresenter.setProgressBarVisiblity(View.INVISIBLE);
		btnLogin.setEnabled(true);
		btnClear.setEnabled(true);
		if (result){
			Toast.makeText(this,"Login Success",Toast.LENGTH_SHORT).show();
			startActivity(new Intent(this, HomeActivity.class));
		}
		else
			Toast.makeText(this,"Login Fail, code = " + code,Toast.LENGTH_SHORT).show();
	}


	@Override
	public void onSetProgressBarVisibility(int visibility) {
		progressBar.setVisibility(visibility);
	}
}
{% endcodeblock %}
从代码可以看出LoginActivity只做了findView以及setListener的工作，而且包含了一个ILoginPresenter，所有业务逻辑都是通过调用ILoginPresenter的具体接口来完成。所以LoginActivity的代码看起来很舒爽，甚至有点愉♂悦呢 (/ω＼*)。视力不错的你可能还看到了ILoginView接口的实现，如果不懂为什么要这样写的话，可以先往下看，这里只要记住“LoginActivity实现了ILoginView接口”。

再来看看ILoginPresenter
{% codeblock ILoginPresenter.java https://github.com/kaedea GitHub %}
public interface ILoginPresenter {
	void clear();
	void doLogin(String name, String passwd);
	void setProgressBarVisiblity(int visiblity);
}
{% endcodeblock %}

{% codeblock LoginPresenterCompl.java https://github.com/kaedea GitHub %}
public class LoginPresenterCompl implements ILoginPresenter {
	ILoginView iLoginView;
	IUser user;
	Handler    handler;

	public LoginPresenterCompl(ILoginView iLoginView) {
		this.iLoginView = iLoginView;
		initUser();
		handler = new Handler(Looper.getMainLooper());
	}

	@Override
	public void clear() {
		iLoginView.onClearText();
	}

	@Override
	public void doLogin(String name, String passwd) {
		Boolean isLoginSuccess = true;
		final int code = user.checkUserValidity(name,passwd);
		if (code!=0) isLoginSuccess = false;
		final Boolean result = isLoginSuccess;
		handler.postDelayed(new Runnable() {
			@Override
			public void run() {
				iLoginView.onLoginResult(result, code);
			}
		}, 3000);

	}

	@Override
	public void setProgressBarVisiblity(int visiblity){
		iLoginView.onSetProgressBarVisibility(visiblity);
	}

	private void initUser(){
		user = new UserModel("mvp","mvp");
	}
}
{% endcodeblock %}
从代码可以看出，LoginPresenterCompl保留了ILoginView的引用，因此在LoginPresenterCompl里就可以直接进行UI操作了，而不用在Activity里完成。这里使用了ILoginView引用，而不是直接使用Activity，这样一来，如果在别的Activity里也需要用到相同的业务逻辑，就可以直接复用LoginPresenterCompl类了（一个Activity可以包含一个以上的Presenter，总之，需要什么业务就new什么样的Presenter，是不是很灵活（＠￣︶￣＠）），这也是MVP的核心思想
>通过IVIew和IPresenter，把Activity的`UI Logic`和`Business Logic`分离开来，Activity just does its basic job! 至于Model嘛，还是原来MVC里的Model。

再来看看ILoginView，至于ILoginView的实现类呢，翻到上面看看LoginActivity吧
{% codeblock ILoginView.java https://github.com/kaedea GitHub %}
public interface ILoginView {
	public void onClearText();
	public void onLoginResult(Boolean result, int code);
	public void onSetProgressBarVisibility(int visibility);
}
{% endcodeblock %}

代码这种东西放在日志里讲好像除了把整个版面拉长没什么卵用，我把几种自己常用的MVP的写法写成一个Demo项目，欢迎围观和PullRequest：[Android-MVP-Pattern](https://github.com/kaedea/Android-MVP-Pattern)。

## 后记
以上就是我的MVP模式的一点理解，在MVVM模式还没有成熟的现在，我觉得没有比MVP模式更好的替代品了。当然今天写的只是MVP的基础使用，介绍的实例项目也非常简单，看不出MVP的优势，后面还会针对MVP模式写一些日志，就目前能想到的至少包括

- Android常规的开发模式经常被称为MV模式（Model-View），引入数据绑定后的MVVM模式（Model-View-ViewModel），与MVP模式的区别
- 目前我们写ListView的Adapter都喜欢把它写成一个内部类，如果有两个Activity里要用同一个Adapter就比较难了，通过MVP模式，能轻松地复用Adapter（你说已经不用ListView了，这不是重点不是么( ˃◡˂ )）
- MVP模式需要多写许多新的接口，这也是其缺点所在，经过一段时间的实战，我自己已有一种优化的MVP模式，我会试着总结一下，把她拿出来说说

## 附录
- [1] : 我也纠结过**MVP模式**或者**MVP结构**的说法那个跟准确一点，国外普遍的叫法是直接叫**Android MVP**，除此之外有叫**MVP Pattern**的也有叫**MVP Framework/Architecture**，个人认为这应该算是一种代码风格（Code Style），在分类上应该比较类似设计模式（Design Pattern），所以现在我一般称为模式，不过这不是重点，不是吗。( ˃◡˂ )

