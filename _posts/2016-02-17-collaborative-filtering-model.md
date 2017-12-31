---
published: true
layout: post
title: "协同过滤"
author: Yu
categories: [论文笔记]
tags:
- 协同过滤
- 推荐系统
- KDD
- SVD
- LSI
---

回顾一下看过的关于协同过滤，推荐系统的论文。


**1.Application of Dimensionality Reduction in Recommender System -- A Case Study**

Knowledge Discovery in Databases(KDD) 中文是在已有数据中找寻知识的技术。

这个可以算是SVD方法做数据降维，协同过滤的一篇非常早的方法。看起来非常简单。

一般我们做推荐产品都是基于一个群体的，这个群体是个sub-group，
整个电商网站的用户会有很多，但是用户之间不一定都有很强的关系。
所以就需要寻找某个用户的邻近用户，
通过这些和他（她）很相似的邻近用户的一些行为来推测他（她）的行为（购买行为，喜欢购买的商品）。
邻居不一定是对称数量的，也就是A有5个邻居，而A的邻居B可能有20个邻居。

推荐系统做的最基本的两个事情：1.预测用户A对某个产品的喜爱程度；2.为用户A推荐一系列产品（用户A可能会购买的）。
在研究中遇到的主要问题：1.稀疏矩阵；2.大数据，计算慢；3.潜在同义词（商品）不好关联在一起。
关于稀疏矩阵在多说两句：有时Pearson nearest neighbor algorithm无法对某些用户推荐很多商品，这时因为存在reduced coverage问题。
如果相似度阈值取得较高，那么用户的邻居空间就会很小，所以在很小的邻居空间里可能就没有很多商品可以用来进行预测和推荐。

在这里本文作者用SVD方法主要解决了两个问题：1.找寻用户同产品间的潜在关系，使得我们可以计算某个用户对某个产品的喜爱程度。
2. 降维，用低维空间代替高维“用户-产品”空间，在低维空间中计算邻居。

这个“用户-产品”矩阵$$R$$是$$i$$个用户对$$j$$个产品的打分。


为了预测，首先要对稀疏矩阵进行填充数值：就是把矩阵里的NA，填成相关的数值。
有两种方法：1.填充用户的打分平均值；2.填充商品的平均得分。试验结果表明用后者较好。
接下来要对数据进行标准化，也有两个可行方案：1.转换成[$$z-score$$](https://en.wikipedia.org/wiki/Standard_score)；2.对于每个数值减去用户的平均值。试验结果表明用后者较好。

$$R_{norm}=R+NPR$$

其中NPR是个需要自己填充的矩阵，提供简单的非个性化推荐。

然后就进行矩阵分解得到低秩的近似矩阵：

- 用SVD分解，获得$$U$$，$$S$$，$$V$$
- 将$$S$$降维到$$k$$维
- 计算$$S_{k}^{1/2}$$，也就是$$S_{k}$$的平方根
- 计算resultant matrices(结式矩阵)：$$U_{k}S_{k}^{1/2}$$和$$S_{k}^{1/2}V_{k}^{'}$$

对于任意一个用户c以及产品p，可以得到预测的得分为：

$$C_{p_{pred}}=\bar{C}+U_{k}*\sqrt{S_k}^{'}*(c)*\sqrt{S_k}*V_{k}^{'}(P)$$


就写这么多，这篇文章后面有例子，一步一步写得很清楚，可以按照例子计算一次，基本方法就会了。


**2.A Linear Ensemble of Individual and Blended Models for Music Rating Prediction**
**3.Novel Models and Ensemble Techniques to Discriminate Favorite Items from Unrated Ones for Personalized Music Recommendation**

这2篇是KDD比较经典的一次比赛，内容就是协同过滤，预测用户对雅虎音乐的打分。做协同过滤最好都看看这篇文章，计算机和数学两方面写的都不错。
台大的多人小组差不多把能用上的方法都用了，人多力量大，这篇文章算是给大家讲解了各种方法解决这类问题的一个思路。

他们所用到的方法有（第一个task中）：

1. Matrix Factorization
2. Restricted Boltzmann Machines
3. kNN
4. Probabilistic Latent Semantic Analysis
5. Probabilistic PCA
6. Supervised Regression

**4.Hybrid Recommendation Models for Binary User Preference Prediction Problem**
这篇还是KDD比赛的，比较了多种neighborhood-based model，latent factor model，content-based model加上SVD分解降维后的结果。
方法要比台大朴素，但效果也很不错。

另外之前说过的[模型融合](http://yulijia.net/cn/机器学习/2012/04/06/model-ensemble.html)也是看了这几篇KDD文章来慢慢了解的。

**5.Factorization Meets the Neighborhood: a Multifaceted Collaborative Filtering Model**

这篇文章是在看文章4的时候提到的，主要就是看里面的公式（5） 潜在因子（latent factor）模型的公式。

[recsyscode](https://code.google.com/archive/p/recsyscode/) 里对文章中的模型有很好的代码实现。



### 单词本

|英文|中文|英文|中文|
|:----:|:----:|:----:|:----:|
|unsubtle|咄咄逼人|depict|描绘|
|latent|潜在|semantic|语义|
|leverage|利用，运用，平衡|delineate|划定|
|sparsity|稀疏|alleviate|减轻缓和|
|retrieval|检索|syntactic|语法，句法|
|norm|范数|taxonomy|分类|
|blend|混合|stochastic|随机|
