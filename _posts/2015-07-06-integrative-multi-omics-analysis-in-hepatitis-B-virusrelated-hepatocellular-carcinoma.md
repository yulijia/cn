---
published: true
layout: post
title: "通过多组学研究方法寻找乙肝病毒引起的肝癌的生物学标志"
author: Yu
categories: 论文笔记
tags:
- hepatitis B virus
- hepatocellualr carcinoma
- multi-omics analysis
---

这篇文章比较偏，如果不是做肝癌研究的，会有很多不明白的地方，另外，对于组学数据的分析写得比较少。做的东西只是描述了一些表面现象，没有挖掘机理。

不是专门做肝癌及其组学数据分析，不建议看这篇文章。

文章的分析主要工作是由Zhao Yi老师组完成的。

## Identification of prognostic biomarkers in hepatitis B virus-related hepatocellular carcinoma and stratification by integrative multi-omics analysis

上面是文章中的题目，这个题目太长了，我在网页链接里缩写了一个简略的题目（同文章中的题目不完全一致）。

### Background

[肝癌如何分类？](http://www.liver.ca/chinese/liver-disease/types/liver-cancer.aspx "下面内容来自加拿大肝脏基金会")


>肝肿瘤分成多种，其中只有几种属癌肿性。最主要的分类法，是鉴定肿瘤属良性（害处相对较少）抑或恶性（可以由肝脏扩散至其他部位，故较为严重）。
>
>**良性肿瘤**
>
>血管瘤（Hemangioma）是最常见的良性肝肿瘤，是始于胎儿的肝脏异常血管生长。身体状况正常的人中，占10% 以上者肝脏有血管瘤。大部分有血管瘤的人均无任何征状，也不需治疗。但在较为罕见的情况下，血管瘤或会扩大并流血，如出现这情况便要进行手术割除。
>
>肝腺瘤（Hepatic adenomas） 是良性的肝细胞肿瘤，大部分情况均无征状也不需治疗。但如果体积大，或会导致痛楚或失血，在这种情况下肿瘤便需割除。肝腺瘤较常见于女性。部分个案显示，避孕药或怀孕或是触发成因。
>
>肝脏局部结节性增生（Focal nodular hyperplasia，简称FNH） 指数种细胞出现类似肿瘤的增长。虽然属良性，但结节性肿瘤与肝癌并不容易分辨。
>
>**恶性肿瘤**
>
>成人最常见的原发性肝癌（始于肝脏的癌症）是肝细胞癌（hepatocellular carcinoma，简称HCC），即肝细胞出现癌症。这类癌症有数种增长模式。有些在开始时是单一个肿瘤，然后渐渐增大。到较后期时，癌细胞便会蔓延至肝脏其他部位。
>
>肝癌亦可以在肝脏多个部位增长，并演变为多个肿瘤。这种情况在肝硬化病人身上最普遍。
>
>另一种肝癌是始于胆小管的胆管癌（cholangiocarcinoma）。胆小管是输送胆汁至胆囊的管道。
>
>然而，大部分的肝癌均非始于肝脏，而是由身体其他部位开始的癌症，扩散至肝脏。这类癌症是以癌症开始的部位（原发部位）命名，属于继发性肝癌或转移性癌症。譬如，始于肺部的癌症扩散至肝脏，便称为扩散至肝脏的转移性肺癌。继发性肝癌较原发性肝癌高出 30 倍。

### Data information

本文对两个病人的外周血，癌旁，第一位病人的原发灶，卫星灶，门静脉癌拴，第二位病人的左肝区和右肝区的进行了基因组和转录组的测序。第一位病人有肝硬化，年龄是四五十岁，第二位病人没有刚硬化，年龄是七十多岁。第一位病人的肝癌属于低分化，第二位病人的肝癌属于高分化，低分化的肝癌细胞恶性程度高。

### Question 1

在本文中研究的是原发性肝癌——肝细胞癌，这种癌症在国内，有很大一部分是由于乙肝、丙肝导致的。原发性肝癌，会有多个病灶，那么这些病灶是源于肿瘤细胞的某个单克隆，还是多克隆？

这个问题可以通过对乙肝病毒同宿主的DNA整合方面来进行研究。

1. 如果，对于一个病人，在不同的肝癌组织中，我们找到的乙肝病毒插入序列都在同一个位置，那么很有可能，这位病人的不同部位的肝癌细胞可能属于同一个单克隆。
2. 反之，乙肝病毒在不同肿瘤组织中，插入到了不同的位置，那么这些肝癌细胞肯定不属于同一个单克隆，也就是说这个病人的肝癌细胞起源具有多克隆性。

根据对乙肝病毒基因整合的研究，文中的第一位病人属于情况1，第二位病人属于情况2。我觉得这只是一种可能性，没准第一个病人，乙肝病毒虽然在不同位点的癌组织中整合在基因组的同一个位置，但是这些癌组织也有可能是在不同或相同时间分别产生的。<u>只研究乙肝病毒的整合情况，能否完善的说明单克隆和多克隆的问题？</u>

### Question 2

文章分别看了两位病人的SNV, CNV, structural variation的情况，并做了系统生发树。

本文中认为，第一位病人的肝癌演化路线是`normal` -> `primary cancer` -> `portal vein tumor` -> `satellite intrahepatic metastases`，第二个病人的肝癌两个病灶更有可能是同时出现的。

但是，我没有理解这个图，从图中看，第二位病人的肝癌演化路线，更像是`normal` -> `left part cancer` -> `right part cancer`。

### Question 3

对于转录组的分析，要结合基因组，在基因组上有大量CNV的区域的基因，其表达量同copy number数量正相关。

在转录组部分的研究中，没有什么实质的内容，对于高表达和低表达的基因，做了功能富集图，用的软件是Cytoscape plugin Enrichment Map。<u>我没有理解图里面的小点（基因集合）里的基因有哪些。</u>

### Question 4

最后，根据基因表达量的差异和KEGG/BioCarta通路分析，文章中找到了21个基因，这些基因属于细胞周期，p53信号，组氨酸代谢等通路中。
之后又在174个病例中进行了验证，其中6个基因存在普遍的（癌症/正常）差异性，之后他们对这些基因和病人的临床数据整合(乙肝表面抗原，谷丙转氨酶，肿瘤分级等)，进行了分析。
文章中发现*TTK*基因的高表达和低表达，同病人的无复发存活率、总存活率相关性高，<q>**TTK基因高表达的病人在肝癌手术后还需要尽早介入治疗**</q>。 

## 分析软件

- Circos
- Cytoscape (plugin Enrichment Map)
- SPSS

还有转录组常用分析软件，具体需要看supplementary。

## 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|prognostic|预后|hepatocellular carcinoma|肝细胞癌|
|stratification|分层|differentiation|分化|
|multifocal|多灶性|intrahepatic|肝内|
|metastasis|转移|lesion|病灶|
|specimen|标本|integration|整合|
|elucidate|阐述|clinicopathological|临床病理|
|mitotic|有丝分裂|synchronously|同步|
|hepatectomy|肝切除|recurrence-free survival(RFS)|无复发生存率|
|overall survival|总生存率|cirrhosis|肝硬化|
|resection|切除|peripheral blood|外周血|
|monoclonal|单克隆|telomerase|端粒酶|
|substitution|突变|translocation|易位|
|aneuploidy|非整倍体|putative|假设|
|portal|门|vein|静脉|
|tumor thrombus|癌拴|inflammatory|炎症|
|coagulation|凝结(血)|coenzyme|辅酶|
|oxidative|氧化|histidine|组氨酸|
|mediate|介导|spindle|放垂体|
|HBsAg|乙肝表面抗原|ALT|谷丙转氨酶|
|albumin|白蛋白|postsurgical|术后|
|biopsy|活检|nodule|结节|
|catastrophic|灾难性的|albeit|尽管|
|epithelial|上皮|prostate|前列腺|
|pancreatic|胰腺|interventional|介入|
|surveillance|监控|hepatectomy|肝切除|
|intriguingly|有趣的是|prospective|预期前瞻性|
|expedite|促进|||
