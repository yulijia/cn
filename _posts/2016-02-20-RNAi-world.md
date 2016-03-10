---
published: ture
layout: post
title: "RNA干扰（RNAi）的世界"
author: Yu
categories: [论文笔记]
tags:
- RNAi
- 诺贝尔演讲
---

重新阅读了RNAi的两位诺贝尔获奖者的演讲稿，应该算不上是论文研读，但也没别的类别可写，就放在这个目录下吧。

**1. return to the RNAi world: rethinking gene expression and evolution**

这是CC Mello的演讲稿，介绍了发现RNAi机制中的标志性事件。Mello有个女儿，是一型糖尿病患者。

> In the year 2000 our daughter Victoria was born. In an unfortunate twist of fate, Victoria developed type-one diabetes in the fall of 2001. Suddenly, I had to learn how to inject into a human, my own daughter, for the first time. Ironically, human insulin, the same bacterially synthesized molecule that inspired me to pursue molecular biology, is now giving Victoria her very life. This experience has given me a new perspective on the importance of medical research. Edit, who is a wonderful nurse, is now taking care of Victoria, and serving as a diabetes counselor for newly diagnosed families.
>
> [Craig C. Mello - Biographical](http://www.nobelprize.org/nobel_prizes/medicine/laureates/2006/mello-bio.html)

演讲的前面提到研究*Caenorhabditis elegans* ( *C.elegans* ) 这种全身透明的线虫给科学试验带来了极大的好处。
在1800-1900年代，德国进化生物学家[奥古斯特·魏斯曼](https://en.wikipedia.org/wiki/August_Weismann) 曾提出种质学说：

> (1) there is a special particle, the biophore, for each trait; (2) that these particles can grow and multiply independent of cell division; (3) that both the nucleus and cytoplasm consist of these biophores; (4) that a given biophore may be represented by many replicas in a single nucleus, including the germ cell; and (5) that during cell division the daughter cells may receive different kinds and numbers of biophores through unequal cell division.

根据我们目前的知识，这个学说的观点（2）和（5）是不正确的，这个学说也是当时的一个假说。但是如果把这段话中的"biophores"替换成"siRNA"，考虑这个理论在一些traits中的情况，我们可以得到一下观点：

> (1) there is a particle, containing <q>siRNAs</q>, for some traits; (2) these <q>siRNAs</q> can grow and multiply independent of cell division; (3) both the nucleus and the cytoplasm can contain the <q>siRNAs</q>; (4) a given <q>siRNA</q> may be represented by many replicas; and (5) that during cell division the daughter cells may receive different kinds and numbers of <q>siRNAs</q> through unequal cell division. 

Mello说这就是当时我们对siRNA所了解的东西，现在看来奥古斯特·魏斯曼的观点在某些生物学现象中是成立的。我想到了[于老师最崇拜的拉马克主义](http://www.cas.cn/xw/zjsd/201401/t20140106_4010664.shtml), 拉马克学说在表观遗传学中很多地方都成立。

接下来，他又具体介绍了一步一步发现RNAi作用机制的过程。


1.长双链RNA是在rde-1的帮助下作用于Small RNA的

![img](http://i.imgur.com/iXQePCq.png)

RNAi和microRNA通路中利用不同的RDE-1蛋白家族的成员，聚集到Dicer上。正当Mello他们认为RDE-1在上游起作用时，其他研究组（Greg Hannon, Ji-Joon Song以及Leemor Joshua-Tor）发现Argonaute蛋白有一个同其他可以剪切RNA的蛋白类似的domain(结构域)。

> These studies demonstrated that Argonaute proteins repre- sent the long sought ‘slicer’ activity (or the cop) that lies at the heart of the RNA-induced silencing pathway.

2.*rde-1*的功能

![img](http://imgur.com/XaCspEY.png)

当然，Mello 他们也没闲着，继续研究RDE-1的功能。RDE-1家族的同源蛋白可能在通路的下游起到关键作用。同时他们认为在通路下游的Argonaute似乎没有完整的能起作用的RNA切割相关的核酶酸domain。

3.沉默pathway

![img](http://imgur.com/tXFoPRX.png)

Mello的研究发现Argonaute也同一些内源的沉默通路相关，包括转座子和转基因沉默通路。

4.染色质-RNA反馈通路

![img](http://imgur.com/LYeVEo1.png)

最有Mello在演讲中介绍了RNA同染色质的相互作用。

>In the active conformation the regulatory region of the gene, called the promoter, is free of nucleosomes and is shown bound by the RNA-polymerase complex, (the complex that produces messenger RNAs and the subject of this year’s Chemistry prize). <q>In the ‘silent’ region a different kind of polymerase activity is recruited. Instead of producing mRNA, this hypothetical polymerase produces transcripts that enter an RNAi-like silencing pathway. </q>


### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|aptly|恰当的|tremendous|非常的，了不起的|
|spectacular|壮观|contemplate|思量|
|inflation|膨胀|stunning|令人惊叹|
|speculating|猜测|nematode|线虫|
|lariat|套索|snare|圈套|
|inflate|使充气，使膨胀|hyphae|菌丝|
|interwine|缠绕在一起|staircage|楼梯|
|segregation|种间隔离|postulate|假设|
|wrap|包裹|polymenzation|聚合物|
|elaborate|精心，详细制定|exemplify|例证|
|glowing|发光|exclusively|仅仅，只，独占|
|provocative|挑衅|metazoan|后生动物|
|descendant|后人|sophistication|诡辩|
|flawed|缺陷|defective|有缺陷的|
|gloss|注释|ingestion|摄入|
|apparatus|仪器|tackle|抓住|
|lethality|杀伤力|viable|可行的|
|vexing|令人烦恼的|endogenous|内源性|
|*Neurospora*|链孢霉|fission yeast|裂殖酵母|
|digress|离题|deficient|匮乏|
|identical|相同的|precursor|先导|
|envisioned|设想|intact|完整无缺|
|polycomb|多梳|virtue of|凭借|
|surveillance|监控|nascent|初期|


**2.Gene Silencing by Double-Stranded RNA(Nobel Lecture)**

Fire的演讲围绕着线虫的生物学试验来写的。比Mello的更侧重于某些人做了些什么。很严谨，把能列出的合作者都列在了slides上。
我觉得比Mello的有意思。尤其是他在演讲中提到了一些science/life-lesson说的很逗：

> The science/life-lesson that one can draw from this is <q>if you can do the experiment the way that seems most likely to be effective, do it just that way</q>

> A subsequent observation from Sam Driver and Craig Mello, yields the lesson <q>if you can?t do the experiment the way that seems most likely to be effective, still do it</q>

> The lesson here, if you?re a postdoc or perhaps a graduate student, is to do experiments that your advisor would never condone or suggest.

在最后Fire也提到了RNAi在非植物界中的生理过程中扮演的角色究竟是什么还不清楚。如何在更多的动物（高等动物，人）中运用这种技术来治疗疾病也要有很漫长的路要走。

时至今日，我再回顾这个2006年的技术时不得不感叹生物领域的技术淘汰的真快，十年后，现在最火的是基因编辑（CRISPR/Cas9），RNAi终究还是停留在实验室里的工具。

CRISPR/Cas9 今后将会如何呢？拭目以待。

补充一个：[如何看待RNAi疗法？](https://www.zhihu.com/question/31136565)

> 著作权归作者所有。
> 商业转载请联系作者获得授权，非商业转载请注明出处。
> 作者：化十
> 链接：https://www.zhihu.com/question/31136565/answer/56390149
> 来源：知乎
>
>RNAi和ASO领域目前最好的公司是位于Boston的Alnylam，以及位于Carlsbad的ISIS；目前alnylam最接近FDA批准的药物是利用LNP递送siRNA治疗TTR Amyloidosis (FAP) (临床三期，目前业界对他的结果相当乐观，可能就在年内批准）； ISIS有自己的核心ASO技术，有一个药物于2013年被批准，治疗hypercholesteromia，还有很多在2/3期临床。两个公司的pipeline里都有多个药物在未来3-5年有批准的可能。但是目前RNAi或ASO的大问题是只能做liver delivery，其他组织都不太成功。RNAi治疗癌症我觉得potency是一个问题，毕竟只是transient knockdown。RNAi刚出来的时候受到的追捧并不比今天的CRISPER/Cas9少，大家都觉得太牛逼；然而在发展的过程中出现了很多挫败，包括big pharma 的撤退等，因此目前该领域都是相对的小公司在develop。幸运的是过去2-3年里有明显的复苏迹象。我们如果再从历史记录看，这种过山车式的pattern也可以从之前的virus gene therapy的发展过程中看到。从这点来讲，我始终对CRISPER/Cas9保持一个谨慎乐观的态度：说到脱靶效应，CRISPER/CAS9面临的问题更多，临床转化的问题比RNAi更复杂。我个人判断RNAi在未来十年将有多个成药的例子（bottom line），但是能有多成功（upper limit），不太好说。



比较搞笑的是我看得这个版本的paper已经在杂志网站下架了，因为侵权，Fire并没有授权Cell Death and Differentiation 这个期刊来刊载他的演讲。这个期刊的文章中压缩了Fire的slides内容（少了几页）。
我已经不知道当时是谁（任课老师or同学）给我发的文献了，这篇绝版文献也找不到了，最后发张照片纪念一下。

![Imgur](http://i.imgur.com/5U0z0Zp.jpg)


单词表过长，我在看这篇文献的时候头脑空白，所有一看不能想起意思的词都标注了出来。

### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|disclaimer|免责声明书|rod|杆|
|intriguingly|有取的事|virulent|剧毒的|
|nasty|严重的|preliminary|初步的|
|pathogen|病原体，病菌|infection|传染|
|inject|注射|interferon|干扰素|
|innate|天生的|fortuitous|偶然发生的|
|bellwether|领导者|albeit|虽然|
|disseminate|散布，传播|accolade|嘉奖|
|vehement|热烈|frustration|挫折|
|pierce|刺入|cuticle|外皮|
|manipulate|操作|enticing|诱人的，迷人的|
|aberrant|异常的|disruption|中断|
|explicit|明确的|construct|结构|
|propensity|偏爱|dampened|抑制，控制，减弱|
|accentuate|强调|tapestry|织锦，挂毯|
|concerted nature|协调一致性|antisense occlusion|反义阻断|
|contaminant|污染物|fortuitous|偶然|
|cognate|同源|sludge|泥浆|
|concocted|调制|far-fetched|牵强的|
|ingredient|组成部分，要素，因素|twitching|颤搐|
|agarose gel|琼脂糖凝胶|deliberately|故意的|
|smear|涂抹，模糊不清|potent|有效的|
|tenable|守得住，合理的|artistry|技艺|
|sundry|各式各样|homeostasis|动态平衡|
|*in situ*|原位|accentuating|强调|
|condone|容忍|deliberate|故意的，权衡，熟虑|
|soaking|浸泡|facilitate|促进|
|Trypanosome|锥虫|parasite|寄生虫|
|conspicuously|显著的|intensively|集中地|
|cadre|干部，骨架|sake|缘故|
|menace|威胁，恐吓|subvert|颠覆|
|attenuate|变细，减弱|apparatus|装置|
|circumvent|围绕|grasp|控制力|
|intricate|错综复杂|elucidating|阐明|
|plethora|过多，过剩|abrogate|废除|
|pristine|纯朴的|reassuring|使安心|
|hindsight|后见之明|recapitulating|总结，摘要|
|catchy|迷人的，易记的|incorporate|组成，包含，吸收|
|intrinsic|固有的，内在的|termini|目的地，界标|
|repertoire|指令表|presume|假定|
|diligently|勤奋的|deviation|背离|
|self-inflicted|自己造成的|phosphate|磷酸盐|
|surveillance|监控|remedy|疗法|
|hitch-hiking|免费搭乘他人之车|permeate|弥漫|
|choreograph|设计舞蹈动作|hone|磨光|
|conceivable|可想到的|aggregate|合计，总数|
|thermodynamic|热力学|eliminate|排除|
|viable|能养活的，可生产的|portfolio|投资组合|
|negotiating|谈判，交涉|thicket|错综复杂|
|trepidation|害怕|endeavor|尝试努力|
|dysregulation|失调|consortium|财团，组织|
|substantial|大量的|inadvertent|无心的|
|omission|省略|||
