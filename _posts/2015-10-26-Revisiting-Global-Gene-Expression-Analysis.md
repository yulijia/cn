---
published: ture
layout: post
title: "基因表达与spike-in"
author: Yu
categories: 论文笔记
tags:
- 基因表达量
- spike-in
- 肿瘤
---

Revisiting Global Gene Expression Analysis 这篇文章在刚发表的时候我们实验室就研读过，但是当时由于自己关注不够多，并且自己处理的数据进行了比例转换所以不涉及这个问题。
但是前一段时间又看了一遍这篇文章，我们都知道在single cell RNA表达分析中一般都要用spike-in来解决normalization的问题。
但是也有很多单细胞表达量的分析没有做这个分析。
由于同第一次看这篇文章已经有很久了，我早已忘记spike-in主要应用在肿瘤的研究中，所以现在觉得只要是肿瘤的研究都要做这个分析，才能准确确定表达量。
今天我开始有时间好好读一遍这篇文章，发现文章中提到的表达量normalization用到的两个样本high c-Myc和low c-Myc都是<u>同样的细胞数量</u>，所以对于bulk数据，这个方法好像没法用。
Encode已经把spike-in当作标准流程了，新上传的RNA表达量数据有些已经带有spike-in了，我需要在去检查一下究竟那些数据是单细胞（定量细胞的）还是bulk（组织）的。

现在简单复述一下这篇文章的内容。


