---
published: ture
layout: post
title: "对于芯片数据中fold change方法和t统计量方法得比较"
author: Yu
categories: 论文笔记
tags: [fold-change,t-statistic, modified t-statistic]
---

A comparison of fold-change and the t-statistic for microarray data analysis，这文章是大神Robert Tibshirani和Daniela M. Witten（是Robert的一个学生，现在华盛顿大学生统专业做PI）写的。整篇文章<q>每句话都非常重要！</q>

对于芯片数据中control和treatment样本间信号强度的比较，筛选差异大的基因，会用到fold-change或者t-statisitic。
文章作者比较了这两种情况的计算出的差异基因之间的差别。
说明在没有背景噪声的情况下用fc比较好，在有背景噪声的情况下用modified t-statisitic比较好。
作者还指出<q>可重复性</q>同<q>精确性</q>之间也不是完全一致。
传统的t检验在可重复性和精确性上都不如fold-change和改良的t检验，所以在芯片数据分析时，不要用传统的t检验。

### Introduction

这部分，文章重点介绍了他们的实验方法，用真实的microarry数据和模拟的数据来做分析，采用的筛选基因的方法包括传统t检验，改良的t检验，两种fold-change方法。
模拟后结果说明用究竟是用fold-change或者改良的t检验取决于我们的研究是对<u>基因表达量的绝对变化</u>感兴趣还是对<u>基因表达量相对于其噪声的变化</u>感兴趣。

> Therefore, a researcher’s decision to use fold-change or a modified t-statistic should be based on <code>biological</code>, rather than statistical, considerations. 

### Statistical measures of differential expression

**方法1. 传统t检验的统计量**

$$T_i=\frac{\bar{x_i}-\bar{y_i}}{s_i}$$ 

其中$$s_i$$是对于基因i的组内样本重复间的标准差。

**方法2. 改良的t统计量**

$$T^{"}_{i}= \frac{\bar{x_i}-\bar{y_i}}{s_i+s_0}$$

其中$$s_0$$是为了让$$T^{"}_{i}$$的变异系数最小的一个常量，在本文中用的是Significance Analysis of Microarrays (Tusher et al. 2001)中的计算方法。
我在wiki[^1]上查了一下，上面说$$s_0$$是根据$$\alpha$$分位数来定的。另外有些文章[^2]中直接将$$s_0$$定义成$$s_i$$的中位数。

**方法3. 标准fold-change**

$$FC_i=\frac{\bar{x}^{'}_{i\cdot}}{\bar{y}^{'}_{i\cdot}}$$

其中$$\bar{x^{'}_{ij}}$$和$$\bar{y^{'}_{ij}}$$是基因i在组内样本j的原始表达量（control除以treatment）。

**方法4. 另一种fold-change算法**

$$FC_i=\bar{x}^{'}_{i\cdot}-\bar{y}^{'}_{i\cdot}$$

其中我们标记方法3的fold-change为$$FC_{ratio}$$，方法4中的为$$FC_{difference}$$。

另外，我们可以看出在增加$$s_0$$的大小后，方法2的排序结果会逼近方法4的排序结果。
$$$s_0$$这个常数越大，t统计量的分母越一致，那么对基因排序起到关键作用的就是分子，分子又通方法4的一样.....所以方法2和方法4的结果会比较一致。

为了证明高度可重复的统计量并不是十分准确的，他们在文中构建了一个人工统计量：

$$P_i=(\bar{x_{i\cdot}})^3-(\bar{y_{i\cdot}})^3$$

P代表power，文中说不建议在实际中使用这个人工统计量。

### Overview of the genes selected using the different measures

文中分别用模拟的数据，按上面的4个方法来计算差异基因。

从下图中可以看出，按普通的t统计量挑选的基因的标准差都很小，
fold-change方法找到的基因在control和treatment里有很大的差异，
改良后的t统计量找到的基因有较小的标准差和组间较大的差异。
由于普通的t统计量和fold-change的结果完全不一样，对于研究者来说，要考虑某个基因在研究中是否重要的根据是<u>表达量的偏移</u>还是<u>标准差的偏移</u>。

![Imgur](http://i.imgur.com/h9vgnOe.png)

### Simulated and real data Concordance

这节主要介绍了他们用的两种模拟策略：一种是基于正态分布的偏移，另一种是基于样本分组间均值和方差的偏移。

关于一致(Concordance)的定义：在一个基因（挑选后的）集合中的基因也在另一个基因集合中的比例。

### Analysis of the accuracy of the different measures

下图就是他们分析的一个结果，可以看到样本量在红线左侧时，用$$FC_{difference}$$比较好，样本量很大时就用改良的t统计量较好。

![Imgur](http://i.imgur.com/kYRA3JS.png)

其实从我们用的方法来寻找差异基因，一共就度量两类差异：
第一类是$$\mid \mu_{control} - \mu_{treatment} \mid $$ ，另一类是$$\mid \frac{\mu_{control} - \mu_{treatment}}{\sigma}\mid$$。
后者主要是标准化基因间的噪声（方差），因为基因均值之间的差异可能是源于基因间表达量的方差有差异。


接下来，他们又考虑了一个比较极端的例子。

|       | Control             | Treatment           | FCdifference | FCratio | T     |
|-------|---------------------|---------------------|--------------|---------|-------|
| Gene1 | 150, 200, 250       | 1, 50, 100          | 3.51         | 3.97    | 1.69  |
| Gene2 | 101.1, 101.2, 101.3 | 100.1, 100.2, 100.3 | 0.014        | 1.01    | 12.25 |

这个例子中Gene1表达量在两组间差异很大，Gene2表达量在两组间差异很小。但是如果用t统计量来衡量的话，Gene2远大于Gene1。

我自己计算的结果通论文上的不太一眼，Gene1的t统计量是3.6844，而不是1.69。

```
t.test(c(101.1,101.2,101.3),c(100.1,100.2,100.3))

  Welch Two Sample t-test

  data:  c(101.1, 101.2, 101.3) and c(100.1, 100.2, 100.3)
  t = 12.247, df = 4, p-value = 0.0002552
  alternative hypothesis: true difference in means is not equal to 0
  95 percent confidence interval:
  0.7733042 1.2266958
  sample estimates:
  mean of x mean of y 
  101.2     100.2 

t.test(c(150,200,250),c(1,50,100))

  Welch Two Sample t-test

  data:  c(150, 200, 250) and c(1, 50, 100)
  t = 3.6844, df = 3.9996, p-value = 0.02113
  alternative hypothesis: true difference in means is not equal to 0
  95 percent confidence interval:
  36.87866 262.45467
  sample estimates:
  mean of x mean of y 
  200.00000  50.33333 

```

那么在生物学家的眼中，究竟哪个基因是需要关注的基因呢？我觉得应该是Gene1吧。

> From this perspective, the question of whether the fold-changes or a modified t-statistic results in more accurate gene orderings is **really a biological one**, 
rather than a statistical one, as it depends on what types of expression differences between control and treatment have biological relevance.

### Analysis of the reproducibility of the different measures

接下来他们又检测了各种方法的可重复性。 从下面的两张图中可以看出前面自己定义的P统计量有很好的重复性（下面第一个图），但是没有很好的精确性（下面第二个图）。
因而说明了，重复性和精确性在某些检验指标中不可间得的问题。


![Imgur](http://i.imgur.com/zUiyLyf.png)

![Imgur](http://i.imgur.com/szsx7pi.png)


### Conclusions

1. $$FC_{difference}$$和改良的t检验都是t检验的一种改良形式，也就是有不同的$$s_0$$。一些$$s_0$$的选取可以提高精确性。
2. 别用普通的t检验。
3. 可重复性高并不暗示着精确性高，The issues of reproducibility and accuracy should be kept separate when evaluating the performance of a statistic.
4. 在实际分析中并没有FC和t统计量谁好谁坏的说法，都要看生物学意义。有噪声干扰就用改良的t检验，没有噪声干扰就用FC。

### 参考资料

[^1]: [Significance analysis of microarrays](https://en.wikipedia.org/wiki/Significance_analysis_of_microarrays)

[^2]: [A Modif ied T-test Feature Selection Method and Its Application on the HapMap Genotype Data](http://www.tu.edu.sg/home/elpwang/PDF_web/07_GPB.pdf)


