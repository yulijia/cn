---
published: ture
layout: post
date: 2017-07-04
title: 模型融合：Stacking model
author: Yu
category: 机器学习
tags:
- Stacking
- Voting
- Averaging
- Bagging
- Boosting
---
<!--xzcat TTP-001_S1_L003.raw.annovar.hg19_multianno.vcf.xz | vcftools  --vcf - --min-meanDP 10  --recode --stdout --recode-INFO-all > test.vcf -->
<!--
vcftools --gzvcf TTP-001_S1_L003.raw.vcf.gz --bed ../../in/SeqCapEZ_Exome_v3.0_Design_Annotation_files/SeqCap_EZ_Exome_v3_hg19_primary_targets.bed --out output_prefix --recode --keep-INFO-all
-->

模型融合的方法有5种：1. 投票，2. 求均值，3. bagging，4. Boosting，5. Stacking[^1]。

其中投票运用在分类问题上，求均值是最简单的回归问题的模型融合方法。

bagging就比较复杂了，有放回的抽样，对抽样的样本建立模型，然后对结果进行1.投票或者2.求均值。

Boosting是用迭代思想，我先建立一个简单的模型，然后找到这个模型的剩余误差，接下来在用另一个模型来预测前一个模型的剩余误差，以此类推，这样会产生多个若分类器（模型），然后给每个分类器一个权重，最终组合成一个强分类器（模型）。

![Gradient_Boosting](http://i.imgur.com/puZ8S3h.png)
上图来自于参考资料[^2]。

Boosting的权重究竟怎么选？
目的是让加权后的错误最小化（损失函数数值最小）。
损失函数有：
1. 无权重平均
2. 加权平均
3. logistic MSE
4. hinge
... 等等

例如决策树，计算weighted impurity scores，一个二分类问题：根据class1和class2中的比例，求信息熵[^2]。


好了，说了这么多废话，终于到重头戏，stacking方法了，这个方法网上的文献不多，混乱程度那是相当高。
stacking 方法的第一层是类似cross validation，对于训练集合分成10份，用其中的9份做training，1份做validation，另外在对test集合做预测，这样，最后会得到一个完整的训练数据的validation结果，以及测试数据的预测结果，然后将这两个结果分别作为第二层的训练数据和测试数据，进行预测[^3]。

![stacking method](http://i.imgur.com/akHjfc3.png "Stacking Models for Improved Predictions")
上图来自于参考资料[^3]。

**那么问题来了，究竟是对测试数据集在第一层时，做10次预测，并将10个结果求均值或者投票，还是每次只对测试数据集的十分之一做预测？**
我个人认为是后者，如果已经对10次预测结果求均值或者投票了，那么就等于已经做了一次第二层对模型融合。个人观点，不一定对，主要是我没有找到[^3]中的代码里对第一层的测试数据集合求均值或者投票。

另外在第二层做模型融合时，regression数据用glm，classification数据用boost，我测试过regression数据用boosting tree，结果糟糕的一塌糊涂（仍旧是个人观点，不一定对）。


后记另一件事情：我发现我在5年前就用`gbm`方法做预测，但是我完全不记得我自己做过这样的事情了<code>_-_</code>。如果觉得理解不了stacking model究竟是用了哪种方法在第一层做预测，直接用python或者R的软件包。在独立日写了一天的代码，最后才发现软件包的我并不感到高兴 <code>:(</code>。



参考资料：

[^1]: [【机器学习】模型融合方法概述](https://zhuanlan.zhihu.com/p/25836678)
[^2]: [信息增益(相对熵) pdf](https://courses.cs.washington.edu/courses/cse455/10au/notes/InfoGain.pdf)
[^3]: [Stacking Models for Improved Predictions](http://www.kdnuggets.com/2017/02/stacking-models-imropved-predictions.html)
