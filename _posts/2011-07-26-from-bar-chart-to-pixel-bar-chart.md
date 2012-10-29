--- 
published: true
title: 从bar chart到pixel bar chart
layout: post
author: Yu
category: 参会有感
tags:
- bar chart
- 可视化
---
上周末去旁听了可视化研讨会（Visualization Workshop），主题演讲是来自Universität Konstanz的[Daniel A. Keim](http://www.inf.uni-konstanz.de/gk/people/member/keim.html "Prof. Dr. Daniel Keim")教授。我对于他提到的pixel bar chart很感兴趣，搜索了一些资料，来介绍一下从bar chart到pixel bar chart的演化过程。

##Bar chart##

bar chart是大家都很常见的条形图，传统的bar chart只能显示很少的一部分数据。

**例1.等宽条形图：**

有一周车辆销售数据  （例子和图片生成程序源自：[Producing Simple Graphs with R](http://www.harding.edu/fmccown/R/#autosdatafile "Producing Simple Graphs with R #Bar Charts#")）

>cars trucks suvs   
1        2        4     
3        5        4     
6        4        6     
4        5        6     
9        12      16     



例如：要表示汽车的一周销量1、3、6、4、9，就可做出如下的条形图。

!["Cars"](http://i.imgur.com/Yb7iu.png "Cars")

图的横轴为日期，纵轴为销售总量，条形高度代表销售量。

若要表示汽车、卡车、suvs的一周销售量，则可做出这样的条形图

<a href="http://yulijia.net/cn/wp-content/uploads/2011/07/Autos.png"><img class="alignnone size-medium wp-image-14" title="Autos" src="http://yulijia.net/cn/wp-content/uploads/2011/07/Autos-300x245.png" alt="" width="300" height="245" /></a>

这时横轴表示三种车辆（并且销售数据按日期的排序），纵轴为销售总量，条形高度代表销售量。

如果还想把总销量表示在图中，则需要这样

<a href="http://yulijia.net/cn/wp-content/uploads/2011/07/Autos01.png"><img class="alignnone size-medium wp-image-15" title="Autos01" src="http://yulijia.net/cn/wp-content/uploads/2011/07/Autos01-300x245.png" alt="" width="300" height="245" /></a>

横轴代表日期，纵轴代表销售总量，每个竖条分成3部分，分别代表不同车辆的销售数据。

以上三个条形图在数据值小的类别上方都留有很大的空白区域，这也是等宽条形图的缺点。

**例2.等高条形图：**

为了解决空间浪费的问题，可以使用等高条形图。

例如表示上面的汽车、卡车、suvs的一周销售量

        CODE： 

        barplot(rep(1,length(as.matrix(autos_data))),width=as.matrix(autos_data), main="Autos",  beside=TRUE, col=rainbow(5))
        
<a href="http://yulijia.net/cn/wp-content/uploads/2011/07/Autos03.png"><img class="alignnone size-medium wp-image-18" title="等高条形图" src="http://yulijia.net/cn/wp-content/uploads/2011/07/Autos03-300x245.png" alt="" width="300" height="245" /></a>

等高条形图的缺陷是无法从图中看出准确的数值（就是指上图中的车辆销售量）。

##Pixel bar chart##

pixel bar chart是在原有bar chart的基础上，将每个数据用一个像素为代表显示在图中，像素在图中有坐标位置和颜色这两个指标值（Daniel A. Keim老师的意思是bar chart加上x-y diagrams），故可以显示数据的多个指标，并可在有限的空间展示大量数据。

<a href="http://yulijia.net/cn/wp-content/uploads/2011/07/pixelbarchart.png"><img class="alignnone size-medium wp-image-35" title="pixelbarchart" src="http://yulijia.net/cn/wp-content/uploads/2011/07/pixelbarchart-300x204.png" alt="" width="300" height="204" /></a>

（图像来源于论文：Pixel bar charts: a visualization technique for very large multi-attributes data sets）

像素条形图的优势是可在一张图中展示大量的多属性数据，例如下图。

这是一个在电子商务中应用的例子，图中的每个像素代表一位顾客，每个条形代表一类产品。a图中的颜色代表顾客的购物总额，b图中的颜色代表访问次数，c图中的颜色代表浏览数量。（从图中可以很直观地看出顾客的购买倾向）
<a href="http://yulijia.net/cn/wp-content/uploads/2011/07/pixelbarchart01.png"><img class="alignnone size-medium wp-image-41" title="Multi-pixel bar charts" src="http://yulijia.net/cn/wp-content/uploads/2011/07/pixelbarchart01-300x149.png" alt="" width="300" height="149" /></a>

（图像来源于论文：Pixel bar charts: a visualization technique for very large multi-attributes data sets）

pixel bar chart具体的算法详见论文：Pixel bar charts: a visualization technique for very large multi-attributes data sets （能搜索到免费pdf下载）

下一步，有时间研究一下如何实现。
