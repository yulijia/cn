---
published: true
layout: post
title: "Jupyter，IJulia以及IRkernel"
author: Yu
categories: 软件世界
tags:
- Jupyter
- IJulia
- IRkernel
---

之前（今年一月份）本以为Jupyter这种形式可以很成功的复制到Jilia和R上，结果我发现装个IJulia非常费尽。
依赖的一个模块在安装时使用`curl -f -o /root/.julia/v0.4/ZMQ/deps/downloads/zeromq-3.2.4.tar.gz -L http://download.zeromq.org/zeromq-3.2.4.tar.gz`的地址已经找不到安装包了。
换成Github的结果还因为亚马逊云的问题没下载下来。顿时失去了用Jupyter写IJulia的兴趣。
20160607更新，上述逗逼问题已经解决了，安装ZMQ要用系统的安装命令`dnf  install zeromq3*` 或者 `apt-get install libzmq3*`。成功安装好IJulia！
ZMQ.jl 两天前更新了新的版本，但是需要在julia里及时更新METAINFO `Pkg.update()` 否则安装时还会出现上述问题。

另外，Rstudio太好用，以至于自己也出了个简易的R notebook，我就没兴趣用IRkernel了。

Jupyter还是用来写python比较好。
