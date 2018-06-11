---
published: true
layout: post
title: "通过RNA纯化进行染色质分离"
author: Yu
categories: 生物信息
tags:
- 测序技术
- GRO-seq
- RNA聚合酶II
---

GRO-seq(Global Run-On Sequencing)测序技术可以在整个基因组范围上绘制参与转录的RNA聚合酶的位置、数量并进行定位。在这个技术下，激活的RNA聚合酶II可以在有Br-UTP（Br标记的三磷酸尿苷）的条件下继续反应，RNA会水解并被有Brd-UTP抗体的磁珠抓住（纯化）。洗下来的RNA在逆转录成cDNA前要进行去帽处理和末端修复。对于cDNA的测序结果反映了正在细胞内被RNA聚合酶II转录的RNA。


![GRO-seq](https://i.imgur.com/hh0v5FW.png)

技术优点：

1. 可以map正在转录中的RNA聚合酶II的位置
2. 确定转录位点的相对活性
3. 检测正义和反义转录
4. 检测全基因组转录
5. 不需要已知转录位点的位置

技术缺点：

1. 由于必须在存在标记核苷酸的情况下进行转录，该方案仅限于细胞培养物和其它人造系统
2. 在准备核苷酸的过程中可能会有人造添加剂的干扰
3. 新的转录起始事件可能会在转录时发生 (New initiation events may occur during the run-on step) 没能理解这句话的含义。
4. 物理障碍可能阻断聚合酶的活动
