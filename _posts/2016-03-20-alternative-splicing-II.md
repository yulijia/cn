---
published: ture
layout: post
title: "可变剪接相关文献II"
author: Yu
categories: 论文笔记
tags:
- 可变剪接
- SVM
- Alu
- Yi Xing
- motif
- TFBS
- 转录调控元件
---

### 1.Accurate identification of alternatively spliced exons using support vector machine

这篇文章发表了10多年了，是介绍SVM如何用于区分可变剪接外显子的。
如果想了解机器学习方法应用的，建议从这篇开始学习。

不过由于生物问题的复杂性，文章中用了243个可变剪接的外显子，1753个非可变剪接的外显子。
这个非平衡样本问题，即正样本（可变剪接）和负样本（非可变剪接）的差异很大。
解决这类问题的方法很多，例如：1.重抽样凑成平衡样本；2.加一些附加数据集；3.采用惩罚模型。

但是从这篇文章中我好像没有具体看到相应的对策。

文章中采用的是binary classification。一共228个特征，包括序列碱基信息，三联密码子信息，外显子长度等特征。

文中也做了False Positive Rate和Ture positive rate(ROC曲线)分析。并且比较了Naive-Bayes和neural net work方法。

特征选择的时候，使用Golub等人的方法，这种方法感觉就是找特征在正负样本中差异大的。

最后结果在10 fold cross validation后AUC可以达到0.93。

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|brute-force enumeration|暴力枚举|merit|价值|
|slack|松弛|convey|传递，表达|
|heuristic|启发式|pyrimidine|嘧啶|
|stretche|延伸|concatenation|一系列互相关联的事物|

### 2.Widespread establishment and regulatory impact of Alu exons in human genes

Yi Xing（邢毅）老师组里的工作，他们组专门研究转录调控，从文章里可以学到不少东西。
本文是介绍alu exon在基因中的调控作用，实验和分析相结合。有高剪接活动的Alu exons富集在5'-UTR区域。
文章里的东西可以说是对Alu exon同转录关系的一个较为全面的总结。

### 3.Automated classification of alternative splicing and transcriptional initiation and construction of visual database of classified patterns

这篇文章是讲述如何对可变剪接类型进行分类，并且还做了个可视化的数据库（网站）。

我关注这篇的内容就在它如何对可见剪接分类，方法挺有意思的，就是对外显子和内含子（基因间区）用二进制进行标注，然后找相似的pattern进行合并。
合并后，又进行了二进制到十进制的转换。已知的一些可变剪接pattern可以换算成这样的十进制数字，然后从基因组上的所有可变5’端和可变剪接换算成的结果中进行查找，
找到一样的，就说明这个可变剪接模式是已知的哪种。

文章的精华全在Figure1和Figure2。

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|atypical|非典型|miscellaneous|杂项|
|herein|此处|decimal|十进制|

### 3.ARH: predicting splice variants from genome-wide data with modified entropy

这是一篇算法文章，预测剪接变异，用的是Affymetrix exon array的数据。

文章中主要用一组公式计算了对转录本剪接的评价：1.在基因层面是区分有可变剪接的基因；2.在外显子层面计算了剪接的离差（偏差）。
在公式（2）中用了以2为底的指数$$p_{g,e}=\frac{2^{\mathopen|\zeta_{g,e}\mathclose|}}{\sum\nolimits_{e=1,...,m} 2^{\mathopen|\zeta_{g,e}\mathclose|}}$$来计算exon splicing probability，没想明白为什么要以2为底(成比例放大便于计算？)。
最后他们加上熵以及权重项搞了个ARH数值（权重*熵，凑一凑），如果这个数值>0.03暗示着剪接现象。

算法实现可以学习一下，一般自己弄个有指示意义的数值也差不多的玩法。

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|deviation|离差，偏差|constitute|构成|
|*per se*|本质上|||


### 4.Discovery and Analysis of Evolutionarily Conserved Intronic Splicing Regulatory Elements

这篇文中着重从基因组层面的信息来寻找同剪接调控相关的元件(内含子剪接调控元件)。文章中把剪接元件序列能研究的内容做的挺全面的，虽然我认为得到的结论也不是很强。

简要记录一下找寻intronic splicing regulatory elements（ISREs）的步骤：

1. 首先从基因组中抽出保守的外显子和外显子两侧的区域。去掉第一个外显子，外显子上下游的内含子区域分别为400bp，区域截取这么长是为了避免只找到microRNA和snoRNA序列。
2. 统计5mer-7mer的短序列。用chisq来计算相同长度的短序列之间的相关性。并排除再启动子上enrich的TFBS序列。<u>这里就有一个问题，TFBS不光在启动子上，所以只排除启动子上的是不严谨的。</u>
3. 聚类，聚类方法好复杂，是他们自己设计的。具体如下：
  - 将长序列同短序列进行比较，如果长序列包含短序列或者chisq相关性高，那么这样的长序列是短序列的“家长”
  - 将短序列同长序列进行比较，如果短序列是长序列的子集或者chisq相关性低，并且这个短序列不是一个“家长”，那么短序列是长序列的“孩子”
  - 合并这样的小“家庭”，条件是：“家长”序列有5个碱基相同，在合并的“家庭”中，家长是有最高chisq分值的序列。如果“孩子”有不止一位“家长”，那么chisq分值最高的是它直接关联“家长”。

这个聚类方式的好处是：1.保证聚类的集合（“家庭”）里的序列高度保守；2.粗劣都是根据实际序列的相似性来聚集的，这些实际序列都是生物学序列可以被实验验证。（这一点是要说明positional weight matirces PWMs不好，因为PWMs统计的序列可能在实际基因组中根本不存在）

文章中也有一句话没看明白。

> An important caveat in our analysis is that on occasion we had more than one cluster with motifs that might have been grouped as one cluster by other clustering methods. 

这句话是说<q>有些时候多余一个的motif簇会被用其他聚类方式聚成一类</q>，但是为什么这样？

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|caveat|警告|resemble|像|
|canonical|规范|cognate|同源|


### 5.MATLIGN: a motif clustering, comparison and matching tool

这是做motif聚类的一篇文章，由于上一篇是关于短序列的，所以这篇就少为跑个题，写一个看过的motif聚类相关的文章。

文章是作者写了个工具做motif聚类，这个工具的优势是对于position frequency matrices(PFM)和degenerate consensus sequences(简并一致序列)都可以做分析。
所用的方法无外乎是那些距离：Kendalls tau rank corre- lation coefficient (I), Spearman's rank correlation coeffi- cient (II), Pearson correlation coefficient (III), normalised Euclidean distance (IV) and evolutionary substitution score (V), 或者这些方法的结合。
有了距离后就用自下而上的聚类方法（Agglomerative hierarchical clustering）来聚类，之后根据silhouette value来优化子集合的数量。


### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|stochastically|随机|repetition|重复|
|heterodimer|异源二聚体|agglomerative|凝聚|
