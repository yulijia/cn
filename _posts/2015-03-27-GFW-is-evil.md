---
published: true
title: GFW大法好
layout: post
author: Yu 
category: 网络观察
tags:
- Github 
- Great Firewall
- Baidu
- DDOS
---

真是什么缺德的事情都能做的出来。今天发现<q>git push + https</q>完全不管用了，查了一下原因，估计是这个事情——[百度统计js被劫持用来DDOS Github](http://drops.wooyun.org/papers/5398)，[V2EX讨论地址（需要翻墙）](http://www.v2ex.com/t/179695)。

然后就立即换成<q>git push+ssh</q>进行操作，可以正常提交。

将https换成ssh的方法是把`.git`文件夹里的config文件中的url进行替换，具体config文件例子如下

~~~
[remote "origin"]
        url = git@github.com:yulijia/freshman21.git 
##之前是url = https://github.com/yulijia/freshman21.git
~~~


