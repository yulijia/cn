---
published: false
layout: post
title: "ContrastRank：一种用于评估推定的癌症驱动基因和肿瘤样品分类的新方法"
author: Yu
categories: 论文笔记
tags:
- 驱动基因
---

找驱动基因是癌症研究领域的永恒话题。这篇文章是三个月前看的了，笔记耽误了三个月，有些当时的想法可能已经不记得了。标题中“推定的癌症驱动基因”就是假定的癌症驱动基因。
本文主要介绍一下这篇文章中推定驱动基因的`ContrastRank`方法，以及我看的另一篇文章**Identifying cancer driver genes in tumor genome sequencing studies**中的方法。对比一下这两种方法。

## ContrastRank

在`ContrastRank`方法中作者认为在基因组上出现的罕见突变对于癌症的发生发展起到了重要的作用。所以找驱动基因，就是要估计基因上出现的罕见的非同义突变。然后定义罕见的致病变异（PDV）为`allele frequency < 0.5%`的突变，存在至少一个PDV的基因叫做假定的受损基因（PIGs）。对于每一个样本中的基因，他们还计算了假定缺陷率（PDR）。

### 数据样本
选自TCGA的三种腺癌，每种腺癌至少有200个配对的样本（正常组织/肿瘤组织）。分别是结肠腺癌，肺癌和前列腺癌。

## Identifying cancer driver genes
