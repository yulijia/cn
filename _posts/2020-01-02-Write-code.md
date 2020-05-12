---
published: ture
layout: post
title: "写代码"
author: Yu
categories: 聚类不能
tags:
- 代码
---

最近在整理硬盘时发现了一个久远的代码文件夹，里面有我从大学开始写的数学计算程序和研究生时期的一些处理数据的脚本。回顾了一下，发现数学相关的程序很多都记不清算法了，研究生时期的脚本写得又特别的青涩（low）<code>╮(￣▽￣)╭</code>。

![img](https://i.imgur.com/Qr94bBll.png)

为了腾出几M的硬盘空间。我决定把一些常用的方法都挪到博客上，温故知新，重新学习一遍（<u>学了也会忘记的，不经常用的方法是不会记在脑内的</u>，就当个松鼠，收集整理好，存在网络上）。

有些完全没有技巧性的，我就挪到[英文博客](http://yulijia.net/en/categories/#HowTo)了。中文博客记录一些可以展开说明的内容。

如无特殊说明，所有程序均按照初期使用的语言编写，其中MATLAB替换成Octave，Python是3.6以上版本，R是最新版本，Perl语言用Perl5，c和c++用电脑里GCC最新版，操作系统是CentOS或者Fedora。

在这里，还要说一下写代码的习惯，最开始的时候，仗着自己用Linux系统，我连代码程序文件的后缀`.pl`，`.sh`都不写，这样造成的重大问题是，光看文件名，我自己都不清楚这个程序是用什么语言写的。
在自己研究生时期的研究工作硬盘[彻底报废](http://yulijia.net/cn/%E7%94%9F%E6%B4%BB%E7%82%B9%E6%BB%B4/2016/04/04/so-sad.html)的时候，抢救回来的数据，很多都是文本格式的乱码，如果当时写了文件名后缀，那么在数据恢复的时候，软件可以根据后缀来选择恢复的数据类型。

其次，写代码要有注释，下面是一个规范的有注释的MATLAB代码。我的其他MATLAB代码，都没写注释，由于MATLAB都是矩阵运算，读起来就很费力了。

```matlab
function dijkstra(V,o)
%V为邻接矩阵，o为零点标号，输出向量d是零点到每个点的距离
A=V;%定义可变矩阵
[m,n]=size(A);
d=zeros(1,m);%零点到个点的距离
d(:)=inf;
Q=A(o,:);%零点所在行的矩阵
d(o)=0;%零点到零点的距离为0
p=10;%循环标志
while(min(Q)~=inf&p~=0)%判断条件矩阵为inf或距离没有inf项时停止
    [a id]=min(Q);%求最小值及其标号
    Q(id)=inf;%消去已经求出的值
    A(o,id)=inf;%消去已经求出的值
    o=id;%转换行列
    if d(id)>a%所求距离比已知小的时候代换
        d(id)=a;
    end
    for j=1:m%改写矩阵的距离
        if (Q(j)>d(id)+A(id,j))
            Q(j)=d(id)+A(id,j);
        end
    end
    p=0;%循环标志设0值
    for i=1:m%检查是否有inf项
        if d(i)==inf
            p=p+1;
        end
    end
end
d
end
```

最后，程序里要写metainfo，例如编写时间，修改时间，修改内容，作者，联系方式等等。尤其在开源软件中，写metainfo会方便记录代码是否有多人进行维护（有点类似于git commit）

2020年5月3日再次提醒自己，写代码一定要有注释，否则，你根本不记得自己三个月前写了什么。。



- [How to rename files](http://yulijia.net/en/howto/2020/01/02/how-to-rename-files.html)
- [Fibonacci数列](http://yulijia.net/cn/%E8%AE%A1%E7%AE%97%E6%96%B9%E6%B3%95/2020/01/03/Fibonacci-sequence.html)
- [Kruskal's algorithm](http://yulijia.net/en/howto/2020/01/05/Kruskal-algorithm.html)
- [常用下载方式总结](http://yulijia.net/cn/%E8%BD%AF%E4%BB%B6%E4%B8%96%E7%95%8C/2020/01/06/Download-tools.html)
- [Perl的没落](http://yulijia.net/cn/%E7%94%9F%E7%89%A9%E4%BF%A1%E6%81%AF/2020/01/07/Fall-of-Perl.html)
- [Dijkstra's algorithm](http://yulijia.net/en/howto/2020/01/06/Dijkstra-algorithm.html)
- [How to draw multiple ggplot2 figures on a page](http://yulijia.net/en/howto/2020/01/15/How-to-draw-multiple-ggplot2-figures-on-a-page.html)
- [树根和回文串](http://yulijia.net/cn/%E7%BC%96%E7%A8%8B%E5%8E%9F%E7%90%86/2020/05/03/digital-root-and-palindrome.html)
- [老古董Fortran](http://yulijia.net/cn/%E8%BD%AF%E4%BB%B6%E4%B8%96%E7%95%8C/2020/05/03/Fortran.html)
- [计算机图形学I--基础画线](http://yulijia.net/cn/%E5%8F%AF%E8%A7%86%E4%BF%A1%E6%81%AF/2020/05/03/Computer-Graphics-I.html)
- [计算机图形学II--基础填充几何变换](http://yulijia.net/cn/%E5%8F%AF%E8%A7%86%E4%BF%A1%E6%81%AF/2020/05/04/Computer-Graphics-II.html)
- [计算方法系列I - 求积分](http://yulijia.net/cn/%E8%AE%A1%E7%AE%97%E6%96%B9%E6%B3%95/2020/05/09/find-the-integration.html)

