---
published: ture
layout: post
title: "关于蛋白质、RNA和癌症的三篇文章"
author: Yu
categories: [论文研读]
tags:
- 蛋白质
- RNA
---

读了三篇PNNL某实验室的文章，PNNL感觉都是做蛋白质。
由于是初次接触蛋白质，所以有很多地方都理解的不好，这篇博客主要记录一下问题。


**Comprehensive Quantitative Analysis of Ovarian and Breast Cancer Tumor Peptidomes**

这篇文章是定量分析肿瘤里的肽组学。由于对于肽链，小整体蛋白（多肽组学）经常被评估为不适合用于研究。

> The study of the low molecular weight collection of bioreactive peptides, protein degradation products, and small intact proteins (i.e., peptidomics) is often criticized as being less sensitive, less reproducible, and as vulnerable to a lack of controls in sample collection and preparation

文章中用定量多肽组学平台和自己开发的分析工具研究了人类卵巢癌和乳腺癌异种移植的肿瘤样本中多肽进行研究。

1. bottom-up [^1]

Bottom-up（自下而上）是一种传统的手段，它将蛋白质的大片段混合物消化/酶解成小片段的肽后再进行分析，是在蛋白质组学的研究中较为广泛使用的一种质谱技术。然而由于选择性剪接、各种蛋白质修饰（例如乙酰化和甲基化）以及内源性蛋白质裂解等复杂机制的存在，使得细胞内产生了复杂的蛋白异构体及种类。Bottom-up无法完整准确地鉴定这些蛋白的特征。

2. Top-down [^1]

Top-down（自上而下）技术虽可以直接对完整的蛋白——包括翻译后修饰蛋白以及其它一些大片段蛋白测序，然而由于不能将完整蛋白质片段分离技术与串联质谱技术相整合而无法开展大规模的蛋白质组研究。

文章的研究做法有点像研究RNA，多肽分析也做得是热图，PCA，火山图等。

同时文章中也发现了个体间多肽的差异，要大于不同组织之间多肽的差异（这个结论在DNA层面也适用，RNA我没仔细做过数据不敢妄下结论）。
也就是聚类的时候每个个体的不同组织部位的数据会聚集到一起，个体和个体相距较远。


### 参考资料

[^1]: http://www.cib.ac.cn/xwdt/kjqy/201111/t20111109_3392779.html


### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|aberrant|异常|degradation|降解|
|mass spectrometric|质谱仪|xenograft|异种移植|
|postexcision|切除后|protease|蛋白酶|
|conventional|传统的、惯例的|proteolysis|蛋白水解|
|proteasomal|蛋白酶体|malignant|恶性的|
|metallopeptidase|金属肽酶|collagen|胶原蛋白|
|chromatography-tandem|色谱串联|serum|血清|
|plasme|血浆|invertebrate|无脊椎的|
|endogenous|内源|explicit|明确的、清楚的|
|repertoire|全部节目|ischemia|失血|
|anesthesia|麻醉|midline|中线|
|vertical|垂直|incision|切口|
|omentum|胃系膜|resect|切除|
|dissect|解剖|strip|条|
|specimen|标本|cryovials|冷冻|
|nitrogen|氮气|basal|基底|
|luminal|管腔|subcutaneously|皮下|
|cryopulverization|低温粉碎|isotopic|同位素|
|extracted ion chromatogram|萃取离子色谱法|elution|洗脱|
|intensity|强度|kinetics|动力学|
|perturbation|摄动|cold ischemia|冷缺血|
|concentration|浓度|precursor|前体|
|propensity|倾向|chymotrypsin|一种肽链内切酶，糜蛋白酶，胰凝乳蛋白酶|
|cytosolic|细胞溶质|proteolytic|蛋白水解|


**The utility of protein and mRNA correlation**


