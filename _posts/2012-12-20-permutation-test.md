---
published: true
title: 置换检验
layout: post
author: Yu
category: 统计原理
tags:
- 非参数
- 置换

---

昨天，在plob.org写完这篇<q>[permutation test 置换检验](http://www.plob.org/2012/12/19/3176.html "Permutation Test 置换检验")</q>。这是一篇拖了半年的文章。
今天，在这里想说一下Permutation test中的一些小细节。

1. permuation是对已有的样本进行重新排序，打乱之前对照组和实验组的差异。而Bootstrap是从样本中重复抽样。

2. permutation test不需要有样本分布为正态的条件（稍微有点废话，非参的方法就是用来处理不是正态的问题的）。**But resampling in a way that moves observations between the two groups requires that the two populations are identical when the null hypothesis is true—not only are their means the same, but also thire spreads and shapes.** 其实还是得需要是同分布的。

3. 可以使用置换检验的情况：
    3.1 Two -sample problems：当零假设说的是<q>两个同分布的总体</q>时。
    3.2 matched pairs desings：当零假设说的是<q>样本在每对之间只有随即的差异</q>时。
    3.3 Relationships between two quantitative variables：当零假设说的<q>变量是不相关的</q>时。
    
4. 如果你要找个置信区间，我们不需要知道零假设是否成立，那么还是用Bootstrap吧。

> 2015.04.04 update
>
> 我在自己的博客里备份了<q>permutation test 置换检验</q>[这篇文章](https://github.com/yulijia/cn/blob/gh-pages/_posts/2015-04-04-Permutation-Test-article-backup.md)
