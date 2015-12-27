title: "图片加载库Fresco的一个Demo"
categories:
  - Android
tags:
  - android
  - fresco
  - github
  - demo
comments: true
date: 2015-11-08 00:00:00
layout:
link:
clearReading:
metaAlignment:
thumbnailImage: 
coverSize:
coverCaption:
coverMeta:
photos:

---
![02](http://7xih5c.com1.z0.glb.clouddn.com/15-10-25/90791990.jpg)
现在市面上各种图片加载库，性能其实相差不是很大，最主要的区别还是使用方式的复杂程度。Fresco使用起来非常简单，也容易扩展，然而这并不是我喜欢Fresco的主要原因。
<!-- more -->

### 基本信息

GitHub : [Fresco Sample Usage](https://github.com/kaedea/Fresco-Sample-Usage)
作者 : [Kaede](https://github.com/kaedea)
参考 : [fresco](https://github.com/facebook/fresco) [06peng](https://github.com/06peng/FrescoDemo) [frescolib.org](http://frescolib.org/)

### 背景

关于图片加载框架，我用过许多轮子，也有自己写过。目前项目在使用的是一个我基于 Volley 修改而来的 ImageLoader ，但是由于产品天花乱坠的需求，现在已经渐渐改得面目全非了，于是打算换成一个新的轮子，在 Glide 和 Fresco 纠结一段时间后，打算先尝试 Fresco 。

图片加载框架如果不处理好Bitmap的缓存问题就容易引发Bitmap泄露，Bitmap泄露是Android内存泄露的一大原因，而内存泄露又是OOM的主要原因。

Bitmap是非常占用内存的，比普通的Java对象大多了，不释放的话很快就OOM了；如果释放过早，如果有ImageView还用着被释放的Bitmap，当这个ImageView被重绘的时候就会抛IllegalState异常。OOM和IllegalState可是为我项目的崩溃率贡献了好多数据。

Android 3.0(Honeycomb)之前，系统把Bitmap的像素数据放在Native层，所以图片加载框架必须手动做好这些Bitmap的释放工作，Honeycomb之后这些放在虚拟机Heap里，虚拟机会帮我们回收，所以可以不用手动释放。但是由于Bitmap本身非常占用虚拟机的内存，虚拟机的内存很快就不够用了，所以会频繁触发虚拟机的GC(Garbage Collector)，然而GC是非常耗性能的工作，因此也会造成APP的卡顿。好在，Android 5.0(Lollipop) 已经妥善解决这个问题了。

对于Honeycomb之前的Bitmap缓存问题，目前我项目的轮子使用的处理方式是Google推荐的方案，简单说一下就是：设置一个count，如果一个Bitmap被set进一个ImageView就+1，remove放就-1，定期检查这些Bitmap，如果count<=0就回收掉。这个方法能通过测试妹子“机の宝库”的考验，无奈在用户的崩溃日志上看起来还是有导致OOM和IllegalState的情况（天朝水深火日的生态啊），而且这一方法并不能解决Lollipop之前频繁GC造成的卡顿问题。

之所以想换Fresco最主要的原因是
>Fresco会在Lollipop之前，把Bitmap放在Ashmem（系统匿名共享内存），在图片不显示的时候，占用的内存会自动被释放，不需要手动释放，也不会频繁触发GC！这会使得APP更加流畅，减少因图片内存占用而引发的OOM，也能有效避免IllegalState，而且在Honeycomb之前的Android版本的表现也同样优秀（官方宣称）。

总之先把源码看一下，拿来用用看，用数据说话吧。目前只写了一个 Demo 项目，后续打算把笔记整理一下，写成一篇日志。

### Fresco 简介
[Fresco](https://github.com/facebook/fresco)是Facebook开源的一个强大的Android图片加载框架，本项目是一个Fresco用法的Demo项目。

### 项目内容
- 简单地加载一张图片
- 自定义图片的加载，比如ScaleType, Rounded Corner, Circle, Fade Animation, Placeholder, Failure Image, Retry Image, ProgressBar, PressedState Overlay
- 加载Gif以及WebPng动态图片
- 监听图片加载的过程
- 渐进式图片加载
- 调整图片大小
- 加载图片后对图片做一些处理
- 在ListView上的使用
- 在RecyclerView上的使用
- 配合第三方图片控件的使用（PhotoView, SubsamplingSacleImageView, GifDrawable）
- 相关代码段

### Fresco的特性
- 完善的内存缓存和释放机制
- 渐进式图片加载
- 动图支持
- 可高度自定义的UI
- 可高度自定义的图片加载过程

详细信息可以参考[frescolib.org](http://frescolib.org/)

### 预览
![01](http://7xih5c.com1.z0.glb.clouddn.com/15-10-25/67535863.jpg)

![02](http://7xih5c.com1.z0.glb.clouddn.com/15-10-25/90791990.jpg)
