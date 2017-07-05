---
published: true
layout: post
title: "ContrastRank：一种用于评估推定的癌症驱动基因和肿瘤样品分类的新方法"
author: Yu
categories: 论文笔记
tags:
- 驱动基因
---

找驱动基因是癌症研究领域的永恒话题。这篇文章是三个月前看的了，笔记耽误了<del>三个月</del>（已经变成）一年，有些当时的想法可能已经不记得了。标题中“推定的癌症驱动基因”就是假定的癌症驱动基因。
本文主要介绍一下这篇文章中推定驱动基因的`ContrastRank`方法，以及我看的另一篇文章 **Identifying cancer driver genes in tumor genome sequencing studies** 中的方法。

## ContrastRank

在`ContrastRank`方法中作者认为在基因组上出现的罕见突变对于癌症的发生发展起到了重要的作用。所以找驱动基因，就是要估计基因上出现的罕见的非同义突变。然后定义罕见的致病变异（PDV）为`allele frequency < 0.5%`的突变，存在至少一个PDV的基因叫做假定的受损基因（PIGs）。对于每一个样本中的基因，他们还计算了假定缺陷率（PDR）。最后根据假定的受损基因（PIGs）的概率的log10数值作为分值，来断定驱动基因。

### 数据样本

选自TCGA的三种腺癌，每种腺癌至少有200个配对的样本（正常组织/肿瘤组织）。分别是结肠腺癌，肺癌和前列腺癌。

## Identifying cancer driver genes

作者首先介绍了之前人们推定驱动基因时忽略的几个问题：
1. 非silent mutation的种类包括很多（missense, nonsense, deletions(indels), mutation in splice sites），对于蛋白质的影响也不同，mutation的选择压力也因为mutation的种类和其所在基因组位置不同而不同。
2. 不同的样本有着不同的背景突变频率。如果一个基因的突变只存在于有大量突变的样本中，那么这些突变很可能是属于特异性样本有大量突变的结果，而不是癌症的原因。
3. 不同的三联密码子产生非同义突变的概率不同。

接下来作者定义了driver-like non-silent mutation在某个样本中发现的事件是伯努利随机变量$$Y_{ij}$$。接下来又定义一个样本中出现的non-silent突变的最大值$$T_{ij}$$以及经验分布函数$$F_{ij}=P(T_{ij}<x|Y_{ij}=1,M_{0})$$，然后通过$$logP(Y_{ij}=y_{ij}, T_{ij}>t_{ij}, j=1,...,J|M_0)$$ 得到检验所需的统计量$$Z_i$$（我不清楚logP这个是怎么回事）。
在求背景分布时，作者假设transitions（转换）和transversion（颠换）突变的频率不相同，并且根据mutation出现在CpG区域和非CpG岛区域进行了mutation类型的划分。通过从背景分布中算统计量的p-value的方法，来推定驱动基因。

### 数据样本

肺腺癌数据：Ding,L. et al. (2008) Somatic mutations affect key pathways in lung adenocarcinoma. Nature, 455, 1069–1075.

## 小结

这两种方法， Identifying cancer driver genes的结果更符合我对驱动基因的定义。首先驱动基因不一定是有罕见突变的基因，可能很多样本中都有这样的突变。 另外该方法在结直肠腺癌的样本中，没找出APC这个关键的基因，我个人觉得效果不好。
