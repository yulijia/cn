---
published: ture
layout: post
title: "对于芯片数据中fold change方法和t统计量方法得比较"
author: Yu
categories: 论文笔记
tags: [fold-change,t-statistic, modified t-statistic]
---

A comparison of fold-change and the t-statistic for microarray data analysis，这文章是大神Robert Tibshirani和Daniela M. Witten（是Robert的一个学生，现在华盛顿大学生统专业做PI）写的。整篇文章每句话都<q>非常重要！</q>  我只有膜拜的份。

最近碰到了芯片的数据，在这个年代还用芯片数据做RNA分析，优势（价格便宜）和劣势（测不准啊）都非常明显。

对于芯片数据中control和treatment样本间信号强度的比较，筛选差异大的基因，会用到fold-change或者t-statisitic。
文章作者比较了这两种情况的计算出的差异基因之间的差别。
说明在没有背景噪声的情况下用fc比较好，在有背景噪声的情况下用t-statisitic。
