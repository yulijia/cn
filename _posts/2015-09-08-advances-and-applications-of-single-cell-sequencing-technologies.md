---
published: true
layout: post
title: "单细胞测序技术的优点和应用"
author: Yu
categories: 论文笔记
tags:
- 单细胞
---

Adevances and Applications of Single-Cell Sequencing Technologies 这篇review很值得一读，它总结了现有的单细胞领域技术、研究内容、现有问题以及今后方向。
下面简单总结一下比较感兴趣的内容。

### 单细胞DNA测序技术的缺陷包括: 测序覆盖度不均匀、allelic dropout（等位片段测序丢失）、假阳性、假阴性等。

multiple-displacement-amplification(MDA)方法由于测序覆盖不均匀，在CNV研究中不值得采用这种方法。

multiple annealilng- and looping-based amplification cycles(MALBAC) 方法假阳性高，但是研究CNV比较好。

NUC-SEQ/single nucleus exome sequencing(SNES) 方法可减少技术误差。

![img](http://i.imgur.com/HwFzceg.png)

### 单细胞RNA测序技术

WAT会造成3'mRNA 的偏差。

### 区分技术误差与生物学多样性(Biological Variation)

为了解释一个突变或者转录物的确在样本里时杂合的，<u>需要对这些结果做必要的实验验证</u>。 在DNA层面用深度测序，digital droplet PCR（微滴式数字PCR）。
在RNA层面，可用单细胞RT-qPCR以及微滴式数字PCR。

### Tissue Mosaicism的研究结果争议性很大（可以参考上一篇文章）

总结下来就是每个研究中都可以看到copy number mosaicism现象，但是这些现象的作用时正向还是负向目前还尚未有定论。

### 癌症方面的研究

研究主要集中在瘤内异质性、单/多克隆演化、CTC细胞携带mutation特点(肿瘤细胞转移问题)。

研究CTC细胞是为了追溯肿瘤和转移灶的mutation情况。

###小结

单细胞研究的问题涵盖：

1. 解读群体差异性
2. 追踪细胞系
3. 细胞类型分类
4. 罕见细胞的基因组学信息刻画

###展望

1. 从单细胞入手，研究单细胞其实是研究单细胞所在的组织的情况。
2. 如何连接并研究单细胞的phenotype到genotype。
3. 如何研究单细胞的多层面数据（例如，某个单细胞的DNA和RNA，某个单细胞的RNA和表观）
4. 在技术上，如何能同时测序上千个单细胞，并降低费用。


