--- 
published: true
title: 坑了同学——机器学习与应用
layout: post
author: Yu
category: 参会有感
tags:
- Bioinformatics
- Generalized Correlation Analysis
- Machine Learning
- 调控网络

---
破折号后面的是主要内容，破折号前面的是次要内容。


首先今天去听了机器学习与应用的研讨会（MLA 2011 - Chinese Workshop on Machine Learning and Applications），这个消息是从Resys China那边知道的。之前还在组里向导师推荐，导师又把这个消息转发到了整个组，以及某些合作伙伴那里。我还告知了其他组的老师和整个班级的同学。因为下周就期末考试了，最后只有一个同学和我同去。结果听完感觉有点把她给坑了，还不如自己一个人去，省得人家一天没复习也没写作业并且晚上还要做别的活动整天都耽误了，在此再次深表歉意 <code>m(_ _)m</code>


为啥这样说呢，主要是这个活动是冲着Michael Q Zhang去的，但由于这次会议主要用中文做报告，Michael的生物知识学的都是英文的，把生物方面的名词翻译成中文之后在讲出来，估计是把他难为怀了，整个过程讲得不太流畅。内容方面，前面是基础知识，我们听着都明白，在座的其他专业的同学都听不明白，后面将应用，没有说具体的机器学习的方法只是简单的提了一下，都是介绍实验室做过的一些工作以及今后的研究方向（有价值，对于我来说就是了解了做生物信息的人会去做哪些工作）。到最后由于时间太紧，提问只有一个名额，我们这边还以为要举手，结果没人理，被一个问何时开概率图模型课程的同学抓到了机会……在此再次再次对同学深表歉意 m(_ _)m


介绍一下整天的内容。


上午首先报告是《多视图在利用未标记数据学习中的效用》，在半监督学中的主要方法是：generative methods、SV3Ms、Graph-based methods、Disagreement-based methods。南大老师做的一些工作表明大家都很熟悉的co-training过程中数据的“多视图”并不重要。co-training问题的主要特点在于：条件独立性、弱独立性、expanson、large difference。他们还定义了一个“完美图”的概念——一个图上所有样本都在同一个class里，说明这些样本是属于同一类的。主动学习主要有两种情况：realizable（能找到分类器、有完美划分）和non-realizable（对噪音信息不知道）。综合半监督学习和主动学习的方法在计算某些问题时是很好的方法。


第二个报告：《style adaptive pattern field classification》，主要是模式识别的内容（会议从这里开始偏向应用，机器学习的内容越来越少）。介绍了style constraint in PR（模式里的样本服从统一分布）、statistical foundation（很多问题是非独立同分布的）、一些历史性工作（seoarating style and content with bilinear model\gaussian style mixture model\style context with second-order statistics）。在类别数很大的情况下所用的方法是：adaptation by style transfer和bayesian field classification with style normalization


第三个报告是微软的关于enabling knowledge driven computing，是关于文本的机器识别理解的。主要通过不同的文本例子解释在机器学习中要注意的问题如何从concept到instance，从instance到concept。还讲了explicit semantic analysis。


下午第一个报告是关于心智成长的，是由北交的一位老师介绍国外的实验室做的工作，文章是How to grow a mind: Statistics, structure and abstraction。这篇文章有75个参考文献，其中40个都是自己实验室的结果，这要是在国内的期刊上是不可能出现的 。但是这个实验室的确是在认识科学和心理学方面的权威， 独创成果很多。对于心智成长问题的主要认识有三个阶段：第一阶段是nativist ，转换到计算机领域就是符号逻辑；第二阶段是associationist，转换到计算机领域就是learning over the unstructured forms of  knowledge；第三阶段，也就是这个实验室的看法是constructivism or "theory theory"，兼有前面两者的内容。主要模型是bayesian models（层次贝叶斯方法）。先验的样子是怎样的？先验本身是怎么来的？这些问题的讨论都在文章中提到。


下午第二个报告是高维多视图数据的广义相关分析，我唯一有点听明白的内容（看到slide中的那么多公式实在是太亲切的T_T）。对于数据的分析，很多时候要做的是相关性分析。数据的种类很多（主要是网络信息数据方面，例如图的tags和内容），有的数据是一一对应的x1-&gt;y1,...,xn-&gt;yn，被称为配对问题。但是有的数据是部分对应的x1-&gt;y1,x2-&gt;y2,...xk-&gt;yk,x(k+1)不对应到y(k+1)...后面的都不对应，被称为不配对问题。配对分析和半配对分析有很多方法，例如CCA。南京航空航天大学的陈松灿教授介绍了半配对无监督、半配对有监督、半配对半监督的相关分析方法，如何改造最初的式子，如何从配对转到半配对的。一些有用的方法LCA\PPLCA\semiCCA。


之后就是Michael Q Zhang的machine learning in bioinformatics，在海量信息中找寻生命遗传的规律。提到的具体模型是HMM隐马尔可夫。主要学要生物信息学家解决的问题是structure和function之间的对应关系。以前做的工作测序yeast全基因组，找它的共表达序列，寻找调控这些基因表达的元件位置。有假阳性干扰的时候也可用机器学习的方法排除这些干扰。概率图模型是一类重要的方法。生物信息学研究的一个方向是建立生物体内的调控网络，例如神经调控网络，更加系统的研究序列-结构-功能之间的关系（就是系统生物学啊）。


最后一个讲座没有听，时间太晚，回校之后还有很多事情要做，有点可惜，但也很没办法，每年11月初的一周举办的这个活动正是研一考试的开始阶段。


**总结一下，概率图模型是我需要学习的一类方法，生物学中还有很多很多问题需要我们用信息学的手段加以解决，广义相关分析可以学习一下，看着slide上的公式推导很感兴趣。**
