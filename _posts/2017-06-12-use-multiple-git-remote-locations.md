---
published: ture
layout: post
title: "使用（Push/Pull）多个Git远程仓库"
author: Yu
categories: 软件世界
tags:
- Git
- 远程同步
---


众所周知，GitLab.com 在今年年初上演了一场惊天大戏——[从删库到直播](https://about.gitlab.com/2017/02/01/gitlab-dot-com-database-incident/)。
最近一段时间GitHub也经常down个十几分钟，据说是断电引起的。

![GitHub_down](http://i.imgur.com/5HmTBcr.png)
![Reason_of_GitHub_down](http://i.imgur.com/9k9GTtG.png)


**为了避免工作上的不便，是时候使用远程同步到多个git仓库了！！**

前不久由于在考虑跳槽，想把现在的工作都保存到云端以免丢失。自从[硬盘挂了](http://yulijia.net/cn/%E7%94%9F%E6%B4%BB%E7%82%B9%E6%BB%B4/2016/04/04/so-sad.html)之后就对自己电脑上的存储设备不再信任，但是存“别人”硬盘上，也肯定不能保证一点问题都没有，例如Apple云同步有权限删除大于180天的资料。由于现在的工作都是在GitHub私有仓库里进行的，考虑到直接复制到硬盘占地方又有设备之间同步的问题，所以干脆把仓库同步到其他远程git仓库服务中。

方法是从[stackoverflow](https://stackoverflow.com/questions/849308/pull-push-from-multiple-remote-locations "pull/push from multiple remote locations")上复制下来的，仅此备份。


**我已经在本地有一个名叫cn的仓库，同步到gitlab，现在想把这个仓库也同步到github，操作如下：**

```bash
## 以https://github.com/yulijia/cn 为例
## 首先cd到仓库相应目录
## 不需要 Git 初始化 git init
## 添加备份仓库地址（在此之前要在备份仓库网站创建相应的空白仓库）
git remote add alt git@github.com:yulijia/cn.git
## Git 添加文件信息
git add .
git commit -m "git init push"
## push到备份地址
git push --set-upstream origin master
```


之后每一次添加commit的push操作都要用两次`git push`，这样才能将本地内容分别备份到两个云端仓库中。
