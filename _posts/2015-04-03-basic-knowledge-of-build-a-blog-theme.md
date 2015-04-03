---
published: ture
layout: post
date: 2015-04-03
title: 一个博客模版应该包括的内容
author: Yu
category: 所思所悟
tags:
- Jekyll
- 博客模版
---

从去年11月底开始，我下定决心要把自己的Jekyll博客模版改成WordPress Twenty Eleven和Twenty Twelve类似的模式，做了个[Freshman21（读作21st）](https://github.com/yulijia/freshman21/)，并且在github上公布了出来（这句有点像废话，本博客就是放在github pages的）。
并且在jekyllthemes.org做了宣传，三个月下来，有不少Jekyll博客的用户使用了我的模版，并且给我的模版纠正了很多错误的地方，非常感谢这些热心的用户。
那么，接下来想总结一下“一个博客模版必备的元素”。

### 1.基本Html+CSS应该包括的内容

- Table of Content
- h1,h2,h3,h4,etc.
- Blockquotes
- Code formatting and highlight
- Table
- font style : cite and bold 
- Responsive web design
- li style
- Open Graph META Tags
- Microdata (schema.org)

### 2.基本的页面应该包括的内容(模块)

- 目录
- 标签
- 自我介绍
- 留言簿
- 版权声明
- 订阅RSS
- 近期文章
- 博客友链
- 博客归档

在上面的项目中，除了“博客归档”需要借助plugin其他都可以用html+css+liquid实现，“博客归档”如果不自己写程序，那么在liquid只能实现按年份的“伪归档”，我的博客模版里就是一个“伪归档”。

### 3.其他附加模块

- Back to top滑动按钮
- google analytics/百度统计
- 分享到按钮
- 站内搜索（推荐google search）
- 异步加载自动展开
- ReadMore 折叠长文章模式

上面所述的模块，设计社交分享，搜索引擎，用户体验，信息统计四个部分。

对于社交分享和统计，如果你的博客是建立在github pages上，请尽量采用国外的社交分享链接和留言系统，我知道这样对于国内读者非常不友好，但是由于GFW<q>温柔注视</q>github的情况时有发生，所以[用国内的产品很可能出现各种莫名其妙的问题](http://yulijia.net/cn/%E7%BD%91%E7%BB%9C%E8%A7%82%E5%AF%9F/2014/12/28/baidu-cdn.html)。
<u>如果你的页面是建立在coding.net这样的国内网站上，并且网站面向国内用户，请禁止使用google系列的所有产品，所有google相关功能都有可替换的国内产品</u>（写完这句，想到自己生活在一个大局域网内，还是挺悲伤的`T_T`）。

站内搜索有两种实现方式，一种是用Jekyll的plugin，在官网上就可以找到，但是这个插件有个弱点，貌似是说文章越多搜索时要缓存的内容越多，搜索速度会变慢。所以，我就采用google site搜索了，国内用户就当作没看见这段话。

用户体验主要想说的是“异步加载自动展开”和“折叠长文章”，前者需要写一些JaveScript，由于我的第一个模版想尽可能的是一个干净的`html+css`模版，所以我就没研究这个内容，不过文章多了，用这个应该用户体验会好些；后者就是在首页只显示博文的一部分内容，需要阅读全文需要点进页面，这个很好实现，用`post.excerpt`或者`post.summary`都可以，条条大路同罗马。
我一开始觉得用`post.summary`[自己写summary的方法比较方便](http://yulijia.net/freshman21/howto/2015/01/18/how-to-create-post-summary.html)，但是后来仔细研究了一下，在模版中采用的是`post.excerpt`方法（我自己博客中没有用，想看效果出门左转找Freshman21）。

### 4.还能做些什么

- cv
- 参考文献的css修饰
- 各种链接的css修饰
- 在多人博客中区分不同作者
- 引用博客文章的权限提示，引用格式
- 数学文章的定理，命题，公里模块的css修饰，炫酷的Q.E.D.

这部分内容只是有想法，没有实现的动力，目前我是一个喜欢极简风格的人。
