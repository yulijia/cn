---
published: ture
layout: post
title: "3C 4C 5C HiC ChIA-PET 以及 ChIP-loop"
author: Yu
categories: 生物信息
tags:
- 染色质构象捕获
- 3C
- 4C
- 5C
- HiC
- ChIA-PET
- ChIP-loop
---

整理一下这几种技术的原理。

### 3C
染色质构象捕获（3C）技术是用福尔马林瞬时固定细胞核染色质，用过量的限制性内切酶酶切消化染色质 - 蛋白质交联物，在 DNA 浓度极低而连接酶浓度极高的条件下用连接酶连接消化物，蛋白酶 K 消化交联物以释放出结合的蛋白质，用推测可能有互作的目的片段的引物进行普通PCR和定量PCR来确定是否存在相互作用。3C 技术假定物理上互作的 DNA 片段连接频率最高，以基因座特异性 PCR 来检测基因组中 DNA 片段之间的物理接触，最终以 PCR 产物的丰度来确定是否存在相互作用。**注意：用PCR意味着我们对于消化后留下的片段，知道其序列信息。**

### 4C
4C 技术称环状染色质构象捕获 （circular chromosome conformation capture） 或芯片染色质构象捕获（chromosome conformation capture-on-chip），特点就是对于酶切下来的片段进行环化，然后用反向PCR从已知区域开始扩增出环状的部分。然后用芯片进行序列分析。此时做PCR，我们不需要知道序列两端的信息，只需要知道一段的信息。

### 5C
若研究几百个染色质片段之间可能存在的相互作用，使用3C技术需要设计大量PCR引物来确定已知片段与假定片段的关系，通量较低，较难实现。因此，人们设计出3C碳拷贝（3C-carbon copy，5C）技术，这个技术是基于3C的基本原理，结合连接介导的扩增 （ligation-mediated amplification，LMA）来增加3C检测的通量。以3C酶切连接文库为模板 ，在3C引物端加上通用接头（例如T7、T3），例如在正向引物（bait）的5‘端加上T7接头，在反向引物的3忆端加上T3接头，若两个推测片段存在相互连接，由于连接酶介导的连接作用的性质，只有连接上的片段才有扩增。 这样，利用通用引物T7、T3进行PCR，而后将产物进行高通量测序即可实现高通量的3C实验。

### HiC
是在3C的基础上，在酶切后将缺口进行补平（dCTP 进行生物素标），然后用连接酶进行连接，将样本进行超声破碎，随后用生物素亲和层析将片段沉淀（也就是抓下来带有生物素标记的片段），加上接头进行深度测序。

### ChIP-loop
常见的有ChIP-3C和ChIP-4C，在过量的限制性内切酶将染色质 -蛋白质交连物酶切消化后，用所研究蛋白质因子特异性的抗体进行免疫沉淀，然后再进行酶切产物连接，后续步骤同3C、4C相同。**注意：使用特异性抗体沉淀下来的蛋白质有可能作用于目的 DNA 旁边的位点，而不是介导目的DNA 与其他 DNA 之间的相互作用。**

### ChIA-PET
ChIA-PET(chromatin immunoprecipitation using PET) 技术是3C、paired-end-tags (PET)和下一代测序技术的结合，既可检测细胞内染色质的相互作用又可解决实验所得DNA片段较小、数据量大等问题。它可以无偏的、在全基因组范围找出与目标蛋白因子作用的染色质片段。其部分实验流程与ChIP-loop实验相似，都是以福尔马林固定细胞，限制性酶切基因组，用目的蛋白特异性的抗体沉淀蛋白质-DNA 复合物，给酶切片段加上带有生物素标记的接头(此接头带有特殊的酶切位点，例如 *Mme* I)，然后进行二次连接反应，再使用带有接头的酶进行酶切(例如 *Mme* I)，所得产物再加上接头，进行深度测序。使用ChIA-PET可确定目标蛋白与DNA作用的位点，也可进一步确定目标蛋白可能调控的基因。带生物素标记可以较准确的定位蛋白质与DNA相互作用区域。

具体实验流程看这张图可以一目了然：

HiC （选自：[Comprehensive Mapping of Long-Range Interactions Reveals Folding Principles of the Human Genome](http://science.sciencemag.org/content/326/5950/289.full)）

![Imgur](http://i.imgur.com/zxLHE12.jpg)

3C，4C，5C （摘自：[wiki](https://en.wikipedia.org/wiki/Chromosome_conformation_capture)）

![Imgur](http://i.imgur.com/TIpfG0A.jpg)

几种方法的比较（选自：[A decade of 3C technologies: insights into nuclear organization](http://genesdev.cshlp.org/content/26/1/11.full)）

![Imgur](http://i.imgur.com/h2HJcdo.jpg)


### 参考资料

[1]: [染色质构象捕获及其衍生技术](www.pibb.ac.cn/pibben/ch/reader/create_pdf.aspx?file_no=20100158)
