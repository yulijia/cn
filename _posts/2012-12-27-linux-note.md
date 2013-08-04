---
published: true
title: linux系统以及服务器操作笔记
layout: post
author: Yu
category: 知行并进
tags:
- Linux
- 服务器

---
这是一个扫盲指导，对于第一次使用linux的用户，希望能有所帮助，尽量少走弯路，少提naive的问题。

####1. 目录结构

首先是对linux目录结构的理解，它的结构目录是
<center>/</center> 

<center>/bin /sbin /home /tmp /lib /usr /var /etc </center>

没有像C:\ D:\ E:\ 这样的盘符，在Windows系统中我们都把系统文件安装在C:\中，而在linux中系统文件是分别放在不同的目录中的，/bin 中存放编译好的二进制可执行程序，/home 是用户存放数据的目录，/lib 用来存放内核模块和共享链接，具体可以[参考这里](http://linux-wiki.cn/wiki/zh-hans/Linux%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84 "linux结构目录")。

那么为什么linux的目录结构是这个样子？[阮一峰对此有个深入的挖掘](http://www.ruanyifeng.com/blog/2012/02/a_history_of_unix_directory_structure.html "Unix目录结构的来历")。

一般用的服务器多为linux系统的，管理员root会给你开通一个帐号ABC，你登录后进入的用户目录就是/home/ABC。

####2. 登录服务器

如何登录服务器？ 在windows下一般可以下载登录软件putty或者setupssh.zip（我记不住名字是什么了，下载的安装包是这样的名字）。
putty是有一个登录界面软件，setupssh.zip则是可以直接用CMD窗口直接登录。

使用setupssh.zip登录需要的命令是 ssh ABC@xxx.xxx.xxx.xxx  回车后，键入密码。

登录后进入/home/ABC的目录下面，有些管理员允许你在/home文件夹下自己的文件夹里存储文件，但是有些数据量很大的文件（GB\TB级别）是不能存储在/home文件夹里的。这时管理员会告诉你可以将文件存放在哪个目录下。

####3. 安装软件

接下来说说所安装软件，在多用户的服务器上，不是每个用户都有权限将软件安装在/usr /opt之类的文件夹里。那么，你只能将自己需要用的软件安装在自己的/home/ABC文件夹里，
需要编译安装的软件（用C写的），第一步很多时候是./config --prefix=/home/ABC  这个的作用就是指定软件安装的地址，是你自己的目录下。之后程序会自动创建/home/ABC/bin目录来存放二进制文件，自动创建/home/ABC/lib目录来存放共享链接和一些库函数。

在安装后，你会发现很多软件只能在安装的目录下“./软件名”这样执行，这是因为你没有设置[环境变量](http://zh.wikipedia.org/wiki/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F "环境变量")，还不能被相应的应用程序或守护进程访问到安装的软件（这半句的解释不一定正确）。 设置环境变量的方法，请自行google，基本格式是：
<pre><code>

1. 修改profile文件： 
#vi /etc/profile 
在里面加入:
export PATH="$PATH:/home/ABC/build_tools/bin"

2. 修改.bashrc文件：
# vi /<p>root</p>/.bashrc 或者 /home/xxxx/.bashrc  <q>我高估了人类的举一反三能力，指写/root/他们不管有没有权限，都敢往/root/下写<\q>
在里面加入：
export PATH="$PATH:/home/ABC/build_tools/bin"

</code></pre>


**注意：方法1在服务器上是只有管理员级别用户才能做到的。**

####4. 常用命令

查看目录下的文件和文件夹 <code>ls</code>。

查看目录下的文件和文件夹的具体属性 <code>ll</code>。**注意：** <q>ll</q>有两个辅助选项很管，一个是<q>-h</q>可以显示文件的大小（以human看得懂的方式<code>;)</code>，所以你知道为啥简称是h了吧）；另一个是<q>-a</q>可以显示隐藏文件，对了，linux系统下的隐藏文件写法是<q>.文件名</q>，这个辅助选项在<q>ls</q>后面加也管用。

[在文件名前加个点，就看不见了，为啥呢？](https://plus.google.com/101960720994009339267/posts/R58WgWwN9jp "A lesson in shortcuts") 看完原因后，大家是不是都有个<q>姚明笑</q>的表情。

跳转目录 <code>cd</code>目录绝对地址或相对地址（如果调转到下层子目录，可以用相对地址）。

察看文件内容 <code>less</code>。**注意：**<q>less -N</q>命令可以显示文件的行号。另外，二进制文件是无法察看的（你能看到的也是乱码），<q>二进制</q>是给机器看的嘛。

复制文件<code>cp</code>。

将文件传输到本地<code>scp</code>。**注意：**这个需要知道本地的ip地址（我没在Windows下测试过，只在linux下用过）。

很多时候，大家需要在服务器后台上运行程序，而不耽误前台的工作。使用的命令是<code>screen 或者nohup</code>，别用什么奇葩的**at**!!!

其实很多时候，使用linux命令时要多用辅助选项<q>-h</q>查看简单帮助，或者用<code>man</code>查看详细的帮助文档。

还有其他常用的<code>vi, top, awk, grep, diff, ln</code>等等，请自行在需要的时候google。

**要记住，你想做的80%的文件处理工作，linux都有<q>常用工具+简单的pipeline</q>可以帮你实现，不要在处理数据时show自己那点可怜的编程技术，耽误处理的速度。**

**最好的学习方法就是逼迫自己使用linux系统，等你每天都见不到Windows时，你会发现自己变成了一个自由软件的忠实使用者。**

**一个学习参考网站[http://nixsrv.com/llthw](http://nixsrv.com/llthw "Learn Linux The Hard Way")**
