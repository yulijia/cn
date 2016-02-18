---
published: ture
layout: post
title: "用单细胞基因组测序来检测人脑中体细胞拷贝数变异"
author: Yu
categories: [论文笔记]
tags:
- 单细胞
- 拷贝数变异
---

Single-Cell, Genome-wide Sequencing Identifies Clonal Somatic Copy-Number Variation in the Human Brain
这篇文章是讲单细胞CNV比较早的一篇。我都忘记为什么要看它了。

主要内容用半侧巨脑畸形和正常人的脑细胞，以及淋巴母细胞等细胞来做单细胞全基因组分析，看看扩增方法的噪声对CNV的影响。

单细胞扩增用的是MDA方法。还有一种单细胞处理方法是基于PCR的GenomePlex。

现有研究表明再神经细胞基因组中体细胞非整倍体比较罕见，但是体细胞CNV并不罕见。
文章中说明clonal somatic CNV在正常脑细胞和半侧巨脑畸形中都存在。
这个clonal somatic CNV的意思我不太明白，按文章的意思应该是一个细胞群体中都有的somatic CNV。

文章中有意思的一个地方是用microarray里的median absolute pairwise difference(MAPD)方法来比较拷贝数的噪声大小。
计算连续两个邻居bin上的log2 CN的绝对差异，并对所有bin取中位数，用这个数字代表噪声大小的分值。
计算结果说明MDA方法的噪声要比GenomePlex方法的大。

在后续研究中，他们只用MAPD<0.45的样本。单细胞采样会对测序结果产生较大影响，对单细胞低覆盖度的CNV分析可以用来评估样本质量。

样本之间的比较没什么有趣的东西，就不再赘述。

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|neuropsychiatric|神经精神|pathological|病理|
|euploid|整倍体|hemimegalencephaly（HMG）|半侧巨脑畸形|
|dysfunction|机能障碍|lymphoblast|淋巴母细胞|
|manifestation|表明，表示|prenatal|胎儿|
|malformation|畸形|defect|缺陷|
|epilepsy|癫痫|aneuploidy|非整倍体|
|tetrasomy|四体型，四倍体|magnitude|重要|
|compensate|补偿|fetus|胎儿|
|postmortem|死后|integrity|正直|
|intersample|采样|discrete|分离|
|integral|完整的|equivocal|模棱两可，意义不明|
|freeze-thaw|冷冻-融化|dicentric|双着丝粒|
|distal|末梢的|unperturbed|未扰动|
|query|质疑|bona fide|真实的|
|autism|孤独症|neuropsychiatric|神经精神疾病|
|nonetheless|但是，虽然如此|suspect|猜疑|
|intractable|难对付的|assay|测定|
