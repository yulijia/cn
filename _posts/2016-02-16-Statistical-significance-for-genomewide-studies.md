---
published: ture
layout: post
title: "p value 与q value"
author: Yu
categories: [论文笔记]
tags:
- q value
- p value
---

最近要重读一批之前读过的文章，会大量更新笔记。

首先，我就又读了一遍Storey 和 Tibshirani 写的Statistical significance for genomewide studies。
纸质版被满篇标注了重点。在这里仅仅写一下两者的异同，推导请具体看文章附录。

文章是用q value度量FDR对p value 做校正。q value可以说是FDR的定量扩展。

### FDR与false positive rate的区别

false positive rate 是符合零模型的特征被认为显著的比率。

FDR是显著的特征属于零模型的比率。

例如：false positive rate = 5% 意思是平均5%的零模型特征在研究中会被判别成显著的。
FDR=5%意思是在所有显著的特征中，平均存在5%的特征是真正属于零模型的。

### familywise error rate

In statistics, familywise error rate (FWER) is the probability of making one or more false discoveries, 
or type I errors, among all the hypotheses when performing multiple hypotheses tests.

中文翻译成“总体错误推断率”比较好。

### p value 与 q value

The p value is an individual measure of the false positive rate while the q value is an individual measurement of the false discovery rate.

比较重要的一点是，p value 如果完全响应零假设（不拒绝），那么p value的分布应该服从均匀分布。解释可以参考:[http://stats.stackexchange.com/questions/10613/why-are-p-values-uniformly-distributed-under-the-null-hypothesis](http://stats.stackexchange.com/questions/10613/why-are-p-values-uniformly-distributed-under-the-null-hypothesis)

q value <= 0.05产生160个表达量具有显著差异的基因，这意味着有大约8个（160*0.05）被称作具有显著差异的基因是假阳的。

对于p value和q value的普遍错误解释是，它们代表假阳性的概率。
例如，一个基因有q value = 0.013，这并不是说它有0.013的概率为假阳的，
0.013是说<q>当我们认为这个基因是假设检验中的一个显著的结果时，而它是一个假阳性结果</q>，这个事件发生的**预计比率（期望比率）**为0.013。


### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|stricter|严格|surge|浪涌|
|underway|进行|in favor of|支持，有利于|
|hexamer|六聚体|dissection|解剖|
|haploid|单倍体|progeny|后代|
|legitimate|合法|obfuscate|混淆|
|intuitively|直观|intermediate|中间的|
|liberal|自由派，自由主义|rigorous|严格的|
|incurre|发生|concrete|实际，具体|
|exploiting|利用|conservative|保守|
|calibrate|较准|arbitrary|随意|
|implicit|隐含|||
