---
published: true
title: GFW大法好
layout: post
author: Yu 
category: 网络观察
tags:
- GitHub 
- Great Firewall
- Baidu
- DDOS
---

真是什么缺德的事情都能做的出来。今天发现<q>git push + https</q>完全不管用了，查了一下原因，估计是这个事情——[百度统计js被劫持用来DDOS Github](http://drops.wooyun.org/papers/5398)，[V2EX讨论地址（需要翻墙）](http://www.v2ex.com/t/179695)。[2015.04.11更新，后续依旧精彩，中华大加农，国外人家没事写了篇论文出来。](http://citizenlab.org/2015/04/chinas-great-cannon/) [2015.04.25更新，google也写了一篇博客来分析。](http://googleonlinesecurity.blogspot.ch/2015/04/a-javascript-based-ddos-attack-as-seen.html)

然后就立即换成<q>git push+ssh</q>进行操作，可以正常提交。

将https换成ssh的方法是把`.git`文件夹里的config文件中的url进行替换，具体config文件例子如下

~~~
[remote "origin"]
        url = git@github.com:yulijia/freshman21.git 
##之前是url = https://github.com/yulijia/freshman21.git
~~~

### 2015.03.29 update

由于DDOS攻击一直在持续，架设在github.io上的网站从中国境内访问有很多问题，另外这个网站之前用了Baidu 的CDN加速，刚才访问时发现，直接5xx报错，我已经将Baidu的加速撤销。

**关掉百度云加速时，首先在系统界面关掉加速，然后再删除网站，切记！否则DNS地址还是百度的**

下面这个命令可以在linux终端中用来查看DNS（ Domain Name System）设置情况:

~~~
### 关掉前
[@localhost ~]# dig yulijia.net +nostats +nocomments +nocmd

;; global options: +cmd
;yulijia.net.     IN  A
yulijia.net.    15  IN  SOA n3368.ns.yunjiasu.com. dns.yunjiasu.com. 2017926777 10000 2400 604800 3600


### 关掉后
[@localhost ~]# dig yulijia.net +nostats +nocomments +nocmd

;; global options: +cmd
;yulijia.net.     IN  A
yulijia.net.    190 IN  A 192.30.252.153
~~~
