---
published: ture
layout: post
title: "可变剪接相关文献"
author: Yu
categories: [论文笔记]
tags:
- 可变剪接
- Benjamin J. Belencowe
- Yoseph Barash
- entropy
---

本文将总结一些看过的可变剪接文章，大致勾画出我关注的可变剪接研究相关历程。

另外，从今天开始我会在标签中添加一些关注的研究者。

### 1.Alternative splicing: decoding an expansive regulatory layer

这篇综述是Benjamin J. Belencowe实验室出品的。讲了很多比较有意思的工作，另外引用文献对重要论文做了简要描述。

我比较感兴趣的是有工作是预测扰乱剪接的mutation。

> In related work [63], a computational method was developed for predicting splicing disrupting mutations by exploiting the principle that the preferred binding location of a splicing factor with respect to splice sites is directly correlated with its positive-acting function, whereas a mutation that creates a binding site for the splicing factor in the ‘wrong’ location is expected to disrupt splicing. 

文章里的几个点：
1. 蛋白质RNA相互作用的分析（CLIP-seq，HITS-CLIP，PAR-CLIP）
2. H3K36me3和H3K9me3对剪接的影响。（组蛋白、核小体、染色质层面对转录可剪接的影响）
3. CTCF与剪接
4. 今后如何结合ncRNA和antisense transcripts来分析可变剪接

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|stride|跨步，大步|fully-committed|完全依赖|
|genotoxic|遗传毒性|perturbation|不安，摄动|
|nascent|初期|inhibit|抑制|
|polyadenylation|多腺苷酸化|synergize|起增效剂作用，协同加强的活动|
|lofty|高耸的|elicit|引出|
|trigeminal ganglion|三叉神经节|infrare|红外线|
|pivotal|中枢，关键|myelodysplasia|脊髓发育不良|
|prognosis|预后|autism spectrum disorder|自闭症谱系障碍|
|amyotrophic lateral sclerosis|肌萎缩侧索硬化|frontotemporal lobar degeneration|额颞叶变性|


### 2.Entropy Measures Quantify Global Splicing Disorders in Cancer

这篇文章估计看过的人都留下了深刻的印象，文章里用Shannon entropy来度量剪接失调（混乱）的程度（参见下图）。

文章中用癌症和正常样本做对比，说明了在癌症中转录本的剪接失调情况会很多。
剪接失调的基因中很多是剪接因子。
并且文章通过以往数据分析了剪接失调同癌症的细胞增殖有着一定的关系。

![Imgur](http://i.imgur.com/mvXH1JL.png)


### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|perturbation|忧虑，不安，摄动|surrogate|代理|
|foetal|胎儿|||


### 3.Expression of 24,426 human alternative splicing events and predicted cis regulation in 48 tissues and cell lines

本文用的是microarray数据来检测cassette exon splicing的情况，主要监测了inclusion和exclusion的**已知**cassette exon。比较老，2008年的文章，有chaolin zhang参与。

在不同组织中有剪接的exon的表达情况各不相同。
他们围绕调控的外显子抽取8个区域（区域见下图）的序列，在序列中找4mer到7mer的“words”，对看这些words的富集情况，从而获得剪接相关的调控元件。

![Imgur](http://i.imgur.com/Ij77696.png)

之后是对高精度RNA可见剪接图谱的研究，对每种检测到的关键motif的特点和潜在功能进行分析，并预测RNA结合蛋白和motif之间的关系。



### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|*in silico*|电脑模拟|*in vivo*|生物活体内|
|*in vitro*|生物活体外|pyrimidine|嘧啶|


### 4.Estimation of alternative splicing variability in human populations

这篇文章评估了可变剪接多样性在两个人群（高加索人，尼日利亚人）里的相同点和差异。

文章中采用CV（coefficient of variation）对基因和转录本的表达量多样性进行了评估，采用splicing ratio $$f_i=\frac{x_i}{\lambda}$$（即某个剪接形式的转录本拷贝数$$x_i$$占这个基因所有转录本拷贝数$$\lambda$$的比例）
结论是基因表达比splicing ratio对于转录本富集的调控贡献较大。

文中将使用同一个TSS的转录本定义位一个基因的转录本，一开始研究了lncRNA然后发现lncRNA看不出什么明显结论，
就只研究mRNA了，在研究时用到了[**Hellinger distance**](https://en.wikipedia.org/wiki/Hellinger_distance)来球splicing ratio的variability（变化程度）。

分析方法和数据对比（在两个人群中）应该是这篇文章的优点。

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|deconvolute|去卷积|Caucasian|高加索人，白人|
|Yoruban|约鲁巴人|Nigerian|尼日利亚人|
|overdispersion|不平均分布，过离散|centroid|质心|

### 5.Epigenetic features are significantly associated with alternative splicing

这篇文章是出自Tian Weidong老师的实验室。主要刻画了表观遗传学特征同可变剪接的关系。
我很早之前在JC上讲过，感觉是一篇细节问题较多的文章。

具体来说文章里研究了组蛋白修饰，9个转录因子，CTCF和RNA Pol II同可变剪接外显子的关系。
这个文章中有很多小问题，感觉做得不严谨，主要在于对表观遗传学数据，并不是所有的都减去input做标准化。

首先，文章一开始的背景里说剪接事件可以分为：cassette exon, exon skipping, blablabla的，我就没弄清楚这里专门指出的 cassette exon 同 exon skipping 的区别在哪里。
我还专门翻了翻后面带的那两篇引用文章，写得都是cassette exon。在result部分就没再出现cassette exon，只用了exon skipping，且这里特指skip单个exon的情况（即不会连续2个或以上的exon都被skip）。

还有就是，研究的数据有一部分同前面我做过笔记的文章中的类似，用的都是ENCODE的RNA-seq外加组蛋白修饰、转录因子，CTCF以及RNA Pol II的数据。
计算的时候还一般都从bam或者wig文件开始，有没有考虑过实验之间的差异性以及如何度量或者减少这类问题？这些数据的mapping质量到底怎么样？

文中最逗的就是关于组蛋白修饰和input的问题，在Figure2中没有做control(input)的处理，但是在Figure6中就做了input的矫正。
也就是文中的最后一个小节专门讲述矫正后的结果是什么样子。
另外在附录里有Figure2情况下input的数据分布情况。为什么不全部矫正后画图呢？像这样有时做矫正，有时不做矫正，会对理解造成困扰。
感觉像是在review后添加了矫正的内容。

还要再啰嗦一句，文中使用的那个对转录本分类的脚本，我也没测试成功，可能是我的输入数据里面有处理不了的转录本。

整篇文章中介绍的方法是可取的，只是很多不严谨的地方，让结果不是那么可信。

*（这个系列未完待续，每次更新5篇为一个post）*
