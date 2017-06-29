---
published: true
layout: post
title: "cDNA片段库的高通量测序以及交联免疫扩增（HITS-CLIP和CLIP-seq）"
author: Yu
categories: 生物信息
tags:
- 测序技术
- HITS-CLIP
- CLIP-seq
---

HITS-CLIP 和 CLIP-seq 可以用于定位体内的蛋白质RNA相互作用位点。这个测序技术同[RIP-seq](http://yulijia.net/cn/%E7%94%9F%E7%89%A9%E4%BF%A1%E6%81%AF/2017/06/20/RNA-immunopreciprtation-sequencing.html)类似，但是用交联来固定蛋白质RNA复合物。方法是将RNA蛋白质复合物用紫外线交联并做免疫沉淀。复合物经过RNA酶和蛋白酶K的处理，然后提取RNA，并逆转录成cDNA，测序结果可提供精确到单碱基的蛋白质与RNA结合信息。

![HITS-CLIP_and_CLIP-seq](http://i.imgur.com/hBGHzWu.png)

技术优点：

1. 用交联来固定蛋白质的靶向结合位点
2. 紫外线交联可以应用于实验材料体内
3. 由于使用RNA酶消化，可以得到低噪声高分辨率的结合位点
4. 不需要对所研究的RNA结合信息有先验了解
5. 全基因组水平的RNA扫描

技术缺点：

1. 没有特异性靶标的抗体可能会结合非特异性的复合物
2. 紫外线交联不是非常有效，需要蛋白质和RNA近距离结合，远距离的可能会无法形成复合物
3. 交联步骤可能会引入外源污染物
