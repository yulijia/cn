---
published: true
layout: post
title: "小鼠胚胎单细胞RNA-seq线性、环状RNA分析"
author: Yu
categories: 论文笔记
tags:
- single cell
- circRNA
- embryos
- 转录组分析
---

Tang Fuchou 老师实验室做胚胎发育分析以及单细胞RNA-seq非常有经验，最近（7月23日）他们发表了一个新单细胞转录组测序方法———— single-cell universal poly(A)-independent RNA sequencing (SUPeR-seq)，主要特点是在cDNA合成时用有固定anchor序列的随机primer代替传统的oligo(dT) primer。

对于实验部分我理解的不多，主要看信息分析部分有什么关于线性、环状RNA的新结果。

在小鼠胚胎细胞不同发育阶段的研究中：

- 该研究中大多数circRNA含有多个外显子，少数（9%）circRNA只含有一个外显子。
- 只有0.9%的circRNA有多于20个潜在的miRNA绑定位点，在功能上绝大多数可能没有起到miRNA海绵的作用。
- circRNA在卵母细胞阶段就已经可以检测到，到受精卵四个-八个细胞阶段开始下降，<q>囊胚细胞阶段降得很低(为啥？)</q>。
- 出现circRNA多的基因的线性转录本表达量也高。
- circRNA两侧的intron要比不环化的RNA intron长。
- 一个基因可以产生多个circRNA，另外这些circRNA倾向于使用同一个5'端的exon，而3'端的exon差异大。
- 对于使用同一个5'端exon的circRNAs，在下游有长intron的circRNA的数量相对同个基因产生的其他circRNA来说显著的多。反之，使用同一个3'端的exon，上游有长intron的circRNA更富集。
- repeat元件在circRNA两侧的intron中不明显富集，但由于circRNA两侧的intron长度相对较长，所以repeat序列的总数要比其他的intron多。（从这点来看repeat序列其作用不在于排列的密度，在于绝对数量）
- 有互补序列的circRNA数量更加富集。
- 相对距离5kb左右的互补序列才有作用。
- 有强splicing motif时不容易形成circRNA。
- circRNA的上下游motif对circRNA的表达起到相反的作用，上游motif强，表达的circRNA多，下游motif弱，表达的circRNA多。


另外，我认为下面这句话看着不太地道。

Gene ontology(GO) analysis of all the 1316 host genes producing these circRNA transcripts showed strong enrichment for terms related to chromatin organization, 
cell division, and response to DNA damage stimulus, <u>suggesting potential roles of these circRNAs in these functional areas</u>. 

