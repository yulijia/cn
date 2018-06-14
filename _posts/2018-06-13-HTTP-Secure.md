---
published: true
layout: post
title: "网站添加了HTTP Secure"
author: Yu
categories: 聚类不能
tags:
- https
- GitHub
---

更新了一下网站的连接，全部都转成`https`。在GitHub Page页面的设置中，最下方有enforce https的选项，这个应该是同Let's Encrypt之类的公司合作的，只要是GitHub Page, 就可以免费获得http secure保护。
但是一定要注意，勾选enforce https之前你的域名DNS必须指向GitHub指定的IP地址，例如：我的博客设定的是[apex domain 指向GitHub Page](https://help.github.com/articles/setting-up-an-apex-domain/)。

开了https之后，别忘了更新网站上不是https的css，js，img链接。

利用sed更新所有md文档的img地址
```
for i in *.md; do sed -i 's/http\:\/\/i.imgur.com/https\:\/\/i.imgur.com/g' $i; done
```

中科大的 google font 源也不管用了（可能是我自己网络的问题），已把它在css中禁用。不管怎样，网站默认字体根据系统自定，凑合看吧。


半年没更新了，还要再闭关一段时间，就这样。
