title: "Themia 演示 - hexo tag plugins"
date: 2015-09-28 20:30:05
categories:
 - Themia
tags:
- tag plugins
- thmeia
- hexo
thumbnailImage: post-thumb.jpg
coverImage: post-cover.jpg
clearReading: true

---
`Tag plugins`并不是日志的标签`tag`，它们大都是来自`Octopress`的插件，能够方便得在日志里插入一些特殊的内容。
This post is used to show how tag plugins are displayed. See [docs](http://zespia.tw/hexo/docs/tag-plugins.html) for more info.
<!--more-->

## Block Quote (blockquote)

### Normal blockquote

> Praesent diam elit, interdum ut pulvinar placerat, imperdiet at magna.

### Quote from a book

{% blockquote David Levithan, Wide Awake %}
Do not just seek happiness for yourself. Seek happiness for all. Through kindness. Through mercy.
{% endblockquote %}

### Quote from Twitter

{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NEW: DevDocs now comes with syntax highlighting. http://devdocs.io
{% endblockquote %}

### Quote from an article on the web

{% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Welcome to Island Marketing %}
Every interaction is both precious and an opportunity to delight.
{% endblockquote %}

## Wide image (wide_image)

{% wide_image http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891412/car-1.jpg "Mercedes SLS" %}

## Image (image)


{% image fancybox fig-100 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891400/car-15.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_750/v1438891400/car-15.jpg %}

{% image fancybox nocaption fig-50 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891396/car-4.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_375/v1438891396/car-4.jpg"Ferrari" %}
{% image fancybox nocaption fig-50 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891357/car-12.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_375/v1438891357/car-12.jpg "BMW i8 Concept" %}

{% image fancybox nocaption fig-33  http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891350/car-14.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_250/v1438891350/car-14.jpg %}
{% image fancybox nocaption fig-33 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891405/car-9.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_250/v1438891405/car-9.jpg %}
{% image fancybox nocaption fig-33 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891391/car-2.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_250/v1438891391/car-2.jpg %}

{% image right fancybox fig-75 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891390/car-11.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_560/v1438891390/car-11.jpg %}
{% image right fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891365/car-8.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438891365/car-8.jpg %}
{% image right fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891355/car-10.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438891355/car-10.jpg %}
{% image right fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891351/car-5.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438891351/car-5.jpg %}

{% image fancybox fig-50 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438891417/car-13.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_375/v1438891417/car-13.jpg %}
{% image fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892912/car-17.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438892912/car-17.jpg %}
{% image fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892910/car-18.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438892910/car-18.jpg %}
{% image fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892909/car-19.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438892909/car-19.jpg %}
{% image clear fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892909/car-20.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438892909/car-20.jpg %}

{% image fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892909/car-21.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438892909/car-21.jpg %}
{% image fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892905/car-22.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438892905/car-22.jpg %}
{% image fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892904/car-23.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438892904/car-23.jpg %}
{% image clear fancybox fig-25 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892894/car-24.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_185/v1438892894/car-24.jpg %}

{% image fig-20 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892892/car-25.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_150/v1438892892/car-25.jpg %}
{% image fig-20 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892892/car-26.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_150/v1438892892/car-26.jpg %}
{% image fig-20 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892888/car-27.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_150/v1438892888/car-27.jpg %}
{% image fig-20 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892878/car-28.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_150/v1438892878/car-28.jpg %}
{% image clear fig-20 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438892877/car-29.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_150/v1438892877/car-29.jpg %}
{% image fig-20 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438893632/car-35.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_150/v1438893632/car-35.jpg %}
{% image fig-20 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438893641/car-30.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_150/v1438893641/car-30.jpg %}
{% image fig-20 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438893639/car-31.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_150/v1438893639/car-31.jpg  %}
{% image fig-20 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438893637/car-32.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_150/v1438893637/car-32.jpg %}
{% image clear fig-20 http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/v1438893635/car-34.jpg http://res.cloudinary.com/tranquilpeak-hexo-theme/image/upload/w_150/v1438893635/car-34.jpg %}



## Code Block

### Normal code block

```
alert('Hello World!');
```

### With caption

{% codeblock Array.map %}
array.map(callback[, thisArg])
{% endcodeblock %}

### With caption and URL

{% codeblock .compact http://underscorejs.org/#compact Underscore.js %}
.compact([0, 1, false, 2, ‘’, 3]);
=> [1, 2, 3]
{% endcodeblock %}

### Gist (gist)

{% gist 996818 %}

### jsFiddle (jsfiddle)

{% jsfiddle ccWP7 %}

## Pullquote (pullquote

### Left 

{% pullquote left %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
{% endpullquote %}

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas tempus molestie arcu, et fringilla mauris placerat ac. Nullam luctus bibendum risus. Ut cursus sed ipsum feugiat egestas. Suspendisse elementum, velit eu consequat consequat, augue lorem dapibus libero, eget pulvinar dolor est sit amet nulla. Suspendisse a porta tortor, et posuere mi. Pellentesque ultricies, mi quis volutpat malesuada, erat felis vulputate nisl, ac congue ante tortor ut ante. Proin aliquam sem vel mauris tincidunt, eget scelerisque tortor euismod. Nulla tincidunt enim nec commodo dictum. Mauris id sapien et orci gravida luctus id ut dui. In vel vulputate odio. Duis vel turpis molestie, scelerisque enim eu, lobortis eros. Cras at ipsum gravida, sagittis ante vel, viverra tellus. Nunc mauris turpis, elementum ullamcorper nisl pretium, ultrices cursus justo. Mauris porttitor commodo eros, ac ornare orci interdum in. Cras fermentum cursus leo sed mattis. In dignissim lorem sem, sit amet elementum mauris venenatis ac.

### Right

{% pullquote right %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
{% endpullquote %}

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ligula justo, lobortis sit amet semper vel, dignissim sit amet libero. Praesent ac tempus ligula. Maecenas at gravida odio. Etiam tristique volutpat lacus eu faucibus. Donec non tempus arcu. Phasellus adipiscing, mauris nec mollis egestas, ipsum nunc auctor velit, et rhoncus lorem ipsum at ante. Praesent et sem in velit volutpat auctor. Duis vel mauris nulla. Maecenas mattis interdum ante, quis sagittis nibh cursus et. Nulla facilisi. Morbi convallis gravida tortor, ut fermentum enim gravida et. Nunc vel dictum nisl, non ultrices libero. Proin vestibulum felis eget orci consectetur lobortis. Vestibulum augue nulla, iaculis vitae augue vehicula, dignissim ultrices libero. Sed imperdiet urna et quam ultrices tincidunt nec ac magna. Etiam vel pharetra elit.