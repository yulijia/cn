---
published: true
layout: post
title: "通过RNA纯化进行染色质分离"
author: Yu
categories: 生物信息
tags:
- 测序技术
- ChIRP
- RNA转录
---

Illumina公司有一张特别牛x的poster，叫做 [For all you seq](https://www.illumina.com/content/dam/illumina-marketing/documents/applications/ngs-library-prep/ForAllYouSeqMethods.pdf "大文件，慎点，我的16G内存小破笔记本在一次全文搜索中死机了")，全面记录了目前问世的所有二代测序技术的建库protocol，但是这张poster是加密的，无法分割、提取进行打印。然后，他们又出了一个手册，来介绍For all you seq里的建库方法，叫做Sequencing Methods Review，全手册加上illumina的广告将近200页。我打算从头到尾都看一遍，有兴趣的就写出来分享一下。

> 对于做生物信息的人，为啥要知道实验上的建库原理？

**因为测序数据的第一道处理步骤就是排除并分析建库和测序时产生的错误和误差。为什么会产生这些问题？如何在mapping时排除相应问题，做到准确alignment？**


第一部分就从RNA转录开始说起，RNA转录的度量方法分为很多种：

- post-translational modifications 后转录修饰
- RNA splicing 剪接
- RNA bound to RNA binding proteins (RBP) 与RNA相关蛋白结合
- RNA expressed at various stages 在不同阶段的表达量
- unique RNA isoforms 转录本异构体
- RNA degradation 降解
- regulation of other RNA species 调控其他RNA “物种” （我不清楚这句话的意思）


### Chromatin isolation by RNA purification

Chromatin isolation by RNA purification (ChIRP-Seq) RNA纯化染色质分离技术是用于定位非编码RNA，例如长非编码RNA及其蛋白同染色质相互作用的位置。

![ChIRP-Seq](https://i.imgur.com/4vm5lpS.png )

首先进行交联，超声打断，用Biotinylated寡核苷酸对感兴趣的RNA进行杂交，并用链霉抗生物素蛋白磁珠捕获复合物。用RNase H（核糖核酸酶H）处理后，对DNA进行提取和测序。

技术优点：

1. 可在基因组全部区域找寻结合位点
2. 可发现新结合位点
3. 可只对感兴趣的RNA进行相应研究

技术缺点：

1. 非特异性的寡核苷酸相互作用会导致对结合位点的错误解读
2. 染色质会在预处理阶段降解
3. 感兴趣的RNA序列信息必须已知 （这不是废话吗，感兴趣的RNA肯定是已知的，已知的能不知道序列？感兴趣的未知RNA的作用位点，知道了也没法研究啊）


