---
published: ture
layout: post
title: "恢复错删的文件"
author: Yu
categories: 软件世界
tags:
- testdisk
- EasyRecovery
- photorec
---

这是在第七个Leap year的2月29日（暴露了`-_-|||`），记录下的逗比事件。


起因：我写了个程序自动重命名下载的图片，改着改着，程序出了bug，把所有图片从图片文件夹`/media/disk/picure`都移动到了当前脚本的工作目录`/root/bin`。
我以为原图片文件夹还有这些图片，就把当前工作目录下的都删除了。 `-_-b`

经过：从昨天晚上到今天，抽时间找了不同的软件和方法来恢复数据。

1.在linux下采用 <q>testdisk</q> 中的<q>photorec</q> 来恢复图片文件。

如果用终端版的不适应，可以安装GUI `dnf install qphotorec`。
具体步骤可以参考[这里](http://www.cgsecurity.org/wiki/PhotoRec_Step_By_Step)。

在使用时请选择只查找没有文件的区域（Free: from the unallocated space only），否则会花费很长时间，给你找出一堆chrome隐藏的网络图片。

我一共测试了在三种地址查找，1. 在/root/硬盘里搜索全部图片（70G空间），2. 在/root/硬盘里搜索没有文件的区域（小于70G空间），3. 在/media/disk/里搜索没有文件的区域（500G空间）。

在三种找法中，第一种最满。所以千万不要搜索全部空间。

找出的图片有几个问题：首先不会按照原来的名字来命名，其次图片文件信息也会丢失，最重要的是所有文件按照在磁盘的位置（就是从0到最大容量的数字）来存放，查找起想要的文件非常不方便。

2.百度经验里的debugfs修复

[该文档](http://jingyan.baidu.com/article/2f9b480d6c2bcd41cb6cc223.html)应该有错。在`dd if= of=` 这个步骤。出来的结果是无法识别的。

绝对不建议使用，除非很熟悉`dd` 命令。

3.EasyRecovery

只测试了恢复`/meida/disk` 里的文件。**绝赞好评！**

软件下载时请不要从中文网站下载，搜索时发现有两个EasyRecovery网址，这里面肯定有李鬼。

直接从英文网站下载，最好找个带keygen的。免费版我使用不成功。

**用这个软件复原的图片包含原名字，在原文件夹的位置结构，含有图片信息!!!**


