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

