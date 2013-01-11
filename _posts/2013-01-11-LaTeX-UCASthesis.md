
--- 
published: true
title: 国科大（UCAS）学位论文LaTeX模板
layout: post
author: Yu
category: 格式技巧
tags: 
- LaTex
- 论文模板

---
**用了2天时间，边学边改，写了个半成品的国科大学位论文LaTeX模板。我想这个学位论文应该是用中文写的最后一篇论文了。使用LaTeX排版中文，实在是有太多的不方便，所以我决定以后使用LaTeX时一律写英文文档。**

模板的下载地址：[https://github.com/yulijia/LaTeX_UCASthesis](https://github.com/yulijia/LaTeX_UCASthesis)

可以用<code>git clone https://github.com/yulijia/LaTeX_UCASthesis.git</code>命令将其clone到本地。

这个模版基于中科院电工所Tao Wang所写的[CASThesis LyX模版](http://code.google.com/p/cas-lyx-template/)，经简化改造成，没有用到自制类.cls文件，是一个代码比较”脏“但是直观可见的模板。

版本号：1.0 beta


###尚存在的问题

1. 复制出的英文会乱码，写模板时我使用的是CJK包，不知道为何英文文字无法正确的复制下来，估计和编码格式有关。

2. 无法生成中文索引，这个问题太恶心了，我所用的编译环境是Gummi集成的，搜索了所有网上关于中文索引乱码的解决办法，不管是自己编译还是用Gummi直接编译，都无法做到没有乱码，所以该模板不具有索引功能。

