---
published: ture
layout: post
title: "数值分析III--求方程组的根"
author: Yu
categories: 计算方法
tags:
- Jacobi
- Gauss-Seidel
---



## 1. 雅克比(Jacobi)迭代法求方程组的根

雅克比迭代法非常简单，对于一个给定的n×n方程组$$\displaystyle A\mathbf {x} =\mathbf {b} $$

$$\displaystyle A={\begin{bmatrix}a_{11}a_{12}\cdots a_{1n}\\a_{21}a_{22}\cdots a_{2n}\\\vdots \vdots \ddots \vdots \\a_{n1}a_{n2}\cdots a_{nn}\end{bmatrix}},\qquad \mathbf {x} ={\begin{bmatrix}x_{1}\\x_{2}\\\vdots \\x_{n}\end{bmatrix}},\qquad \mathbf {b} ={\begin{bmatrix}b_{1}\\b_{2}\\\vdots \\b_{n}\end{bmatrix}}.$$


可以把 A分解成两个矩阵

$$\displaystyle A=D+R\qquad \qquad D={\begin{bmatrix}a_{11}0\cdots 0\\0a_{22}\cdots 0\\\vdots \vdots \ddots \vdots \\00\cdots a_{nn}\end{bmatrix}},\qquad R={\begin{bmatrix}0a_{12}\cdots a_{1n}\\a_{21}0\cdots a_{2n}\\\vdots \vdots \ddots \vdots \\a_{n1}a_{n2}\cdots 0\end{bmatrix}}$$


方程组可以改写为 $$\displaystyle D\mathbf {x} =\mathbf {b} -R\mathbf {x} $$，该公式即为迭代公式。

又可写成 $$\displaystyle \mathbf {x} ^{(k+1)}=D^{-1}(\mathbf {b} -R\mathbf {x} ^{(k)})$$。

注意这种解方程组的问题，矩阵都要满一定的收敛条件，在这里是迭代矩阵的谱半径小于1，$$\rho (D^{-1}R)<1$$。

```cpp
#include"math.h"
#include"stdio.h"
#include"stdlib.h"
void main()
{
	double x1,x2,x3,x11,x22,x33;
    int i=0;
    printf("No.0008雅克比迭代法求方程组的根\n\n输入初值：");
    scanf("%lf %lf %lf",&x1,&x2,&x3);
    while(fabs(x11-(1-x2-x3)/(-8.0))>0.001 && fabs(x22-(16-x1-x3)/(-5.0))>0.001 && fabs(x33-(7-x1-x2)/(-4.0))>0.001)
  {
	x11=(1-x2-x3)/(-8.0);//写迭代式 
	x22=(16-x1-x3)/(-5.0);//写迭代式
	x33=(7-x1-x2)/(-4.0);//写迭代式
	x1=x11;
	x2=x22;
	x3=x33;
    i++;
  }	
	printf("解为：\nx1=%lf\nx2=%lf \nx3=%lf\n迭代次数：%d\n",x1,x2,x3,i);
system("pause");
} 

```



## 2. 高斯-赛德尔(Gauss-Seidel)迭代法求方程组的根

高斯-赛德尔迭代法和雅克比迭代法的区别在于，将A分解为一个上三角矩阵和下三角矩阵的形式。

$$\displaystyle A=L_{*}+U\qquad {\text{其中}}\qquad L_{*}={\begin{bmatrix}a_{11}0\cdots 0\\a_{21}a_{22}\cdots 0\\\vdots \vdots \ddots \vdots \\a_{n1}a_{n2}\cdots a_{nn}\end{bmatrix}},\quad U={\begin{bmatrix}0a_{12}\cdots a_{1n}\\00\cdots a_{2n}\\\vdots \vdots \ddots \vdots \\00\cdots 0\end{bmatrix}}$$

这样，代入迭代式后为：

$$\displaystyle L_{*}\mathbf {x} =\mathbf {b} -U\mathbf {x}$$

$$\displaystyle \mathbf {x} ^{(k+1)}=L_{*}^{-1}(\mathbf {b} -U\mathbf {x} ^{(k)})$$

系数矩阵 A 严格对角占优或对称正定时，高斯-赛德尔迭代法必收敛。

```cpp
#include"math.h"
#include"stdio.h"
#include"stdlib.h"
main()
{
	double x1,x2,x3,x11,x22,x33;
    int i=0;
    printf("No.0009高斯赛德尔(Gauss-Seidel)迭代法求方程组的根\n\n输入初值：");
    scanf("%lf %lf %lf",&x1,&x2,&x3);
    while(fabs(x11-(1-x2-x3)/(-8.0))>0.01 && fabs(x22-(16-x1-x3)/(-5.0))>0.01 && fabs(x33-(7-x1-x2)/(-4.0))>0.01)
  {
	x11=x1;x22=x2;x33=x3;
	x1=(1-x2-x3)/(-8.0);//写迭代式 
	x2=(16-x1-x3)/(-5.0);//写迭代式
	x3=(7-x1-x2)/(-4.0);//写迭代式
    i++;
  }	
	printf("解为：\nx1=%lf\nx2=%lf \nx3=%lf\n迭代次数：%d\n",x1,x2,x3,i);
system("pause");
}
```

## 3. 牛顿迭代法求方程组的根

这个根牛顿迭代法求解方程的根一样。。。

$$\displaystyle x_{n+1}=x_{n}-J_{F}(x_{n})^{-1}F(x_{n})$$


其中 $$J_{F}(x)$$是雅克比矩阵。

 
```cpp
#include"math.h"
#include"stdio.h"
#include"stdlib.h"
main()
{
	double x1,x2,x11,x22;
    int i=0;
    printf("No.0010牛顿迭代法求方程组的根\n\n输入初值：");
    scanf("%lf %lf",&x1,&x2);
	x11=x1-(2*x2/(2*x2-8*x1)*(x1+2*x2-3)-2/(2*x2-8*x1)*(2*x1*x1+x2*x2-5));//写迭代式 
	x22=x2-(-4*x1/(2*x2-8*x1)*(x1+2*x2-3)+1/(2*x2-8*x1)*(2*x1*x1+x2*x2-5));
    i++;//写迭代式
 while(fabs(x11-x1)>0.001 && fabs(x22-x2)>0.001)
  { x1=x11;
	x2=x22;
	x11=x1-(2*x2/(2*x2-8*x1)*(x1+2*x2-3)-2/(2*x2-8*x1)*(2*x1*x1+x2*x2-5));//写迭代式 
	x22=x2-(-4*x1/(2*x2-8*x1)*(x1+2*x2-3)+1/(2*x2-8*x1)*(2*x1*x1+x2*x2-5));//写迭代式
    i++;
  }	
	printf("解为：\nx1=%lf\nx2=%lf \n迭代次数：%d\n",x11,x22,i);
system("pause");
} 
```
