---
published: true
layout: post
title: "基因表达与spiked-in"
author: Yu
categories: 论文笔记
tags:
- 基因表达量
- spiked-in
- 肿瘤
---

**Revisiting Global Gene Expression Analysis**这篇文章在刚发表的时候我们实验室就研读过，但是当时由于自己关注不够多，并且自己处理的数据进行了比例转换所以不涉及这个问题。
但是前一段时间又看了一遍这篇文章，我们都知道在single cell RNA表达分析中一般都要用spiked-in来解决normalization的问题。
但是也有很多单细胞表达量的分析没有做这个分析。
由于同第一次看这篇文章已经有很久了，我早已忘记spiked-in主要应用在肿瘤的研究中，所以现在觉得只要是肿瘤的研究都要做这个分析，才能准确确定表达量。
今天我开始有时间好好读一遍这篇文章，发现文章中提到的表达量normalization用到的两个样本high c-Myc和low c-Myc都是<u>同样的细胞数量</u>，所以对于bulk数据，这个方法好像没法用。
Encode已经把spiked-in当作标准流程了，新上传的RNA表达量数据有些已经带有[spiked-in](https://www.encodeproject.org/experiments/ENCSR466KZY/)了，我需要在去检查一下究竟那些数据是单细胞（定量细胞的）还是bulk（组织）的<code>大致看了一下，好像tissue的就有</code>。

现在简单复述一下这篇文章的内容。


1. 首先以往研究中发现c-Myc高的细胞中很多基因的表达水平整体提高，整体的RNA水平要比c-Myc低的细胞高出2-3倍。
这个现象引出问题：以往的标准化方法没有考虑到整体表达水平的升高和抑制，这样会导致解读RNA表达量数据出现问题。

![Img](http://i.imgur.com/Laucfou.png)

2. 如上图所示，AB图中两个细胞的RNA水平一致，所以标准化后可以看到基因B和E表达量是明显升高的。
对于CD图中的两个细胞中的一个细胞表达了比另一个细胞多1到2倍的RNA，如果还用正常的标准化方法可以看到A、G、I这三个基因表达量上升。
而D、E、F这三个基因表达量下降。但实际情况呢，其实这些基因基本上表达量都升高了。
<q>这个标准化产生的问题是基于这样一个假设，即我们认为每个细胞的所有mRNA表达水平是一致的。</q>

3. 进一步说明我们常用的分析方法将这种表达量的差异看作技术误差，也就是理解为噪声，
并希望在研究中对于不同的样本或实验之间的<q>表达水平</q>要有同样的中位数，或均值，或在一个范围内的表达量分布要基本一致。

4. 为了得到可靠的基因表达量，文章中采用spiked-in 标准，加入表达量基本确定的RNA作为参照。
他们分别在Microarrays，RNA-seq以及Nanostring中做了实验，加入spiked-in RNA的表达谱变化更接近真实情况。
另外，做实验时严格统计了c-Myc高和c-Myc低的细胞数目[^1]在同等细胞数目的条件下进行的RNA表达情况的分析。

5. 当无法具体统计细胞数目时怎么办？
When cell counting may be problematic, as for expression experiments from solid tumors or tissues, DNA content may be used as a surrogate if ploidy and DNA replication profiles are also characterized to prevent the introduction of a DNA content-based artifact.

6. 以前的全基因组表达量数目中有多少我们已经解读错了？
How prevalent is misinterpretation of genome-wide expression data due to the assumption that cells produce similar levels of total RNA? 
The answer is likely related to the prevalence of regulatory mechanisms that globally amplify or suppress transcription.

最后对于RPKM的标准化可以用R包*affy*中的loess.normalize[^2]来实现。说白了就是做回归平滑的时后可以选取所有的样本点（老方法），或者只选取一部分样本点（spiked-in的RNA，新方法）。



备注：

[^1]: Cell number was determined by counting cells with C-hip disposable hemocytometers (Digital Bio) and equivalent numbers of high- and low-Myc cells were harvested.

[^2]: The names "lowess" and "loess" are derived from the term "locally weighted scatter plot smooth".
