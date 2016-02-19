---
published: ture
layout: post
title: "贝叶斯理论在21世纪的作用，统计功效与样本大小"
author: Yu
categories: 
- 论文笔记
- 统计原理
tags:
- 贝叶斯
- 统计功效
- Bradley Efron
---


今天看了两个短篇，大神Efron给science在2年半前写的贝叶斯理论在21世纪的作用<q>Bayes’ Theorem in the 21st Century</q>；
Nature Methods有个系列讲统计显著性points of significance之中的<q>Power and sample size</q>。

重新读完之后感到，统计和生物是密不可分的，做生物不懂统计，得到的结果就失去了指导实践的意义。

Efron大神的短篇主要讲贝叶斯是非常有用滴，从1763年至今，越来越有用，在上世纪50年代我们有了**经验贝叶斯**这个工具。
该工具在新世纪的大数据统计中焕发光彩。贝叶斯统计让Nate Silver在2012年美国总统大选中百分百预测了50个州的结果。
现在我们还可以结合FDR来用这个工具。当然，贝叶斯也不是万能的，我们总要有其他工具来检测我们的贝叶斯结果是否合理，就是频率理论。

### 关于显著程度

我们总是说某个假设检验结果显著，那么究竟怎么样才叫真正的显著呢？起码type I error 在0.05，统计功效（整体1减去type II error）在0.80。

如下图中的b所示，即便功效达到0.8，也有可能出现阳性预测率仅仅为0.64的情况。这是因为只有10%的假设是有效的（not null）

![Imgur](http://i.imgur.com/n291Ycl.png)


用效应值$$d=(\mu_A-\mu_0)/\sigma$$可以来度量零假设分布和备择假设分布之间的差异。

理想情况下，我们希望在type I error 一定的情况下，power越大越好。
达到这个目的有两种方式，一种是用多样本集（参见下图a）， 另一种是增大效应值d（下图b）。

![Imgur](http://i.imgur.com/J7mwLsX.png)

所以做试验要有尽量多的生物学重复，会适当减小统计功效太小的问题。
