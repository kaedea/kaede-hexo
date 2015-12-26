title: "Hexo响应式主题 : Themia"
date: 2015-10-05 14:00:00
layout: 
link: 
categories:
 - Themia
tags: 
 - themia 
 - hexo
 - release

clearReading: false
metaAlignment: left
thumbnailImage: http://7xih5c.com1.z0.glb.clouddn.com/15-10-7/37512301.jpg
coverImage: 
coverSize: 
coverCaption: 
coverMeta: 
photos:

comments: true
---
[Themia](https://github.com/kaedea/hexo-theme-themia)是一个华丽的Hexo响应式主题，由**LouisBarranqueiro**开发的主题[TranquiPeak](https://github.com/LouisBarranqueiro/tranquilpeak-hexo-theme)的基础上改造而来，**大部分功能都是原有主题的**，只是为了我自己的需求做了小部分的修改。
<!--more-->

![](http://7xih5c.com1.z0.glb.clouddn.com/15-10-8/37832013.jpg)

下面是**LouisBarranqueiro**本人对于该主题的介绍：
>Tranquilpeak is a gorgeous responsive theme for Hexo blog framework. It has many features and integrated services to improve user experience.

<!--toc-->

### 基本信息
 - 作者：[Kaedea](https://github.com/kaedea) （基于[TranquiPeak](https://github.com/LouisBarranqueiro/tranquilpeak-hexo-theme)）
 - 环境：[Hexo](https://hexo.io/zh-cn/) 3.0.0 以上
 - 项目：[hexo-theme-themia](https://github.com/kaedea/hexo-theme-themia)

### 主题特点
#### 响应式主题
TranquiPeak主题能够适配宽屏电脑、普通电脑、平板、手机多种分辨率的设备。

在一般情况下，她看起来像是这样的
![PC](http://img-storage.qiniudn.com/15-10-5/88952248.jpg)

平板模式下则是这样
![](http://img-storage.qiniudn.com/15-10-5/27983.jpg)

手机以及更小的屏幕上则是
![](http://img-storage.qiniudn.com/15-10-5/69822281.jpg)

![](http://img-storage.qiniudn.com/15-10-5/55387878.jpg)

总之，响应式设计就是这么狂霸酷拽叼。（然而并没有什么卵用，还有在IE上的一些兼容性问题请无视 (°ー°〃)）

#### 漂亮的边栏 SideBar
TranquiPeak自带有漂亮的侧边栏，可以现实用户头像、用户名、日志向导以及一些自定义入口。
在主题的设置文件`_config.yml`里可以设置SideBar的属性
{% codeblock _config.yml https://github.com/kaedea GitHub %}
# sidebar节点下的menu和author_links是用于分组，三级节点home表示SideBar上面的一个入口
# icon用的是FontAwesome，具体用法Google一下立刻明白
# search的st-search-show-outputs是SwiftType的固定用法，不能改
# 总体的结构为 `groups of links` -> `link` -> `title, link, icon`
sidebar:
    menu:
        home:
            title: global.home
            url: /
            icon: home
        categories:
            title: global.categories
            url: /all-categories
            icon: bookmark
        archives:
            title: global.archives
            url: /all-archives
            icon: bars
        search:
            title: global.search
            url: /#search
            icon: search
            class: st-search-show-outputs

    author_links:
         github:
             title: global.github
             url: https://github.com/kaedea
             icon: github-square
         mail:
             title: global.mail
             url: mailto:kidhaibara@gmail.com
             icon: envelope-o
{% endcodeblock %}

除了设置SideBar的入口之外，还可以设置SideBar的样式。
同样在设置文件`_config.yml`中
{% codeblock _config.yml https://github.com/kaedea GitHub %}
# 设置Sidebar的样式
# 1: 表示在大屏幕显示宽的SideBar，在中屏幕显示窄的SideBar，在小屏幕现实抽屉SideBar（宽）
# 2: 表示在大屏幕和中屏幕显示窄的SideBar，在小屏幕现实抽屉SideBar（窄）
# 3: 在所有屏幕显示抽屉SideBar（宽）
# 4: 在所有屏幕显示抽屉SideBar（窄）
sidebar_behavior: 1

# 是否在全部的日志里都隐藏SideBar（如果为false，也可以单独指定某一篇日志隐藏SideBar）
clear_reading: false
{% endcodeblock %}

#### 可自定义的背景图片 Background CoverImage
可以给整个主题设置一个背景图片，通常情况下只会在SideBar部分显示背景图片，日志部分会被日志的背景颜色遮挡。在打开`About`卡片的时候，就能看到整张背景图片。
在设置文件`_config.yml`中
{% codeblock _config.yml https://github.com/kaedea GitHub %}
# 可以直接使用外链图片
# 可以把图片放在`source/assets/images/`中，然后用以下方式使用图片
cover_image: /assets/images/cover_miku.jpg
{% endcodeblock %}

#### 简洁的**关于我**卡片 About Page
**About Page**是TranquiPeak主题的一个特色功能，用简洁的卡片显示博主的简要信息，点击SideBar的头像则可以打开**About Page**。
![](http://7xih5c.com1.z0.glb.clouddn.com/15-10-5/63215622.jpg)

在设置文件`_config.yml`中
{% codeblock _config.yml https://github.com/kaedea GitHub %}
# Author
# 你可以在`languages`文件夹中修改你的个人信息
author:
    email: kidhaibara@gmail.com
    location: Chiba Japan
    picture: avatar_01.png
    twitter
    google_plus:
{% endcodeblock %}

#### 支持国际化语言(i18n)
**Language(i18n)**是**Hexo**的一个功能，TranquiPeak主题也支持该功能，只要在`\themia\languages\`文件夹下增加对应语言的YML文件，并在Hexo的`_config.yml`中，把language标签设置为指定的语言，即可把主题的语言环境切换到改语言。

例如，在`\themia\languages\`的`en.yml`文件，可以进行这样的设置
{% codeblock en.yml https://github.com/kaedea GitHub %}
global:
    home: "Home"
    categories: "Categories"
    tags: "Tags"
    archives: "Archive"
    ...
pagination:
    newer_posts: "Previous"
    older_posts: "Next"
    ...
post:
    toc: "Table of Contents"
    read_more: "Continue reading"
    go_to_website: "Go to website"
    ...
author:
    bio: "話は安いものですので、コードを表させてください！"
    job: "Android Developer"
{% endcodeblock %}


#### 搜索 Swiftype
TranquiPeak主题自带了[Swiftype](https://swiftype.com/)搜索功能，使用此功能，必须先到[Swiftype](https://swiftype.com/)申请**Install Key**，再把它填写到主题配置文件的`swiftype_install_key`标签。


### 日志功能

#### 日志缩略图 Post ThumbnailImage
缩略图是TranquiPeak主题的特色功能，在日志的主页里，会显示日志的缩略信息。除此之外，你还可以给日志设定一个缩略图。
下面是有缩略和无缩略图的情况
![](http://7xih5c.com1.z0.glb.clouddn.com/15-10-5/36810674.jpg)

给日志设置一张缩略图，只需要在日志的`.md`文件里设置
{% codeblock post.md https://github.com/kaedea GitHub %}
title: "开始将博客搬迁到HEXO"
date: 2015-04-09 02:04:58
categories: Whisper
tags: 随笔
# 设置日志缩略图，可以是外链，也可以是相对路径
thumbnailImage: thumbnail_02.jpg
{% endcodeblock %}


#### 日志封面图 Post CoverImage
封面图也是TranquiPeak主题的特色功能，在日志里，你可以设置一张大的海报作为日志的封面，具体效果可以参考[CoverImage Post](http://kaedea.com/demo-themia/2015/09/29/themia-demo-cover-image/)。

给日志设置一张封面图，只需要在日志的`.md`文件里设置
{% codeblock post.md https://github.com/kaedea GitHub %}
# 表示该日志隐藏SideBar
clearReading: true
# 日志的副标题居中
metaAlignment: center
# 日志的封面图
coverImage: post-cover.jpg
# 封面图的大小
coverSize: full
# 封面的标题
coverCaption: 
# 是否在封面上现实日志的标题和副标题
coverMeta: out
{% endcodeblock %}


#### 多种图片展示方式
图片是一般日志必不可少的元素，TranquiPeak主题提供了多种在日志中显示图片的方式。

一般图片
![](http://7xih5c.com1.z0.glb.clouddn.com/15-10-7/35511032.jpg)
宽屏图片
![](http://7xih5c.com1.z0.glb.clouddn.com/15-10-7/70294173.jpg)
FancyBox
![](http://7xih5c.com1.z0.glb.clouddn.com/15-10-7/51537048.jpg)

具体情况可以参考[Themia 演示 - demostrate image](http://kaedea.com/demo-themia/2015/09/28/themia-demo-image-demo/)


#### 相册型日志 Gallery Post
并不是所有的日志的主体都是文字哈，有时候可以发布一组图片作为日志，这时候当然要选用高大上的**Gallery Post**了，具体效果可以参考[Themia 演示 - image gallery post](http://kaedea.com/demo-themia/2015/09/05/themia-demo-image-gallery/)。


#### 日志分享功能
TranquiPeak主题自带了**Twitter**、**Facebook**、**Google+**的分享功能，不过这些功能对于国内的用户可能有点鸡肋，所以Themia主题增加了**新浪微博**、**人人网**和**QQ空间**的分享功能。

具体修改过程可以参考[网页分享按钮与接口的使用](http://chichele.li/2015/06/17/%E7%BD%91%E9%A1%B5%E5%88%86%E4%BA%AB%E6%8C%89%E9%92%AE%E4%B8%8E%E6%8E%A5%E5%8F%A3%E7%9A%84%E4%BD%BF%E7%94%A8/)。


#### 日志评论功能 Disqus
TranquiPeak主题自带了**Disqus**用户评论系统（这也是静态博客能与其他用户交流的关键），许多国内的用户会觉得**Disqus**在国内水土不服，偏向于用**多说**系统，但是我认为**多说**系统的主题风格与TranquiPeak主题有点格格不入，所以还是保留使用**Disqus**。

如果你想修改**Disqus**，可以参考[Hexo tranquilpeak主题使用多说评论系统](http://chichele.li/2015/06/14/Hexo%20tranquilpeak%E4%B8%BB%E9%A2%98%E4%BD%BF%E7%94%A8%E5%A4%9A%E8%AF%B4%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F/)。


#### 其他功能

- Hexo Tag Plugins 支持 [Themia 演示 - hexo tag plugins](http://kaedea.com/demo-themia/2015/09/28/themia-demo-hexo-tag-plugins/)
- 同时支持**Markdown**和**Html** [Themia 演示 - archive elements](http://kaedea.com/demo-themia/2015/09/12/themia-demo-elements/)
- 使用视屏、音乐等资源 [Themia 演示 - insert music & video](http://kaedea.com/demo-themia/2015/09/06/themia-demo-video/)


### Themia做了哪些更改？
感谢**LouisBarranqueiro**为我们带了这么棒的一个主题，我也是花了好几周的时间，研究对比各种`Hexo主题`，最后才确定**TranquiPeak**比较符合我的需求。

Themia主要在TranquiPeak的基础上做了以下一些修改

#### 调整日志的宽度
TranquiPeak的日志宽度最高是750px，这个在1336宽的笔记本上看还不错，但是在1920的显示器上，日志区就只有不到一半的宽度，感觉还是不够的，所以我把大屏显示器分辨率下日志的宽度改成80%。

#### 修改字体
TranquiPeak的字体用的是Google的WebFont，默认的比较适合外国人的审美，但是就是不是很适合我，特别是标题和对中日文字的显示不是很好，因此我使用了Google的思源黑体和Microsoft的微软雅黑，标题的FontFamily是`Verdana, Geneva, 'Open Sans', SimHei, "Noto Sans", "Noto Sans CJK SC", 'Microsoft Yahei', sans-serif;`，正文的FontFamily是`'Open Sans', "Noto Sans", "Noto Sans CJK SC", 'Microsoft Yahei', sans-serif;`，以后估计还有改进的地方。

#### 修改字体颜色的配色
我参考了Google提供的Material Design Color Palette，对TranquiPeak的标题、副标题、分割线、导航栏等地方的颜色进行修(tu)改(ya)。

#### 增加图片加载的淡入动画
所有图片第一次加载的时候会启动淡入动画，这里其实还是不是很完美，我本意是喜欢日志的图片不要一次性全部加载的，而是滚动到哪里才加载当前的图片（也就是传说中的懒加载），可是折腾了好多都没能搞定，所以暂时先折中，**亟待改进**。

#### 日志缩略图居中截取
TranquiPeak的日志缩略图是一个亮点，但是原本的缩略图是固定长宽的，无论你使用什么图片都会拉伸或压缩填满，我把这改成了居中截取（CenterCrop），在IE上没有效果。

#### 修改分享功能
原本的日志分享功能基本是满足外国人用的，所以我增加了微博、QQ空间等分享功能，嘛，用的是JiaThis的功能，要添加什么分享都很容易就是。

#### 其他
其实还是有很多细节的修改，我算是进坑了就是 ╮(￣▽￣")╭。

