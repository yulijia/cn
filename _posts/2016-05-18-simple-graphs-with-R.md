---
published: ture
layout: post
title: "R画图速查手册"
author: Yu
categories: 可视信息
tags:
- ggplot2
- graphics
- R
- 统计图形
- Tufte 
- Rmarkdown
- Bookdown
---

最近在写R画图的速查手册，写这个东西主要是记录学习R的基本画图命令。除此之外，还学习了Rmarkdown Tufte样式的使用。
不得不提，用这个样式编写绘图类的文档，不如使用普通的书籍格式方便。$\LaTeX$编写文档时图表与正文不一定能紧密相连。
基本上前面添加两句话，后面的图位置就全都跑了，在这个版式里该问题由为突出，主要是Tufte包里没有页面内部的交叉引用功能。
用了2天后，我就转向了Bookdown包，这个包是Xie Yihui从手术室出来后连续几个月不间断工作完成的新包，但是基本命令我还没有掌握，
所以第一版的速查手册是用Tufte包完成的。第一版里面对于排版以及大纲逻辑都不太清晰，以后的更新中会有较大改动。

PDF版文件在这里[下载](http://yulijia.net/projects/SimpleGraphswithR.pdf)，会持续更新。

Bookdown包目前编译pdf文档采用的命令是`bookdown::render_book("index.Rmd", "bookdown::pdf_book")`。注意**首先**要将R工作目录跳转到需要编译的文档目录下，否则会找不到要编译的文件。
不能在函数中以添加路径的方式来编译，因为找不到需要涵盖到书籍里的所有文档（这是错误的->`render_book("/root/bookfiles/index.Rmd")`）。

#### 参考资料

[ 一篇文章、一本書的完整結構](http://www.cs.pu.edu.tw/~wckuo/doc/latex123/node12.html)
