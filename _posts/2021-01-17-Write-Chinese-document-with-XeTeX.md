---
published: ture
layout: post
title: "使用XeTeX写中文文档"
author: Yu
categories: 格式技巧
tags:
- XeTeX
- TeX Live
- CTeX
---

这篇也是[写代码](http://yulijia.net/cn/%E8%81%9A%E7%B1%BB%E4%B8%8D%E8%83%BD/2020/01/02/Write-code.html)的一部分，对于 $$\LaTeX$$ 的使用，感觉中文排版之前是一个痛点，其他的宏以及类的使用方法看几个例子就足够了。所以这里只记录了如何用 $$Xe\TeX$$ 写中文文档。除了中英混排，中日、中韩以及日韩、英日、英韩的混排估计都有类似的排版问题，还需要自己搜索相关资料解决。

$$Xe\TeX$$ 支持引擎直接支持 Unicode 字符。别再用什么 CJKutf8 了。 如果你用Linux系统，下载安装$$\TeX Live$$ 套装，安装有界面的编辑软件 Gummi，可以完美的撰写中文文档。我觉得使用相关 Windows 环境下的软件，也能完成这个任务。 另外，$$C\TeX$$ 宏集做中英文混排据说非常棒，如果无法忍受默认的 $$Xe\TeX$$ 排版效果，可以选择 $$C\TeX$$ 宏集。对于我来说用最简单的就足够了。


```LaTeX
\documentclass{article}
\usepackage{fontspec}
\setmainfont{文泉驿点阵正黑}
\XeTeXlinebreaklocale "zh"
\XeTeXlinebreakskip = 0pt plus 1pt minus 0.1pt
\begin{document}
\title{这是Xe\TeX 编排的中文}
\author{YU Lijia}
\maketitle
Xe\TeX 支持引擎直接支持 Unicode 字符。别再用什么 CJKutf8 了。 如果你用Linux系统，下载安装\TeX Live 套装，安装有界面的编辑软件Gummi，可以完美的撰写中文文档。我觉得使用相关 Windows 环境下的软件，也能完成这个任务。 另外，C\TeX 宏集做中英文混排据说非常棒，如果无法忍受默认的Xe\TeX 排版效果，可以选择C\TeX 宏集。对于我来说用最简单的就足够了。

%\tableofcontents
\section{\TeX Live是什么？}

\begin{tabular}[t]{|l|c|c|}
\hline
对比	& CTeX & TeXLive \\
\hline
操作系统 &	只限于Windows下 &	通用 \\
\hline
制作人 & 中科院吴凌云和其他小伙伴 &	TUG \\
\hline
其他 & 对MiK\TeX 的再封装 & 可刻录在光盘直接运行 \\
\hline
\end{tabular}\\
 
C\TeX 和 \TeX Live都是 \LaTeX 的发行版，包括编译器和配套软件安装包。 C\TeX 已经完全过时。所以发行版一定要选择 \TeX Live。
 
\section{C\TeX 发行版和C\TeX 宏集是什么关系}

C\TeX 发行版是基于MiK\TeX 的 Windows下编译\TeX 文件的软件， C\TeX 宏集是专为中英文混排设计的sty宏包和cls文类的集合。


\end{document}
```
