--- 
published: true
title: 模型融合
layout: post
author: Yu
categories:
- 机器学习
tag: Machine Learning

---
model ensemble /aggregation techniques(201208环球科学)

我对此的理解还比较浅显，最早知道这个东西还是今年看到了一个[PPT](http://www.slideshare.net/xlvector/how-to-do-model-ensemble "how to do model ensemble")，主要理解就是单个模型的结果不够理想，如果想得到更好的结果，需要把很多单个模型的结果融合在一起。

那么究竟是怎么个“融合”呢？ 这个问题之前一直没搞明白，最近在用随机森林方面的方法来处理数据，顿悟出，模型融合可以想像成“再次的机器学习过程”。已知模型A、模型B、模型C，测试数据输出的结果分别为a，b和c，用训练数据通过模型输出的训练数据预测结果为a1，b1和c1。我们可以将a1，b1，c1的数据带入到训练数据中再次训练，得到更加贴近真实结果的模型，再用这个模型训练测试数据结果a，b和c。得到的结果会比一次训练的好。（这其实也就是个多层神经网络的思想，但是与神经网络不同的是：每次的输入数据是“上次的输入数据”+“上次的输入结果”）。

当然，方法多种多样，“上次的输入数据”+“上次的输入结果”是一种输入数据类型，“上次的输入结果”也是一种输入数据类型，融合所用的方法也很多，直接用机器学习里的各类方法，或者用统计回归，皆可。一切皆有可能。

