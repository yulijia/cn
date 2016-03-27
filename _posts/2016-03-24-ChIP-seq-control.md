---
published: ture
layout: post
title: "ChIPseq的input对照和IgG对照"
author: Yu
categories: [生物信息]
tags:
- ChIP
- 染色质免疫共沉淀
---

思前想后，还是开了这个目录，要不有些东西写了就归类不能了。

今天谈一下ChIP-seq流程以及数据control的问题。ChIP是染色质免疫共沉淀，基本原理是在活细胞状态下固定蛋白质-DNA复合物，并将其随机切断为一定长度范围内的染色质小片段，然后通过免疫学方法沉淀此复合体，特异性地富集目的蛋白结合的DNA片段，通过对目的片断的纯化与检测，从而获得蛋白质与DNA相互作用的信息。

ChIP-seq的流程中一定要有去除deplication的步骤，虽然网上讨论中大家总是谨慎的回答<q>it depends on...blablabla...</q>。

ChIP中一般会用到对照数据，对照数据就是在不特意富集所研究的蛋白结合的DNA片段情况下，有多少DNA片段可以纯化并检验出来。

一般有两种对照，一种是Mock IP（看看在不用抗体的情况下有哪些蛋白会和DNA结合），另一种是直接检测input DNA。在最后[^1]列出了一个非常好的ChIP教学文档，里面介绍了抓IgG和input DNA究竟是怎么一回事。


首先说input DNA：这是通过整套流程，但没有用抗体去筛选DNA片段时，最后会被纯化下来的DNA片段，即：这些片段不代表同转录因子相结合的区域。
接下来是Mock IP：这是通过类似的ChIP处理，但不抓想研究的蛋白时，纯化出的一些同蛋白相结合的DNA片段。

一般情况下优先选择Input DNA方法，第二种方法有正义（究竟这么抓到的DNA能否做对照？我对此持怀疑态度）。

另外，Treatment和control的处理也需要关注，在call peaks的时候要选择会用Control做校正的方法。
如果是自己处理，查找Treatment的分布信息，也要做校正，否则就像我之间讨论过的[某篇文章](http://yulijia.net/cn/论文笔记/2016/03/08/alternative-splicing.html#5)一样。

### 参考资料

[^1]: [Background Information: Chromatin Immunoprecipitation](http://fg.cns.utexas.edu/fg/course_notebook_chapter_ten.html)

