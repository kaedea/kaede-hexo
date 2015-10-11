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
Android **MVP模式**也不是什么新鲜的东西了，我在自己的项目了也普遍地使用了这个设计模式。当项目越来越庞大、复杂，参与的研发人员越来越多的时候，**MVP模式**的优势就充分显示出来了。
<!-- more -->
*导读：MVP模式是MVC模式在Android上的一种变体，介绍MVP就得先介绍MVC。在MVC模式中，Activity应该是属于View这一层。而实质上，它既承担了View，更多地却包含一些Controller的东西在里面。这对于开发与维护来说极度不利，耦合度大高了。把Activity的View和Controller抽离出来就变成了View和Presenter，这就是MVP模式。*

## 什么是MVC模式
MVP模式（Model-View-Presenter）可以说是MVC模式（Model-View-Controller）在Android开发上的一种变种、进化模式。后者大家可能比较熟悉，就算不熟悉也可能或多或少地在自己的项目中用到过。要介绍MVP模式，记不得不先说说MVC模式。MVC模式的结构分为三部分，实体层的Model，视图层的View，以及控制层的Controller层。

![MVC结构](http://7xih5c.com1.z0.glb.clouddn.com/15-10-11/13126761.jpg)

其中View层其实就是程序的UI界面，用于向用户展示数据以及接收用户的输入；而Model层就是JavaBean实体类，用于保存实例数据；Controller控制器用于更新UI界面和数据实例。

例如，View层接受用户的输入，然后通过Controller修改对应的Model实例；同时，当Model实例的数据发生变化的时候，需要修改UI界面，可以通过Controller更新界面。（View层也可以直接更新Model实例的数据，而不用每次都通过Controller，这样对于一些简单的数据更新工作会变得简单许多。）

举个简单的例子，现在要实现一个飘雪的动态壁纸，可以给雪花定义一个实体类Snow，里面存放XY轴坐标数据，View层当然就是SurfaceView（或者其他视图），为了实现雪花飘的效果，可以启动一个后台线程，在线程里不断更新Snow里的坐标值，这部分就是Controller的工作了，Controller里还要定时更新SurfaceView上面的雪花。进一步的话，可以在SurfaceView上监听用户的点击，如果用户点击，只通过Controller对触摸点周围的Snow的坐标值进行调整，从而实现雪花在用户点击后出现弹开等效果。具体的MVC模式请自行Google。

## 重点要说的MVP模式
在Android项目中，Activity和Fragment占据了大部分的开发工作。如果有一种设计模式（或者说结构）专门是为优化Activity和Fragment的代码而产生的，你说这种模式重要不？这就是MVP设计模式。

按照MVC的分层，Activity和Fragment（后面只说Activity）应该属于View层，用于展示UI界面，已经接收用户的输入，此外还要承担一些生命周期的工作。Activity是在Android开发中充当非常重要的角色，特别是TA的生命周期的功能，所以开发的时候我们经常把一些业务逻辑直接写在Activity里面，这非常直观方便，代价就是Activity会越来越臃肿，超过1000行代码是常有的事，如果有进行代码重构经验的人，看到1000+行的类肯定会有所顾虑。因此Activity不仅承担了View的角色，还承担了一部分的Controller角色，这样一来V和C就耦合在一起了，虽然这样写方便，但是如果业务调整的话，要维护起来就难了，而且在一个臃肿的Activity类查找业务逻辑的代码也会非常蛋疼，所以有必要在Activity中，把View和Controller抽离开来，而这就是MVP模式的工作了。

![MVP结构](http://7xih5c.com1.z0.glb.clouddn.com/15-10-11/2114527.jpg)

MVP把Activity中对View的操作抽象成View接口，把业务逻辑的操作成Presenter接口，Model类还是原来的Model。这就是MVP模式，现在这样的话，Activity的工作的简单了，只用来响应生命周期，其他工作都丢到Presenter中去完成。从上图可以看出，Presenter是Model和View之间的桥梁，为了让结构变得更加简单，View并不能直接对Model进行操作，这也是MVP与MVC最大的不同之处。

## MVP模式的作用
MVP的好处都有啥，谁说对了就给他……

- 分离了视图逻辑和业务逻辑，降低了耦合
- Activity只处理生命周期的任务，代码变得更加简洁
- 视图逻辑和业务逻辑分别抽象到了View和Presenter的接口中去，提高代码的可阅读性
- 把业务逻辑抽到Presenter中去，避免后台线程引用着Activity导致Activity的资源无法被系统回收从而引起内存泄露和OOM
- Presenter被抽象成接口，可以有多种具体的实现，所以方便进行单元测试

说了这么多，没看懂？好吧，我自己都没看懂自己写的，我们还是直接看代码吧。

