---
published: ture
layout: post
title: "关于基因组结构变异和基因型的综述"
author: Yu
categories: 论文笔记
tags:
- 结构变异
---

Genome structural variation discovery and genotyping，这篇2011年的综述介绍了结构变异的检测方法和其他相关内容，对于初次进入这个领域的人是一篇不错的指导资料。

<q>一般情况下如果在正文中没有提到文章题目，请看日至的连接，连接只要不太长，就是英文题目。</q>

首先来看一下基因结构变异都有哪些情况。一般情况下，定义结构变异在1kb以上的区域的插入、缺失或者倒位。

1. Deletion
2. Novel sequence insertion
3. Mobile-element insertion
4. Tandem duplication
5. Interspersed duplication
6. Inversion
7. Translocation 


![Imgur](http://i.imgur.com/sCvaAOT.png)


对于大的变异（主要是获得或者缺失几百kb的片段）在人群中是十分少见的（<1%）但是会影响很大一部分疾病。
对于多拷贝基因家族，主要是基因拷贝数量的变异，主要对于疾病的作用是在敏感性方面（即，有些拷贝变异使得个体更容易得某些疾病）。

### 基于杂交的芯片方法

#### array CGH (array comparative genomic hybridization)

这个方法好像直接用两个样本的数据进行比较，取ratio。
存在的问题是，当只有一个样本时，在reference样本上的一个缺失，会被错判成测试样本上的一个增加。所以用array CGH的关键是要有一个可靠的reference。
这种方法多用于检测大于100kb的CNV。基本无法定位breakpoint。

罗氏提供的此类芯片（2011年）每个oligonucleotide长约1M，一共2.1M个。
检测一个CNV要3到10个probe。

#### SNP array

SNP芯片可以测CNV，应该是[这么一回事](http://www.biomart.cn/specials/cnv2014/article/84169 "Affymetrix SNP 6.0芯片介绍")。文章中也是这个意思。
SNP芯片的缺点是信噪比低(low signal-to-noise ratio)。也就是噪声大。

#### 芯片的整体缺陷

探针都是定义好的，没法发现新的SV，breakpoint上也不一定有探针。

上述两个平台的芯片在检测拷贝数变多方面上比检测拷贝数减少要困难，敏感性降低。
所以很容易就看到检测出的小区域SV变化绝大多数都是缺失。

非特异性的芯片对于10kb一下的SV检测敏感性都会降低（除了那些特别设计的芯片）。

当然，芯片最重要的缺陷是在检测含有重复序列区域的时候。
array CGH和SNP平台的假设都是在参考基因组上都是二倍体，但是在重复区域这一假设并不有效。但是CNV同片段重复有强相关性，很多breakpoint也出现在重复区域。

### single-molecule analysis （这章节没看懂）

理解SV的结构和位置必须需要从单分子层面的可视化手段。
fluorescent *in situ* hybridization(FISH) 和光谱核型（spectral karyotyping）分析是我们窥视普通和稀有基因组结构变异的方法。
但是这些方法的缺点也很明显，低产出，低分辨率，只能找到500kb~5Mb的结构变异。
有一个源于酵母基因组的相关技术现在可以用于人类基因组的SV检测（好像是光纤方面的）[^1] [^2] 。此技术是基于对传统限制性图谱的改良，对固定的DNA做限制性消化。这个技术可以用来检测倒位，转座，拷贝数变异以及这些结构变异的位置。
但是，还是对检测新的结构变异有限制，因为它的技术中需要用到参考基因组。（<u>这段关于实验的内容没有看得太明白</u>）

另外文章还说，条形码技术是一项非常有用的技术，在未来可以支持高通量的检测结构变异。这些方法包括在纳米级别的通道扫描荧光标记的DNA分子等（these methods include scanning fluorescently nick-labelled DNA molecules in nano-channel flow cells or nanoslits and the use of SNP-specific labelling of stretched DNA for haplotype resolution）。

### 基于测序的计算技术

#### Read-pair technologies

这个方法就是对于pair-end 的一对短序列进行中间空缺长度以及短序列方向的检测，找出同参考基因组相比有映射空缺(span)或者方向问题的序列。
序列如果映射到很远的两个地方，说明是一个deletion。序列如果映射到极端近的地方，没准就是一个insertion。
如果方向不一致没准是倒位，或者一系列的串联重复。
如果序列只有一端可以映射到参考基因组，而另一端不能映射到参考基因组，很有可能是新的insetion(Read pairs in which only one end clusters and the others do not map to the reference have been used to flag variant sequences not included in the reference genome (novel insertions).)。
采用这种方法的软件有: `PEMer`, `VariationHunter`, `BreakDancer`, `MoDIL`, `MoGUL`, `HYDRA`, `Corona` 和 `SPANNER`。

#### Read-depth methods

这个方法基于`序列映射的深度是泊松分布或改良的泊松分布`的假设，然后探测这些序列的深度不符合分布的情况，深度超高的地方可能有重复区域，深度低的地方可能是deletion。
这个方法最先用于癌症基因组的重排列现象（rearrangements）。如果用此类方法来找寻小范围的deletion和duplication（breakpoint级别的），需要的方法是`event-wise-testing (EWT) algorithm`
以及`CNVnator`软件。

#### Split-read approaches

分割短序列的方法可以用来检测deletion和小的insertion，分辨率可以达到“碱基”级别。这种方法首次应用在较长的sanger测序的序列上。
这种方法意在用分割短序列的方法找寻breakpoint。，这条序列无法直接比对到基因组上，序列中间有gap可能是deletion，比对到基因组上中间总是多出一块有可能是insertion。
`Pindel algorithm`用在paired-end的reads上大大减少了此类方法的搜索空间，提高效率。

#### Sequence assembly

理论上，所有形式的结构变异可以归结为拷贝，内容，结构的差异。我们可以通过从头（*de novo*）组装来识别这些变异。
也就是将短序列拼接成一个长序列contig然后再同参考序列进行比较。
基于短枪法(shortgun)从头比对拼接相关的软件有`EULER-USR`，`ABySS`，`SOAPdenovo`和`ALLPATHS-LG`。除此之外，`Cortex`可以用来做*de novo*的拼接，也可以设置成不同程度的根据参考序列来拼接。
另外，它还可以在不用参考序列的情况下进行组装和找寻SV。`NovelSeq framework` 合并*de novo*和局部组装的方法来定位新的序列insertion。`TIGRA`用来找寻SV中的breakpoint。

**这些方法的局限在于**

只能找寻一部分SV，并且由于算法的不同，找到的结果差异较大。
Read-pair technologies 方法对于重复区域的处理有问题，另外对于breakpoint的搜寻要取决于fragment的大小和分布，对建库有较高的要求，且价格不便宜。
90%的检测到的区域小于1kb并且大多数都是deletion，insertion很少能检测到。
Read-depth methods 方法没法赵精确的breakpoint。
Split-read approaches 分割短序列只在unique的区域可靠(split read is currently reliable only in the unique regions of the genome)。
Sequence assembly 方法在重复区域有偏，在这些区域找不准。

`SPANNER`，`CNVer`和`Genome STRip`三个方法，联合read-pair和read-depth方法，来找CNV，增加了可靠性。

人类基因组中有很多重复序列和片段重复，这些区域需要有更好的算法来检测SV。另外短序列深度（reads depth）也是很重要的指标，例如人类1000基因计划的数据，reads depth只有2到6fold。
敏感性和精确性同reads depth相关。

`MoGUL`算法结合多个个体的数据来找共同的CNV，解决了局部reads深度的问题，但是也降低了对于低频CNV的敏感性。

`VariationHunter` 采用相似的策略，并且对于稀有结构变化较为敏感。


上面讲到的不同检测方法参见下图。

![Imgur](http://i.imgur.com/DnIetuN.png)


### Genotyping（基因分形）

不同于测序技术，这个技术就是用PCR之类的方法检测已知的结构变异。对于检测的窗口大小可以设计的较为自由。
方法包括：`PCR-based techniques`，`SNP array-based techniques`，`Array CGH-based techniques`，`sequencing-based approaches`。
在sequencing-based approaches中又简单介绍了几个软件的内容，详情请看论文，这里就不介绍了。


### future direction

加强检测精确性，要结合计算方法和实验方法。
建立“金标准”来评价不同的SV结果。

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|elusive|难以捉摸的|widen|放宽，拓宽|
|tandem|串联|intersperse|穿插，点缀|
|inversion|倒位|susceptibility|敏感性，易受损害的状态|
|Hybridization|杂交|workhorse|驮马，主力，重负荷机器|
|refine|提炼|overwhelmingly|无法抵抗，压倒性的，绝大多数|
|ascertainment|探查|valid|有效|
|pathogenic|致病性|optical|光纤|
|capillary|毛细血管|capillary sequencing|毛细管测序|
|delineate|划定|fosmid|F黏粒|
|segmental|阶段性|stretch|拉神|
|span|跨度|infancy|婴儿期|
|discordant|不和谐的|prohibitively|禁止|
|devise|设计|versatile|多才多艺|
|owing to|由于|facilitate|方便，帮助，促进|
|collapse|塌陷|ameliorate|改善|
|impuitation|归罪|discrepancy|差异，矛盾，不符合之处|
|veil|面纱|lift|揭开|



### Reference

[^1]: Schwartz, D. C. et al. Ordered restriction maps of Saccharomyces cerevisiae chromosomes constructed by optical mapping. Science 262, 110–114 (1993).

[^2]: Teague, B. et al. High-resolution human genome structure by single-molecule analysis. Proc. Natl Acad. Sci. USA 107, 10848–10853 (2010). Application of the optical mapping technology to characterize human genome structure.

