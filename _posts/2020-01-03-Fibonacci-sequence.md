---
published: ture
layout: post
title: "Fibonacci数列"
author: Yu
categories: 计算方法
tags:
- Fibonacci
- 递归
- 时间复杂度
- 通项公式
---

接上篇内容，翻倒远古时期用MATLAB写的Fibonacci数列第N项的计算方法，直觉上写一个递归函数就可以搞定问题，但是其计算时间复杂度是<code>O(2^n)</code>。

当然，如果需要降低时间复杂度，应该写成循环的形式。我一开始以为自己写的就是递归函数的版本，查着资料，写着博客，猛然发现自己写的就是循环。

```matlab
%古老的脚本，从第三项开始计算数列的内容
function y=Fibonacci(k)
    a=[1 1];
        for i=3:k
        a(i)=a(i-1)+a(i-2);
        end
    y=a(k);
end
```

如果还想偷懒，可以写成矩阵计算的样子。

$$\begin{bmatrix}f_{n+1} \\ f_{n}\end{bmatrix}=\begin{bmatrix}1 & 1 \\ 1 & 0\end{bmatrix}\cdot\begin{bmatrix}f_{n} \\ f_{n-1}\end{bmatrix}$$

```matlab
function y=Fibonacci(n)
  a=[1 0];
  b=[1 1;1 0];
  y=a*b^(n)*[0;1];
end
```

到这里，其实还没进入我想说的内容。我为了查询Fibonacci数列的算法，搜索了一些资源，基本总结有4种方法（递归，循环，矩阵，通项），最后一种就是用通项公式进行计算。

看到第四种方法时，我懵了，Fibonacci数列还有通项公式？等我再看到通项公式的内容，才发现，这个公式在高中时期就已经学过了。对于公式的内容，自己一直没有记住过。温故知新，这次从头学了一遍通项公式的计算。

具体方法，即从上面的矩阵方法中，求$$\begin{bmatrix}1 & 1 \\ 1 & 0\end{bmatrix}$$的特征值和特征向量，然后带回到方程中，已知$$f_{0}=\begin{bmatrix}1  \\  0\end{bmatrix}$$ 然后可求通项[^1]。

网上还有一些初级数学的方法可以求解，但是我忘记高中时候是怎么推导的了（很可能是用差分方法），如果有机会，翻翻之前的笔记，尽量找出来。

[^1]: [Fibonacci number: Matrix form](https://en.wikipedia.org/wiki/Fibonacci_number#Matrix_form)

