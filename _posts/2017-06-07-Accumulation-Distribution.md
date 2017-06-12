---
published: ture
layout: post
title: "累积分布?累积/派发线!"
author: Yu
categories: 量化投资
tags:
- 累积/派发线
- 股票
---

**Accumulation Distribution** 乍一看可以翻译成累积分布，但累积分布的正确英文写法是cumulative distribution。
今天要说的这个Accumulation Distribution是证券交易中的技术指标——累积/派发线。

难道我这个浓眉大眼的家伙也开始炒股了？ <code>-__,-</code>
当然不是，我只是想用空闲时间了解一些经济学基本知识，从网上找到了[Online Trading Concepts
](http://www.onlinetradingconcepts.com/)，这个和计算有点关系的技术指标介绍网站，所以打算好好看一看，为了记录自己的学习成果，有机会就编译点网站上内容。

累积/派发线通过**成交量**来确认价格趋势，对于可能导致价格波动反转的弱趋势给出预警。

累积：当天收盘高于前一天收盘价时，将成交量计入前一日的成交量累积值中，作为今日的累积/派发线值。
派发：当天收盘低于前一天收盘价时，将成交量从前一日的成交量累积值中减去，作为今日的累积/派发线值。

所以累积/派发线是用来检测价格矩估计和成交量矩估计之间的差异。

![img](http://i.imgur.com/7Mr32v2.gif)

两个时间点之间的成交量曲线是上涨的，那么说明价格会上涨，泛指则应认定为价格会有波动（下降）。

- High #1 到 High #2

图中的High #1 到 High #2 的价格是一样的，但是累积/派发线呈下降趋势，说明价格会有波动（下降）。

- High #3 到 High #4

图中的High #3 到 High #4 的价格是上涨的，但是累积/派发线呈下降趋势，说明价格会有波动（下降）。

- Low #1 to Low #2

a sign of strength， 翻译不好这个strength的意思。但是看图，应该还是波动（下降）趋势。

累积/派发线是一个实用的检测价格趋势反转的指标。其他类似的分析成交量和价格的指标是Chaikin Oscillator (蔡金摆动指标), Money Flow Index (资金流量指标)，以及 Price Volume Trend indicator (价格交易量趋势指标)。
