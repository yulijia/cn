---
published: true
layout: post
title: "人类胚胎以及胚胎干细胞的单细胞RNA测序数据分析"
author: Yu
categories: 论文笔记
tags:
- Single Cell
- RNA seq
- embryos
- hESC
---

### Single cell RNA seq profiling of human preimplantation embryos and embryonic stem cells

*Nature Structural & Molecular Biology 20, 1131–1139 (2013) doi:10.1038/nsmb.2660*

*Received 18 July 2013 Accepted 05 August 2013 Published online 11 August 2013*

[http://www.nature.com/nsmb/journal/v20/n9/full/nsmb.2660.html](http://www.nature.com/nsmb/journal/v20/n9/full/nsmb.2660.html)

本文一共对胚胎以及胚胎干细胞系阶段的124个单细胞进行测序。分析了RNA表达情况，是关于单细胞RNA方面的一篇早期研究文章。

### 主要研究结论

#### 1.不同细胞类型间的转录情况分析

本文研究的细胞类型包括卵母细胞，受精卵，2细胞卵裂球，4细胞卵裂球，8细胞卵裂球，桑椹胚，晚期囊胚，hESC细胞，传代10代后的hESC细胞。所有细胞经过了严格的形态学筛选。以往研究中已经确认在4细胞和8细胞阶段基因的表达情况会有极大的改变，该阶段是[Maternal to zygotic transition (MZT)](https://en.wikipedia.org/wiki/Maternal_to_zygotic_transition) 期。
本文在单细胞中测得属于RefSeq基因列表里的11006个基因(占所有RefSeq基因的49%)以及RefSeq转录本列表中18002个转录本（占总体的48%）。对于受精卵胚胎细胞的表达水平（RPKM>0.1）进行了聚类分析以及主成份分析，分析发现8细胞阶段和桑椹胚阶段的的表达水平有些类似。在人类中MZT阶段主要是在8细胞时期，文中找到了2495个显著上调的基因（zygotic gene activation）,上调基因的功能多富集在RNA新陈代谢，RNA剪接，核糖核蛋白复合物的生成，核糖体的产生中。

#### 2.可变剪接的动态模式

文中分析的基因里有4822个基因至少产生了2个转录本。根据转录本特异性的外显子连接区域（junction）序列的唯一比对(uniquely mapping)，有20%（总数4822）的基因产生了2个以上的转录本，最高达到7个转录本。在所研究的7个发育阶段中（卵母细胞，受精卵，2细胞卵裂球，4细胞卵裂球，8细胞卵裂球，桑椹胚，晚期囊胚）只有206个基因在每个阶段都有多转录本的表达，其他的基因的多转录本只在特定的几个阶段中能检测到。另外，至少66%的情况下，基因所表达的主要异构体（major isoform）别其他的异构体表达量高2倍。另外文中以forkhead box(FOX) transcriptional factor, *FOXP1*为例子，说明了一个ESC阶段特异性转录本异构体有一个外显子（exon 18b），这个异构体编码出的蛋白质与维持细胞多功能性相关，在体外胚胎干细胞中检测到的exon 18b是exon 18a的25倍。<u>但是这幅图上（见下方），还展示了一个非特异性表达的外显子exon 19，图中可以看到这个外显子在PE(原始内胚层)时期没有表达量数据，这个究竟是为什么，文中没有给出解释。</u>

![fig3D](https://i.imgur.com/fEuROLV.png)

#### 3.长非编码RNA(lncRNA)的表达情况

如果把所有的数据（124个细胞？）整合在一起分析，lncRNA的转录本拷贝数量均值是蛋白编码基因的十分之一（10%），同前人的数据结果较为一致。但是，如果对于每个单细胞进行分析，lncRNA的拷贝数量均值可以达到蛋白编码基因的40.5%。<u>文章中只有在这里用到了拷贝数量(copy number)这个词组，我不知道这个是指普通意义上的DNA上的gene copy number还是表达量水平。</u>

#### 4.未知的蛋白编码转录本以及lncRNA

为了找寻未知的新转录本，文中，首先排除了在已知基因上下游10kb范围内找到的未知转录本，并认为这些潜在的未知转录本可能是已知基因的一部分。接下来，对在排除后的区域内找到的新转录本进行了分析，从转录本长度，保守性方面说明文中所找到的新转录本同已知的转录本很相似，并且也看到了一些转录本在7个发育阶段的表达水平有很大的差异，说明这些新找出的转录本参与到了胚胎的发育调控中。

#### 5.hESCs和外胚层细胞的异同点（tracing pluripotency during the derivation of hESCs）

hESCs是从囊胚内团细胞（inner cell mass）的外胚层中分化来的，但是关于hESCs同外胚层细胞的异同点的全面分析却很少。本文分析了晚期囊胚阶段的30个细胞（分别属于桑椹胚滋养外胚层(mural TE)，极滋养外胚层细胞(polar TE)，外胚层以及原始内胚层），对已知RefSeq基因的表达情况进行聚类分析（在聚类中用到了bootstrap）。并对一些marker基因在外胚层、滋养外胚层、原始内胚层中的相对表达情况做了分析。之后又对hESCs细胞以及EPI细胞中的上下调的多功能性marker基因进行了分析，分析结果既有一致性，又有区别。说明hESCs细胞与EPI细胞的基因表达有区别。这种区别不仅体现在已知的基因中，对于文章找到的新转录本和lncRNA也存在着类似的区别。最后他们还分析了hESCs同小鼠胚胎干细胞之间的关系（mEpiSCs），分析发现hESCs同mEpiSCs比较类似，mEpiSC特异性的marker基因在hESCs中高表达，但是mESC特异性的marker基因表达量不高。

### 分析软件

- clValid package (`SOTA function`)
- Coding Potential Calculator (求保守性水平 $$\omega$$ metric)
- pvclust package
- Cufflinks
- Trinity (*de novo* transcriptome reconstruction)
- PASA (eukaryotic genome annotation tool)
- Cluster (gene expression pattern)
- JavaTreeview (gene expression pattern)

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|preimplantation|胚胎植入前|maternal|母系|
|epiblast(EPI)|外胚层|*in vitro*|体外|
|blastomere|卵裂球|oocyte|卵母细胞|
|maternal-zygotic transition|母系-合子过渡期|segregation|分离|
|trophectoderm|滋养外胚层|fibroblast|成纤维细胞|
|triplet|三联体|orthologous|直系同源|
|bovine|牛|blastocyst|胚囊|
|facilitated|便利|pluripotency|多能性|
|derivation|起源，衍生|metaphase|中期|
|zygote|受精卵|morula|桑椹胚|
|Late blastocyst|晚期囊胚|lineage|谱系|
|morphological|形态学|stringent|严格的|
|criteria|标准|germ|生殖|
|gamete|配子|phosphorylation|磷酸化|
|metabolism|新陈代谢|ribonucleoprotein|核糖核蛋白|
|biogenesis|合成|ribosome|核糖体|
|primitive endoderm|原始内胚层|maintenance|维持|
|inherite|遗传|drastically|彻底|
|hatch|孵化|subtly|巧妙地|
|precursor|先导|cytokine|细胞因子|
|cryopreservation|冷冻保存|pave|铺|
|dissect|解剖|reproductive|生殖|
|lysate|裂解液|deoxynucleotidyl transferase|脱氧核苷酸转移酶|
|culture|培养|immunostain|免疫染色|
|karyotype|核型|teratoma|畸胎瘤|
|heteroscedasticity|异方差性|passage|传代|



