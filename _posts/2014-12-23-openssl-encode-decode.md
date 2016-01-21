---
published: true
title: 文本加密解密
layout: post
author: Yu 
category: 
- 壳牌脚本
tags:
- encode
- decode
- openssl
---

首先普及一个常识，<q>密码</q>是一种用来混淆的技术，它希望将正常的（可识别的）信息转变为无法识别的信息，这种无法识别的信息是可以再加工并恢复的。密码学（cryptology）是研究如何隐密地传递信息的学科。<q>Password或cipher</q>，应该被翻译成口令/暗号（结果现在中文里也翻译成了密码），口令原来的意义是口头暗号，也叫“通行字”，是一个用于身份验证的保密的字符串，用以保护不想被别人看到的隐私以及防止未经授权的操作，达到保护隐私以及防止未经授权的操作的目的。

研究文本加密解密的原因是我记不住自己的网站口令了，索性写如了文档中，进行加密，再存入数据库。

在网上研究了一些加密/解密的方法，最好用的是[openssl](https://www.openssl.org/)这个工具。文本的加密解密主要使用的是openssl里的密码算法库。
如果在网上搜索，可以得到很多基于openssl的加密、解密方法。这里我主要介绍一点，基于enc（symmetric cipher routines）的加密解密时command里要添加<code>-A</code> 选项。这个选项的作用是对于一串字符加密或解密时，所有内容在一行内输出。在需要加密的字符串长度超过40时（今在我的电脑上测试的数据，fedora 20），如果没有加入<code>-A</code>选项，解密时会出现"error reading input file" 以及 "bad magic number" 这两种错误提示。

### 问题重现

```
## 将一个长达45个字符的字符串进行加密，加密方法 enc -aes-256-cfb
$ echo "123456789012345678901234567890123456789012345" | openssl enc -aes-256-cfb -e -base64 -k "test" -salt 
```

```
$ echo "123456789012345678901234567890123456789012345" | openssl enc -aes-256-cfb -e -base64 -k "test" -salt
U2FsdGVkX1+jfo70LlMECXRyLhH9N/Pp9jRK7yMyqdhmEiDdM13fTsh/nntt/yd8
3A2VaByW0yRBIs1oEKk=
```

由上可以看到，加密后的输出被分成了两行。

接下来，对输出内容进行解密:

```
## 对分成两部分的加密字符串分别解密
$ echo "U2FsdGVkX1+jfo70LlMECXRyLhH9N/Pp9jRK7yMyqdhmEiDdM13fTsh/nntt/yd8" |openssl enc -aes-256-cfb -d -base64 -k "test"
12345678901234567890123456789012
$ echo "3A2VaByW0yRBIs1oEKk=" |openssl enc -aes-256-cfb -d -base64 -k "test"
error reading input file

## 对分成两部分的加密字符串合并解密
$ echo "U2FsdGVkX1+jfo70LlMECXRyLhH9N/Pp9jRK7yMyqdhmEiDdM13fTsh/nntt/yd83A2VaByW0yRBIs1oEKk=" |openssl enc -aes-256-cfb -d -base64 -k "test"
error reading input file
$ echo "U2FsdGVkX1+jfo70LlMECXRyLhH9N/Pp9jRK7yMyqdhmEiDdM13fTsh/nntt/yd8 3A2VaByW0yRBIs1oEKk=" |openssl enc -aes-256-cfb -d -base64 -k "test"
error reading input file
$ echo "U2FsdGVkX1+jfo70LlMECXRyLhH9N/Pp9jRK7yMyqdhmEiDdM13fTsh/nntt/yd8\ 3A2VaByW0yRBIs1oEKk=" |openssl enc -aes-256-cfb -d -base64 -k "test"
error reading input file
$ echo "U2FsdGVkX1+jfo70LlMECXRyLhH9N/Pp9jRK7yMyqdhmEiDdM13fTsh/nntt/yd8\n3A2VaByW0yRBIs1oEKk=" |openssl enc -aes-256-cfb -d -base64 -k "test"
error reading input file
```

由上可以看出，根本就无法正常解密之前的字符串。

### 解决方法

查找资料后，发现需要在<code>openssl</code> 语句中增加<q>-A</q>选项，具体为:

```bash
$ echo "123456789012345678901234567890123456789012345" | openssl enc -aes-256-cfb -e -base64 -k "test" -salt -A
U2FsdGVkX19XLlseSQxqXVmA8LIfIpQyEv/lVrM9EJk2RyMcHJsubnxN2M+365RnBG3oxXDYPOBNqIU+q0E=
$ echo "U2FsdGVkX19XLlseSQxqXVmA8LIfIpQyEv/lVrM9EJk2RyMcHJsubnxN2M+365RnBG3oxXDYPOBNqIU+q0E=" |openssl enc -aes-256-cfb -d -base64 -k "test" -A
123456789012345678901234567890123456789012345
```
