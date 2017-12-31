---
published: true
layout: post
title: "RNA免疫沉淀测序"
author: Yu
categories: 生物信息
tags:
- 测序技术
- RIP-seq
---

这个就是ChIP-seq的RNA版。

RNA免疫沉淀测序用来定位蛋白质与RNA结合的位置。在该方法中，用特定的蛋白抗体来对RNA-蛋白复合物进行免疫沉淀。 RNA酶消化后，提取蛋白质覆盖的RNA并逆转录成cDNA。 然后将位置映射回基因组。

![RIP-seq](http://i.imgur.com/MSMDDHM.png)

技术优点：

1. 可以针对特异性（研究需要）的蛋白-RNA复合物。
2. 由于使用RNase消化，可以得到背景噪声低，高分辨率的绑定位点信息
3. 不需要任何关于RNA的具体先验知识（不需要提前知道需要的是哪些RNA序列）
4. 全基因组范围的RNA搜索

技术缺点：

1. 需要特定蛋白质的抗体
2. 非特异性抗体将沉淀非特异性复合物
3. 复合物若缺乏crosslink或者稳定性，会造成假阴性
4. RNase消化过程必须仔细控制
