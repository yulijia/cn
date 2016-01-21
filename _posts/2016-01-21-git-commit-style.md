---
published: ture
layout: post
title: "git commit 编写风格模板"
author: Yu
categories: 格式技巧
tags:
- Git
---


最近看了Ruan YiFeng写的[Commit message 和 Change log 编写指南](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)。
了解了如何写规范的commit message。

### 编写规范

先简要记录一下编写规范，这部分内容可以直接看Ruan YiFeng的博客，要比我写的详细。
编写规范里基本所有内容都来自于Ruan YiFeng的博客，这是我第一次，也是最后一次，在自己的博客里大规模的搬运其他博客的内容。

~~~
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
~~~

commit message包含三个部分，header, body和footer，其中header必须有，body和footer可以按情况省略。

**type 字段**

- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

**scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。**

也就是写用户会感觉到改变在哪个地方。

**subject是 commit 目的的简短描述，不超过50个字符**

- 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
- 第一个字母小写
- 结尾不加句号（.）

**Body 部分是对本次 commit 的详细描述，可以分成多行**

- 使用第一人称现在时，比如使用change而不是changed或changes。
- 应该说明代码变动的动机，以及与以前行为的对比。

**Footer**

- 如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。
- 关闭 Issue

另外，也可以包括JIRA issue references或者其他actions。

<q>**Revert**</q>

这是一种特殊情况，为了撤销前面的操作。

如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header。

~~~
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
~~~

Body部分的格式是固定的，必须写成`This reverts commit &lt;hash>.`，其中的`hash`是被撤销 commit 的 `SHA 标识符`。
如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，
那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的Reverts小标题下面。

https://github.com/yulijia/cn/commit/e36d3ee657107623ff3fffc4bf8aec4b26a9bac0

### 修改git message默认编辑器

说了这么多写作规范，如果有个模板可以直接拷贝，是再好不过的。

使用模板之前，先对git message的默认编辑器做个修改，默认的是`nano`，但这个软件我不会用。

用下面的命令，可以把默认编辑器改成`vim`：

~~~
git config core.editor "vim"
~~~

### 使用模板

我采用了[Linell编写的模板](https://gist.github.com/Linell/bd8100c4e04348c7966d)

安装方式如下：

~~~
curl https://gist.githubusercontent.com/Linell/bd8100c4e04348c7966d/raw/37c1f07f864587a01eb051dc38264267f4a840df/.git-commit-template.txt >> ~/.git-commit-template.txt
git config --global commit.template ~/.git-commit-template.txt
~~~


另外，在这里也提供一个中文的模板

~~~
curl https://gist.githubusercontent.com/yulijia/fe2522fe138b6ed41ff4/raw/5fa0007d1863f70cf4631f2dc1513c8676cd4ab8/.git-commit-template.txt >> ~/.git-commit-template.txt
git config --global commit.template ~/.git-commit-template.txt
~~~
