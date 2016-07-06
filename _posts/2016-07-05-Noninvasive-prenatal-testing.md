---
published: ture
layout: post
title: "NIPT检测"
author: Yu
categories: 生物信息
tags:
- NIPT
---

NIPT（Noninvasive prenatal testing）非侵入式产前检测，国内一般称作“无创DNA产前检测技术”。之前一直没有时间看，这个技术究竟怎么从母亲的血液中测胎儿的DNA，现在有时间了，赶紧记录一下原理。

NIPT技术细分为两种：一种是测CNV，另一种是测SNP。
在2012年时比较流行的4中具体方式是[^1]：
1. Sequenom 公司：定量，短序列全基因组测序，并且评估胚胎DNA含量
2. Verinata 公司：定量，短序列全基因组深度测序，不评估胚胎的DNA含量
3. Ariosa 公司：定量，目标区域扩增，并且根据SNP频率来确定胚胎DNA含量
4. Natera 公司：基于非定量的SNP，分析等位基因频率（这个方法中用白细胞的测序结果作为母亲的基因型）


其中重点要说明的是，测CNV是不用区分母亲和胎儿的DNA的，首先，我们明确母亲没有任何一种三体综合征和染色体缺失，那么在这种条件下仍然检测出一定比例的三倍体或者单倍体，那么就说明是胚胎出现了问题。

从测序角度来说就是测序深度越高越精确，对于测序结果是否说明有染色体异常，用假设检验（Z-score）来估计其异常程度。

下图比较了四个公司的方法的准确性，可以看到对于21三体综合征是最准确的，对于18三体综合征和单倍体的检测准确性低。

![Imgur](http://i.imgur.com/017StNv.png)


测不准的原因在于测序技术有GC偏好性，并且在13和X染色体上表现得很明显[^2]。

NIPT方法目前主要还是用于测染色体倍增或者缺失（截至2013年），对于一些微缺失和微倍增（ microdeletions and microduplication ）用芯片的方法也开展了检测研究。

我个人的理解，孕妇首先应该做常规血检和B超检查，如果检查认为有问题，可以先做一个无创DNA产前检测来确认一下，如果无创也指示有问题或者数值处于临界值，那么继续做羊水穿刺来确定。

我本认为技术应该很高超，结果看完相关网络资料发现不用区分母婴的DNA时，方法也就很常规了。


[^1] [Noninvasive Prenatal Testing (NIPT): Separate But Not Equal](http://www.agt-info.org/Documents/2014%20Annual%20Meeting/HANDOUT%20Strom.pdf)
[^2] [Non-invasive prenatal aneuploidy testing: technologies and clinical implications. By: Brynn Levy and Errol Norwitz, June 20, 2013](http://www.mlo-online.com/non-invasive-prenatal-aneuploidy-testing-technologies-and-clinical-implications.php)
