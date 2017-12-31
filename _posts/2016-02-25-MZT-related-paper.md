---
published: true
layout: post
title: "母本到合子转换（MZT）发育相关的文章"
author: Yu
categories: [论文笔记]
tags:
- MZT
- 组蛋白
- H3K4me3
- H3K27me3
- H3K36me3
- mRNA
- 转录组
- 斑马鱼
- MBT
- 降解
- cis-regulatory
- miRNA
- H3K9me3
- ZGA
---

感觉这样写下去，博客就变成论文记录了。为了避免这种情况，以后**论文笔记**都以归纳总结多篇文章为主，如果是非常好的文章，会单开一篇写一写。

### 1.Chromatin signature of embryonic pluripotency is established during genome activation

这是一篇讲述斑马鱼MZT阶段组蛋白和RNA聚合脢II在基因组结合位置的文章。

文中说明RNA聚合脢II同组蛋白（H3K4me3，H3K27me3，H3K36me3）结合到相关的基因组位置是发生在合子基因组激活时期。
很多不活跃的基因到活跃的时，有组蛋白H3K4me3的Mark。序列特异性的转录因子会先指导组蛋白H3K4的甲基化，然后招募RNA聚合脢II。
最后总结三个方面：1.合子基因组激活同组蛋白H3的三甲基化有关，说明组蛋白修饰提供了MZT期的调控信息；
2.在ES cells中也存在bivalent domains;3.有些单价且有H3K4me3修饰的基因没有被激活。


### 2.Transcriptome Analysis of Zebrafish Embryogenesis Using Microarrays

这篇文章分析了斑马鱼的胚胎时期转录本数据(Microarrays)，包含的时间点有：母本时期，囊胚期，原肠胚期，分裂期，pharyngula （咽喉胚期）。

做了各种层次聚类，每个聚类里有特点的基因都介绍了。该文章的亮点是找到了在pre-MBT时期表达的一些基因（整体表达水平低，所以不好发现），这些基因可能对后面MBT时期转录本调控起到作用。


### 3.A complex ‘mRNA degradation code’ controls gene expression during animal development

在这篇综述中，作者详细介绍了mRNA降解在生物发育中控制基因表达。
首先说降解会控制基因表达动力学：如果降解太快，那么基因表达水平会很低，会影响转录进程；如果降解太慢，基因表达水平就会很高（机体会想这个细胞是不是不想玩了），细胞就会进入机体删除阶段。
mRNA降解受控于RBPs（RNA结合蛋白），small RNAs，miRNA-RBP，cis-regulatory（顺式作用元件）。
RNA降解在动物发育中的作用有两点：1.控制发育过程；2.细胞特异性。

### 4.Prepatterning of Developmental Gene Expression by Modified Histones before Zygotic Genome Activation

这篇文章发在Developmental Cell上，很有意思，试验设计合理。

主要是讲斑马鱼发育阶段Zygotic Genome Activation（ZGA）时期的组蛋白信号对于转录的影响。
共检测了H3K4me3, H3K9me3, H3K27me3, H3K36me3, RNA PolII的marker在不同时期基因组上的分布情况。
研究发现H3K4me3富集在1000个pre-MBT时期的基因上，至少9000个MBT和post-MBT时期的基因上。
在这个部分，研究的母系表达的基因，也就是这些基因在pre-MBT期基本不表达，而在MBT期开始表达上调。

研究结果揭示了在不同时期这些组蛋白甲基化富集在基因组上的情况各有特点。尤其是在256个细胞阶段检测到的H3K4me3, H3K9me3和H3K27me3说明在这个时期转录抑制已经存在。

之后又发现H3K4me3 marker在256个细胞时期，存在于一些转录不活跃的基因区域上。
本来想说明这些基因不活跃，还找出了H3K36me3和RNA PolII的marker做对照，结果发现H3K36me3的确没什么信号，
但是RNA PolII存在于基因的启动子区域（不在gene body，也是转录不活跃的表现）。

我个人觉得最有意思的就是下面的这张图。作者们做了一个**epigenetic fate map of the pre-MBT H3K4me3-marked gene**,
从这个图可以看到不同的基因在不同的阶段又不同的表观遗传学marker。

![Imgur](http://i.imgur.com/Iv2t3bO.png)

后续，文章有讲述了Pre-MBT时期H3K4me3 mark对合子转录的积极作用，以及在精子和卵细胞中有这个maker的交集的基因有哪些。

### 5.Transcript clearance during the maternal-to-zygotic transition

这篇review有意思的地方是在后面的引用文献中作者点评了一些他们感兴趣的文章，这也方便了读者的阅读。

综述的主要内容是讲mRNA在MTZ过程中的降解以及它的机制。RNA结合蛋白，小RNA家族均有参与，后面还说了降解的mRNA有哪些作用。

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|bearing|方位|immunoprecipitation|免疫|
|bivalent|二价|poise|平衡|
|synchronous|同时存在|be posied for|准备好|
|heterologous transcription|异源转录|pertinent|关于...的，有关的|
|permanently|永久的|discrepancy|矛盾，不符合之处|
|inducible|可诱导的|basal|基底|
|segmentation|分割|organogenesis|器官发育|
|demarcate|定界限|amenability|服从|
|mutagenesis|突变形成|morpholino|吗啉基|
|mencement|开端|coordinate|协调，同时|
|putative|推定|chorion|绒毛膜|
|rhamnose|鼠李糖|lectin|凝集素|
|synchronous|同步|primordial|初生的，原始的|
|somitogenesis|体节发育|sea urchin|海胆|
|proteolytic|蛋白水解|conjugate|结合|
|pigment|色素|depletion|消耗|
|nascent|初期|milieu|周围|
|distorte|扭曲的|exoribonuclease|核糖核酸外切酶|
|nascent|初期|transient|短暂的|
|poeron|操纵子|chaperone|监督人|
|stoichiometry|化学计量|dictate|控制|
|bearing|风姿|convergent|趋同|
|chimeras|嵌合体|gamete|配子|
|per se|本质|onward|向前|
|entail|牵涉|homeostatic|自我平衡|
|guiescence|静止|stricto sensu|狭义上来说，严格意义上|
