---
published: ture
layout: post
title: "常用下载方式总结"
author: Yu
categories: 软件世界
tags:
- aria2
- wget
- rsync
- bypy
- scp
---

### 断点续传

网络传输速度很大程度上会影响我的工作。服务器与服务器之间的通连，有时`scp`不是最好的选择，例如：网络出现问题，两个服务器之间的连接断开后，使用`scp`再次连接时无法进行断点续传。

使用rsync做服务器之间的文件传输（备份），可以做到断点续传。

```bash
rsync -avzP -e 'ssh -p 8888' abc@xxx.xxx.xxx.xxxx:/home/abc/filename ./
```

### wget并行下载

`-P 8`八线程，`-t 0`无限重试，`-nv` 下载时只显示更新和出错信息，不显示指令的详细执行过程

就是输入的地址urls.txt，每一行用一个wget命令进行下载，一次最多同时下载8个文件。

```bash
xargs -P 8 -n 1 wget -nv -c -t 0 <urls.txt
```

### wget下载动态连接的文件

```bash
wget -c 'http://some.site.com/download?id=234&status=download' -O output_filename
```

随时上网检索一下，上面这个方法不一定每个动态连接的文件都能下载，例如google网盘的。


### aria2分段下载大文件

`-s 3` 分成3份，`-x 3` 用3个连接从服务器下载文件

```bash
aria2c  -s 3 -x 3 "https://baidu.com/d/datadump.current.zip"
```

### bypy将百度云盘数据下载到服务器

安装信息：(bypy)[https://github.com/houtianze/bypy]

测试发现，大文件上传比慢。文件只能上传到`全部文件>apps>bypy`这个文件夹。


