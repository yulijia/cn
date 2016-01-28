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

文章一开头就说本文不在于竭尽可能的罗列前人的工作，而是指出什么样的实验能产生科学有用的结论。

正片一共就两页，首先说明了从1999年的一个关于mRNA和蛋白质的研究开始，大家发现了转录组表达水平和蛋白质组的含量没有一个很好的定量关系可以解释。
也就是转录组数据不能预测蛋白质组的水平。但是，RNA在蛋白质翻译中肯定起到了作用，例如：microRNA可以调控蛋白质合成。
mRNA和蛋白质得降解速率也大不相同（前者几分钟，后者几个小时甚至几年），并且对于同一个基因来说，其RNA和蛋白质的合成/降解速率也没有联系。
所以我们不能期望发现mRNA和蛋白质之间简单的相关性。

第二部分就是说如何整合多组学数据，产生深入的新发现。

随着各种技术的不断发展，多种数据整合是非常重要的。蛋白质可以用来监视磷酸化过程，转录组可以用来说明基因上下调时被哪些转录调控因子所调控。
蛋白质可以决定哪些转录本在哪个时间点可以翻译成蛋白质。整个过程是非常复杂的相互调控。
有研究发现，结肠癌CNA的变化通过反式作用来影响多种蛋白质。这个工作建立起了突变（CNV）同表型的关系。

最后作者表达了我们需要的是真正的整合组学研究的观念模式，而不仅仅是相关性研究(see Box 1)。

Box 1. Outstanding questions

- What is data integration beyond correlation? 
- How do we educate new scientists to appreciate the diversity of -omics measurements?
- How to determine which -omic data type is best to investigate a hypothesis?
- When to generate multi-omic data?

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|nuanced|细微差别|disruptive|破坏性|
|interrogation|审讯|elucidate|阐明|
|succinctly|简洁的|pervasive|普遍|
|oscillation|[振荡](http://www.hwjyw.com/jxyd/cybx/200811/t20081104_23265.shtml)|[orthogonally](http://stats.stackexchange.com/questions/30592/what-is-the-meaning-of-orthogonal-in-validation-testing)|互不相关|
|utilitarian|功利|perspective|角度|
|phosphorylation|磷酸化|delineating|描述|
|cognate|同源|myriad|无数|
|paradigm|范式|mindeset|观念模式，思维倾向|

**Analytical platform evaluation for quantification of ERG in prostate cancer using protein and mRNA detection methods**

这篇文章是实验检测技术。用PRISM-SRM质谱（不需要抗体）方法来检测前列腺癌症中的ERG蛋白，这种蛋白由于基因融合导致变化，是一个癌基因（原癌）蛋白。

文章的摘要部分已经把内容讲得很清晰了：本文主旨就是找寻新的前列腺癌症检测靶标以及检测方法。在细胞、组织和直肠指诊尿液沉积物中做实验，
用ELISA, western blog, NanoString和qRT-PCR分别检测蛋白和RNA含量。
结果就是不管是检测ERG转录本产物还是蛋白质产物，在临床诊断和预后分析中都有价值。

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|prostate|前列腺|post-DRE|直肠指诊|
|sediment|沉积物|immunosorbent|免疫吸附|
|lysate|裂解液|prognostic assays|预后分析|
|androgen|雄激素|Ewing's sarcoma|尤文氏肉瘤|
|indolent|缓慢|impetus|动力|
|epitope|抗原决定部位|immunohistochemistry|免疫组织化学|
|serologic|血清学|assay|试验|
|hemocytometer|细胞计数器|ailquote|整除|
|titrate|滴定|stroma|基质|
|spurre|鞭策|biopsies|组织活检|
|Caucasian|高加索人，白种人|endothelial|内皮|
|devoid|缺乏|mimic，mimicking|模仿|
