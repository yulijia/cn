--- 
published: true
title: 在不同电脑上git push同个github账户下的repositories
layout: post
author: Yu
category: 知行并进
tags: 
- Github
- Git

---
###起因

终于回家了啊，但是还不忘工作呀。把github的内容拷到移动硬盘里，带了回来。用自己的电脑继续写博客，结果gitpush出问题了。用了一个未知用户名push了一条更改记录。

###经过

上网搜索了一下，主要是SSH Keys没有配置好，先在本地电脑建立一个SSH Keys，然后在github上添加公钥。之后用git pull将本地版本库与github上的保持一致。

####方法

方法一：把A电脑上的密钥拷贝到B电脑上，名字可以不使用id_rsa，例如这里名字改为，id_rsa.new。

方法二：用ssh-keygen重新生成ssh公钥/密钥对。


####具体步骤

1. 检查SSH Keys，将已有的key备份。（[做什么都要备份，要不就干等着吃亏吧](http://yulijia.net/en/git/2012/10/09/github-pages.html "all file on your disk folder will be deleted")）

          $cd ~/.ssh
          $ls
              config  id_rsa  id_rsa.pub  known_hosts
          $mkdir key_backup
          $cp id_rsa* key_backup
          $rm id_rsa*

2. 添加SSH Keys
          
    1. 复制老key到新电脑上，cp A电脑上~/.ssh/id_rsa  到B电脑上 ~/.ssh/id_rsa.new，并把权限改为600
    
              $ssh -T git@github.com  #测试看是否能成功
                   Hi 你的名字! You've successfully authenticated, but GitHub does not provide shell access.
                   
    3. 重新生成新key
    
              $ssh-keygen -C "youremail@youremail.com" -f ~/.ssh/id_rsa.new

3. 设置用户名和电子邮件。      

  
          $ git config --global user.name "Firstname Lastname"
          $ git config --global user.email "youremail@youremail.com"
          
4. 本地运行 git pull。

###结果

打通<q>任督二脉</q>，成功了。

###参考链接

- [使用github换电脑了怎么办？](http://jpuyy.com/2012/07/use-github-and-change-computer.html "使用github换电脑了怎么办？")

- [Git的多账号如何处理？](https://gist.github.com/suziewong/4378434 "Git的多账号如何处理？")

- [多个github帐号的使用配置](http://goo.gl/3eUg8 "多个github帐号 google搜索结果")

- [non-fast forward](http://stackoverflow.com/questions/1713137/github-first-push-problem-how-to-merge-remote-changes "Github first push problem… how to merge remote changes?") 
