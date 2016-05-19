---
published: ture
layout: post
title: "Rmarkdown的Tufte模板用xeCJK包写中文的一点问题"
author: Yu
categories: 格式技巧
tags:
- Tufte
- xeCJK
- Rmarkdown
- LaTeX
- bookdown
---

我自己的系统里没有安装windows下的字体，也不打算装ctex宏包，所以需要用xeCJK宏包来显示中文。

如果在没有安装SimSun字体的情况下使用Rmarkdown里的tufte包的模板写中文文档，编译时会报错找不到SimSun字体。
这是因为tufte模板里作者默认使用ctex，ctex默认使用了SimSun字体。

如果把ctex去掉，用`in_header: header.tex` 的方法来调用xeCJK宏包，那么会发现有些页面的字会重叠或者不显示。

例如在模板的中文例子里“响应式页面”后面有一段话：

```markdown
# 响应式页面

这个包生成的HTML页面是响应式的：
如果页宽小于760像素，边栏内容会自动隐藏。
此时我们可以点击脚注的序号显示它，其它边栏附注则可以通过点击圆圈加号的符号显示。

# 结语

希望诸位喜欢R Markdown的超级简洁性，同时我们感谢Tufte-CSS和Tufte-LaTeX项目的作者们，没有他们的辛勤劳动，就没有这个**tufte**包。
这份文档的R Markdown源文档可以在[Github上找到](https://github.com/rstudio/tufte/raw/master/inst/rmarkdown/templates/tufte_ctex/skeleton/skeleton.Rmd)，
或者直接使用RStudio菜单`File -> New File -> R Markdown -> From Template`新建一个文档，或直接从R里面打开这个Rmd文件：
```

但是在生成的文档中缺失了。

![Imgur](http://i.imgur.com/BsXTesC.png)


解决这个问题的最简单方法就是在header里重新定义上边界和下边界的距离。

```latex
\usepackage{xeCJK}  
\setCJKmainfont{WenQuanYi Zen Hei} 
%定義top和bottom邊界的距離
\usepackage{geometry}
\geometry{top=2cm,bottom=2cm}
```
所以完整的Rmarkdown YAML 写法是：

```YAML
---
title: "Tufte样式"
subtitle: "一个R Markdown实现"
author: "JJ Allaire，谢益辉"
date: "`r Sys.Date()`"
output:
  tufte::tufte_handout:
    citation_package: natbib
    includes:
      in_header: header.tex
    latex_engine: xelatex
biblio-title: 参考文献
bibliography: skeleton.bib
link-citations: yes
---

```

其中header.tex 像上面$$\LaTeX$$例子中的那样。


## 这是打脸最快的一篇文章

20160519更新

我现在已经不用tufte包了，改用bookdown包的`bookdown::tufte_handout2`。

**强烈推荐使用，但要注意编译后的排版同tufte包的有所不同，主要是bookdown包里的tufte样式貌似没有对table进行优化。**

在bookdown里配置YAML实现中文tufte sytle的方法如下所示。

```YAML
title: "A Minimal Book Example"
author: "Yihui Xie"
date: "`r Sys.Date()`"
output: 
  bookdown::tufte_handout2:
    citation_package: natbib
    latex_engine: xelatex
    includes: 
      in_header: header.tex
    toc: yes
link-citations: yes
description: "This is a minimal example of using the bookdown package to write a book."
```



