---
published: ture
layout: post
title: "数值分析II--求方程的根"
author: Yu
categories: 计算方法
tags:
- 二分法
- 牛顿迭代法
- 弦割法
---


## 1. 二分法求方程的根

二分法可行的条件是有介值定理支持。

介值定理说明在实数范围内，$$[a,b]$$区间上可以画出一个连续曲线。$$f(a)<u<f(b)$$ 存在，那么存在$$c$$, $$a<c<b$$，使得$$f(c)=u$$。

二分法就是$$a$$与$$b$$异号时，介值定理的特殊情况，即存在实数$$c$$使得$$f(c)=0$$存在。

```cpp
#include"math.h"
#include"stdio.h"
#include"stdlib.h"
double fun(double k)
{return 1-k-sin(k);//所求方程 
}
void main()
{double a,b,x;int i=0;
printf("No.0004二分法求方程的根\n\n输入区间左端点：");
scanf("%lf",&a);
printf("输入区间右端点："); 
scanf("%lf",&b);
x=(a+b)/2.0;
while(/*fabs(fun(x))>0.00005||*/fabs(a-b)>0.00005)//近似范围 
{
if(fun(a)*fun(x)<0) b=x;
if(fun(b)*fun(x)<0) a=x;
x=(a+b)/2.0;
i++;}
printf("方程的根：%lf\n",x);
printf("迭代次数：%d\n\n",i);
system("pause");
}
```

## 2. 迭代法求方程的根

迭代法主要是将$$f(x)=0$$这种等式，该写成$$x=\varphi(x)$$，然后给定一个初始的$$x_0$$，根据公式$$x_1=\varphi(x_0)$$，求出$$x_1$$，接下来，比较$$x_1$$和$$x_0$$的差值大小，如果差值等于0或者一个非常非常小的数，那么则求出最终的$$x$$即为$$x_1$$；如果差值还很大，则进行迭代步骤，将$$x_1$$带入到公式右侧$$\varphi(x_1)$$，求出左侧的$$x_2$$，重复上述比较步骤，直到$$x$$收敛于一个定值。

```cpp
#include"math.h"
#include"stdio.h"
#include"stdlib.h"
double fun(double k)
{
	return pow(1+k*k,1/3.0);//所求方程 
}
void main()
{double a,b,x,x1,l=1;
int i=0,p;
printf("No.0005迭代法方程的根\n\n选择输入数据种类：\n1.数值\n2.区间\n");
printf("\n");
while(l==1)
{scanf("%d",&p);
if(p!=1&&p!=2) printf("请输入指定序号\n\n");//判断输入的序号是否正确 
else l=0;
}
switch(p)
 {
 case 1:
		printf("数据种类\n1.数值\n输入数值：");
		scanf("%lf",&x);
		x1=fun(x);i=i+1;
		break;
 case 2:printf("数据种类\n2.区间\n");
		printf("输入区间左端点：");
		scanf("%lf",&x);
		printf("输入区间右端点：");
		scanf("%lf",&x1);x1=fun((x+x1)/2.);i=i+1;
		break;
 }
while(fabs(x-x1)>0.00005)
{
x=fun(x1);
i=i+1;
x1=fun(x);
i=i+1;
}
printf("方程的根：%lf\n",x1); 
printf("迭代次数：%d\n\n",i);
system("pause");
}
```

## 3.牛顿迭代法

牛顿迭代法又称为牛顿-拉弗森方法(Newton-Raphson method)，它比一般的迭代法有更高的收敛速度。

![Newton-Raphson method](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Ganzhi001.jpg/200px-Ganzhi001.jpg)

$$f(x_0)$$点的切线是$$f(x)$$的线性逼近。离$$f(x_0)$$点距离越近，这种逼近的效果也就越好，也就是说，切线与曲线之间的误差越小。所以我们可以说在$$f(x_0)$$点附近，$$切线\approx f(x)$$。

牛顿-拉弗森方法提出来的思路就是利用切线是曲线的线性逼近这个思想，随便找一个曲线上的$$f(x_0)$$点（为什么随便找，根据切线是切点附近的曲线的近似，应该在根点附近找，但是很显然我们现在还不知道根点在哪里），做一个切线，切线的根$$x_1$$（就是和x轴的交点）与曲线的根，还有一定的距离。我们从这个切线的根$$x_1$$出发，做一根垂线，和曲线相交于$$f(x_1)$$点，继续重复刚才的工作，多次迭代后会越来越接近曲线的根，即迭代收敛。

在计算时，首先选择一个$$x_0$$，然后计算相应的$$f(x_0)$$和切线斜率$$f^{'}(x_0)$$，接下来计算穿过点（$$x_0$$,$$f(x_0)$$）并且斜率为$$f^{'}(x_0)$$的直线和$$x$$轴的交点的$$x_1$$坐标，公式为：
$$0=(x_1-x_0)f^{'}(x_0)+f(x_0)$$， 将其转化为$$x_1=\varphi(x_0)$$的形式，即有：$$x_{n+1}=x_n-\frac{f(x_n)}{f^{'}(x_n)}$$

将初始的$$x_0$$代入到上述公式中，经过多次迭代，可以求得最后的根。

```cpp
#include"math.h"
#include"stdio.h"
#include"stdlib.h"
double fun(double k)
{
	return k*k*k-k*k-1;//所求方程 
}
double fun1(double k)
{  
	return 3*k*k-2*k;//所求方程的一阶导函数 
}
void main()
{double a,b,x,x1,l=1;
int i=0,p;
printf("No.0006牛顿迭代法求方程的根\n\n选择输入数据种类：\n1.数值\n2.区间\n");
printf("\n");
while(l==1)
{scanf("%d",&p);
if(p!=1&&p!=2) printf("请输入指定序号\n\n");//判断输入的序号是否正确 
else l=0;
}
switch(p)
{
 case 1:
		printf("数据种类\n1.数值\n输入数值：");
		scanf("%lf",&x1);
		break;
 case 2:printf("数据种类\n2.区间\n");
		printf("输入区间左端点：");
		scanf("%lf",&x);
		printf("输入区间右端点：");
		scanf("%lf",&x1);x1=(x+x1)/2.;
		break;
 }
while(fabs(fun(x1)/fun1(x1))>0.00005)
{
x=x1-fun(x1)/fun1(x1);
x1=x;
i++;
}
printf("方程的根：%lf\n",x1); 
printf("迭代次数：%d\n\n",i);
system("pause");
}
```

## 4. 弦割法

弦割法(Secant Method)是基于牛顿法的一种改进，基本思想是用弦的斜率近似代替目标函数的切线斜率，并用割线与横轴交点的横坐标作为方程式的根的近似。

![SecantMethod](https://upload.wikimedia.org/wikipedia/commons/thumb/9/92/Secant_method.svg/300px-Secant_method.svg.png)

公式就不推了，参见维基百科或者百度百科。

```cpp
#include"math.h"
#include"stdio.h"
#include"stdlib.h"
double fun(double k)
{
	return k*k*k-k*k-1;//所求方程 
}
main()
{double a,b,x,x1,l=1,x0,x2;
int i=0,p;
printf("No.0007弦割法求方程的根\n\n选择输入种类：\n1.单点\n2.双点\n");
printf("\n");
while(l==1)
{scanf("%d",&p);
if(p!=1&&p!=2) printf("请输入指定序号\n\n");//判断输入的序号是否正确 
else l=0;
}
switch(p)
{
 case 1:
		printf("种类\n1.单点\n");
		printf("输入点1：");
		scanf("%lf",&x);
		printf("输入点2：");
		scanf("%lf",&x1);
        while(fabs(fun(x1)*(x1-x)/(fun(x1)-fun(x)))>0.00005)
        {
        x2=x1-fun(x1)*(x1-x)/(fun(x1)-fun(x));
        x1=x2;
        i++;
        }
        printf("方程的根：%lf\n",x1); 
        printf("迭代次数：%d\n\n",i);
		break;
 case 2:printf("种类\n2.双点\n");
		printf("输入点1：");
		scanf("%lf",&x);
		printf("输入点2：");
		scanf("%lf",&x1);
        while(fabs(fun(x1)*(x1-x)/(fun(x1)-fun(x)))>0.00005)
        {
        x2=x1-fun(x1)*(x1-x)/(fun(x1)-fun(x));
        x=x1;
        x1=x2;
        i++;
        }
        printf("方程的根：%lf\n",x1); 
        printf("迭代次数：%d\n\n",i);
	    break;
}
system("pause");

```

