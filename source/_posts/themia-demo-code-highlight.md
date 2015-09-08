title: Themia Sample - 代码高亮
date: 2015-09-08 20:02:11
layout: 
link: 
categories:
 - Themia
tags: 
 - themia 
 - hexo
 - code

clearReading: false
metaAlignment: left
thumbnailImage: 
coverImage: 
coverSize: 
coverCaption: 
coverMeta: 
photos:

comments: true

---
展示在日志中插入代码块，支持高亮显示，并且有几种显示代码块的模式。
<!-- more -->

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

### Gist

{% gist 996818 %}

### jsFiddle

{% jsfiddle ccWP7 %}

