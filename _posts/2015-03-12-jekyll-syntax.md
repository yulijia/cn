---
published: false
title: Jekyll 语法小节
layout: post
author: Yu 
category: 软件世界
tags:
- Jekyll
- 静态博客
---

最近尝试用Jekyll写个小展示网站，发现Jekyll的功能还是很强大的。之前Ruby很多不熟悉的语法，现在也都能摸索着用在Jekyll的Plugin上。总结记录一下我常用的Jekyll基本语法。

### post头部定义

每写一篇markdown格式的文章，需要在文章的最开始写入一些常规信息变量的取值，具体有:指定模板(layout), 标题(title), 描述(description), 分类(category/categories), tags, 是否发布(published), 以及自定义变量(超级好用)。


```
---
layout:     post
title:      title
category: blog
published: true # default true (可以不写这一行)
---
```



