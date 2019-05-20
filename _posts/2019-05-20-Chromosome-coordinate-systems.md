---
published: ture
layout: post
title: "染色体坐标系"
author: Yu
categories: 生物信息
tags:
- 坐标系
- 染色体
---

一开始学生物信息分析的时候，知道BED格式中染色体坐标系是从0开始的。用久了各种工具，突然有一天发现SAM和BAM格式的染色体坐标系起始位置是不一样的。猛然间发现生物信息学的分析工具中各种坐标不统一。
读了一些英文资料，觉得有必要在博客里记录一下各种坐标系的位置关系。

### 以0为起点

| sequence | A | C |<font color="red"> G </font>|<font color="red"> T </font>|<font color="red"> A </font>|   |
|:--------:|:-:|:-:|:-:|:-:|:-:|:-:|
|  0-based | 0 | 1 |<font color="red"> 2 </font>|<font color="red"> 3 </font>| <font color="red">4 </font>| 5 |



### 以1为起点

| sequence | A | C |<font color="red"> G </font>|<font color="red"> T </font>|<font color="red"> A </font>|   |
|:--------:|:-:|:-:|:-:|:-:|:-:|:-:|
|  1-based | 1 | 2 |<font color="red"> 3 </font>|<font color="red"> 4 </font>|<font color="red"> 5 </font>| 6 |



除了其实为点的坐标位置不同，终止位置的坐标是否包括最后一个位置，在不同的格式和工具里也是不一样的。

例如上面序列中的GTA的坐标位置：

> 以0为起始位点，包含最后一个位置: 2-4
> 以1为起始位点，包含最后一个位置: 3-5
> 以1为起始位点，不包含最后一个位置: 3-6


下面记录一些工具的染色体坐标系定义位置：


1. 以0为起始位点：SAM, VCF, GFF 和 Wiggle 格式
2. 以1为起始位点：BAM, BCFv2 和 PSL 格式
3. Ensembl：以1为起始位点，包含最后一个位置。[https://asia.ensembl.org/info/docs/api/core/core_tutorial.html](https://asia.ensembl.org/info/docs/api/core/core_tutorial.html)
4. **UCSC Genome Browser**：内部表示，以0为起始位点，并用以1为起始位点时的终止位点（程序员为了编程方便煞费苦心）。外部显示，以1为起始位点。[http://genome.ucsc.edu/FAQ/FAQtracks.html#tracks1](http://genome.ucsc.edu/FAQ/FAQtracks.html#tracks1)
5. **BED 格式**：以0为起始位点，不包含最后一个位置。**BED格式经常使用，在分析中别弄错起始位置和终点位置非常重要** [http://genome.ucsc.edu/FAQ/FAQformat.html#format1](http://genome.ucsc.edu/FAQ/FAQformat.html#format1)
6. MAF 格式：以1为起始位点，包含最后一个位置。




### 参考文献

1. [Chromosome coordinate systems: 0-based, 1-based](https://arnaudceol.wordpress.com/2014/09/18/chromosome-coordinate-systems-0-based-1-based/)
