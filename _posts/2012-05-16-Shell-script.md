--- 
published: true
title: Shell 处理文本常用命令
layout: post
author: Yu
categories: 
- 壳牌脚本
- 编程攻略
tag: Shell

---

没啥技术含量，最近频繁使用，仅做存档，持续更新。

###1.剔除重复行###

<span style="color: #993300;"><code>uniq filename</code></span>

效果

<code>原始文档：
4
4
5
5
5</code>

<code>使用后：
4
5</code>

###2.分割文件###

<span style="color: #993300;"><code>split -500 filename</code></span>

效果

<code>将文件每500行分割成一个子文件</code>

###2.1.grep分割文件###

<span style="color: #993300;"><code>grep -w 'abc' filename</code></span>

效果

<code>按照关键词abc，提取出其所在行的内容</code>

###3.按某列排序并提取某一行###

<span style="color: #993300;"><code>cat filename | sort -k2nr |awk '{FS=","; print \$1"\t"\$7}' &gt;newfilename</code></span>

效果

<code>按第二列排序，并提取第一列和第七列的值，输入到指定文件中</code>

