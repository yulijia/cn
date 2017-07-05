---
published: ture
layout: post
date: 2017-06-29
title: "Kaggle奔驰猜数字挑战赛"
author: Yu
category: 机器学习
tags:
- Kaggle
- 决定系数
---

大约5天前，Kaggle的一项由[奔驰汽车公司主办的机器学习挑战赛](https://www.kaggle.com/c/mercedes-benz-greener-manufacturing)变成了猜数字挑战赛。比赛原意是通过给定的抹去信息的数据来预测y值，预测结果的准确性根据决定系数来评估。

<q>参与者</q>在Kaggle平台提交`测试数据`的预测结果后，平台会先检测19%的预测结果，产生<q>参与者</q>在公开排名榜的名次。还有81%的预测结果的检测不公布排名，<q>参与者</q>就有了一个自己也不清楚的非公开排名榜的名次。等到比赛结束，公开那个“非公开排名榜”的结果，产生<q>参与者</q>的最终排名。
这个方法本来是为了防止大家通过排名榜来“撞出”测试数据的预测结果，由于这19%和81%的测试结果排序是固定的（不是每次随机挑出19%和81%），在这次的比赛中公开排行榜彻底沦为娱乐工具。

一个<q>参与者</q>在Kaggle论坛上公布了他们的发现，可以用[公开排行榜反馈的决定系数来找出19%测试数据的真实值](https://www.kaggle.com/c/mercedes-benz-greener-manufacturing/discussion/35271)。
原理十分简单：

决定系数（R squared） $$R^{2}=1-\frac{\sum_{i=1}^{N}{(y_i-\hat{y})^2}}{\sum_{i=1}^{N}{(y_i-\bar{y})^2}}$$
分母是个常数，被称作总平方和，记为 $$S_{tot}$$ 。

首先提交一个所有预测结果都为0的答案，得到：

$$R_{0}=1-\frac{\sum_{i=1}^{N}{(y_i-0)^2}}{S_{tot}}=1-\frac{y_1^2}{S_{tot}}-\frac{\sum_{i=2}^{N}{(y_i-\hat{y})^2}}{S_{tot}}$$

然后将预测结果第一个数值改成100，再次提交，可以得到：
$$R_{100}=1-\frac{(y_1-100)^2}{S_{tot}}-\frac{\sum_{i=2}^{N}(y_i)^2}{S_{tot}}$$

通过联立两个方程，就能求解出$$y_{1}$$的真实值。

该方法公布人做了[网站](https://crowdstats.eu/topics/kaggle-mercedes-benz-greener-manufacturing-leaderboard-probing)， 号召大家一起来“撞库”。目前已经停止提交新的撞库结果，因为有人蓄意提交假信息。

说来说去，机器学习比赛中撞库的事情常有发生大多是根据评判测试数据的方法来猜数字。如何能避免这种情况，评估测试结果的19%和81%这两组数据最好要随机产生。在预测数据集足够大的情况下，才能避免此类情况产生不良后果。

最新进展，官方出了一个[声明](https://www.kaggle.com/c/mercedes-benz-greener-manufacturing/discussion/35566)，表示不会公开“公开排行榜”的结果，并且强调若参赛者若过分关注公开排行榜的数据结果，会造成模型过拟合。
