---
published: ture
layout: post
title: " 119个人类转录因子结合到基因组区域的序列特征和染色质结构分析"
author: Yu
categories: [论文笔记]
tags:
- 组蛋白
- 染色质结构
- 转录因子
---

这篇文章有幸聆听过wengzhiping老师的汇报。当时刚刚开始做这方面的研究，什么都不懂。
现在看看，这篇文章内容丰富，在对问题的提出和验证方面比较合理。

他们使用MEME-ChIP软件来做motif discovery。然后对于每个peak，将E-value最小的作为“主要motif”，将其他E-value显著的作为“二级motif”。

再将这些unique motif（79个）分成已知数据库中的，以及未知的（12个）。文中还说，要注意在MEME中找到的最富集在peak上的“主要motif”不一定是canonical motif。
TF 结合位置一般在DNase I peak的两侧，也就是山谷的位置。他们还分析了未知motif是同一些已知motif的关系。有的未知motif在一些已知motif的peaks里。

接下来是weng老师自己认为比较有意思的一个亮点（她曾讲完后专门问我们感觉是不是很有意思），TF之间的结合关系：
两个TFs是紧挨着结合在DNA序列上，还是一个TF与另一个TF结合，后一个TF结合在DNA序列上？

为了检测这两中假设，他们计算peaks中每种motif的比例：1.peaks中有两个motif；2.peaks中reads绝大多数是非cannonical motif；3.peaks中reads绝大多数是canonical motif。

看这三种的比例，根据比例来判断TFs究竟是如何结合的（参见下图）。

![Imgur](http://i.imgur.com/GJ9JiNG.png)

另外，文中介绍bound motif site是在peaks区域的，unbound motif site是在peaks外的motif site，文中分析bound site区域的DNase I 超敏感位点和TS motifs都富集很多。

接下来，本文还分析了邻近的motif sites是不是同向的，还是反向（也就是如有两个TF，那么它们是结合在同一侧DNA链上，还是结合在互补链上）的，多个motif sites之间的距离是多远，有没有特点。
我觉得这两个问题很有意思，分析结果发现不同的TF之间距离和方向的特点不同。

接下来他们又分析了组织特异性的TF。最后还分析了TF位置同核小体之间的关系。核小体的两侧是有比较多的TF peaks。
大多数TF都喜欢结合在GC含量高，没有核小体，并且DNase I 易感的区域。在DNA序列上核小体被赶走与DNA序列的固有特征无关。
TF喜欢结合到GC含量高区域，这些区域有很多是启动子区域，但是启动子区域的核小体排布很有规律，那么TF同核小体岂不是喜欢往一块凑？
文章中说TFs会结合到赶走核小体或者组织核小体紧密排布的基因组区域。

#### 总结一下这个研究都做了哪些工作？

1. 找序列motifs和TF结合位点
2. 对motifs分类，分别分析已知和未知motifs
3. 比较bound 和 unbound motif sites的特点（在peaks里和不在peaks里的motif）
4. TFs的<q>共结合</q>形式有哪些？3种
5. <q>共结合</q>TFs之间的距离和结合方向偏好性
6. 序列特异性的TFs结合在细胞类型特异性的细胞中
7. 已蛋白蛋白共结合（拴住）这种方式结合的非序列特异性TFs有哪些特点
8. 核小体同TFs的关系
9. 总结TFs与序列结合的3个特点
10. 细胞类型特异性的TFs结合区域的染色质结构
11. 网站Factorbook.org

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|canonical|权威|tethering|拴住|
|repetitive|重复|teratocarcinoma|畸胎瘤|
|deplete|枯竭|oscillatory|震荡性，摆动的|
|striking|显著的|in vivo|体内|
|in vitro|体外|intrinsic|固有的|
|dips|倾角|evict|依法驱逐|
|albeit|虽然|deviate|脱离|
|intrinsically|本质上|anecdotal|轶事|

