---
published: ture
layout: post
title: "多组织间的DNA甲基化系统研究"
author: Yu
categories: 论文笔记
tags:
- DNA methylation
- ENCODE
---

前一段时间有幸聆听了杨晓飞做的关于DNA甲基化相关的报告，现在简要回顾一下他们这篇文章的内容。另外这个工作的参与者里还有Xiaojian Shao老师，不过他挂名的工作单位实在是太奇怪了`_-_`。另外这篇文章是收费的，所有Supplementary无法下载`-_-'`

### Systematic DNA methylation analysis of multiple cell lines reveals common and specific patterns within and across tissues of origin

这个工作主要是用定义并设计了一个方法找出DNA甲基化相关位置（local clusters of CpG sites），并在获得的DNA甲基化区段内进行多组织间的分析。

整个工作分为三个层次：

- 找寻DNA甲基化在各个组织间的common pattern
  * 在基因组上的富集情况
  * 功能
  * 同（基因）表达的相关性
- 细胞谱系特异性的pattern
  * 甲基化pattern
  * 在基因组上的富集情况
  * motif的富集情况
- 细胞系特异性的pattern
  * 甲基化pattern
  * 功能的富集
  * 同（基因）表达的相关性

#### 1.local clusters of CpG sites（LCCS）的找寻方法

本文采用的ENCODE项目reduced representation bisulfite sequencing (RRBS)的甲基化数据，一共用了54正常细胞系。

根据我自己对数据的理解，由于RRBS数据只是在一些位点测定了DNA的甲基化情况，而不是全基因组测定DNA甲基化情况，所以位点比较稀疏。

local clusters of CpG sites的就是把DNA甲基化位点密集的区域变成一个unit，对DNA甲基化位点进行聚类。具体的聚类方法如下（意思差不多，这个是我听讲座后自己总结的）：

1. 找到在整个基因组上距离最近的两个甲基化位点，将这两个点归为一个unit
2. 从这两个点的上下游找寻距离这个unit最近的一个甲基化位点，把这第三个甲基化位点放入unit里
3. 重复第二个步骤，直到这个unit的长度达到500bp(不超过500bp)，这样就选出了一个LCCS
4. 接下来再次进行第一到第三步骤，直至所有的甲基化位点都成为某个LCCS的一部分

最终在所有用于研究的细胞系中，他们找到了35276个LCCSs，LCCSs的长度中位数是79bp，每个LCCS上有7个CpG。对于大多数LCCSs（21417，60.7%）甲基化比例(percent methylated value，简称为PM)的方差小于5。

#### 2.加权LCCS共甲基化网络的分析展示出不同生物（过程）相关的共甲基化模块

*下面所有分析中没有对DNA甲基化数据做样本间的normalization，当时演讲人说ENCODE网站上有信息说这些数据可以相互比较。*

本文中将LCCSs进行聚类，发现了7个group(module 模块)，这7个模块中5个是高甲基化的，2个是低甲基化的。高甲基化的区域多在非编码，基因体，open sea[^1]，低甲基化的区域多为启动子， CpG islands（CGI）在open sea区域很少见。接下来，就是对高甲基化和低甲基化区域(各个模块)的分析（关于功能，以及同基因表达的相关性），没有什么有意思的发现，就不赘述了。

在什么地方用到了网络？ 为了度量不同细胞系之间的LCCS是否相似，文中采用加权LCCS共甲基化网络，找出细胞系之间相似的甲基化LCCS模块。

#### 3.细胞谱系特异性的pattern分析

首先对LCCSs根据细胞谱系进行聚类（血液、肝脏、肺、心脏等），发现细胞谱系特异性的DNA甲基化多富集在基因体 和非CpG岛区域。之后就找了在低甲基化的LCCSs区域内的motif，发现了一些同转录调控相关的蛋白motif。最后找到了同细胞谱系特异性的LCCSs相关的一些基因，这些基因根据资料也的确是细胞谱系特异性表达。

#### 4.细胞系特异性的pattern

本文中发现细胞特异性的LCCSs富集在不同的染色质状态（chromatin states），细胞系特异性的高甲基化LCCSs在weak transcriptional state富集，低甲基化的LCCSs富集在活跃的启动子和增强子区域。

### 分析软件

- WGCNA package
- HOMER

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|deplete|用尽，少有|intragenic|基因内|
|antagonism|对立，相克|||

### 附注

[^1]: [Alix Groom: How to measure DNA methylation](http://www.bristol.ac.uk/caite/geocode/newcastleshortcourse/howtomeasuredna.pdf)

![CpG islands/shores/shelves/open sea](http://i.imgur.com/TFVakGv.png)


