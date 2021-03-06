---
published: ture
layout: post
title: "计算方法系列I - 求积分"
author: Yu
categories: 计算方法
tags:
- 复化辛普森公式
- 复化梯形公式
- 牛顿-柯特斯公式
---

开始介绍本科时期学习的计算方法的内容，即求积分，求方程的根（普通的x元x次方程，方程组），所涉及到的基本步骤都是迭代循环之类的。

这个部分的程序都是C语言（极少部份C++语法）写的，`system('pause')`在linux下不管用。不知道为什么那时候写程序`{`都会换行，现在看起来好不习惯。



## 1.牛顿-柯特斯公式 (Newton–Cotes formulas)

后面要介绍的复化辛普森法和复化梯形法都是[牛顿-柯特斯公式](https://en.wikipedia.org/wiki/Newton%E2%80%93Cotes_formulas)的特殊形式，所以先介绍一下牛顿-柯特斯公式的形式：

$$\int_a^b f(x)\mathrm{d}x\approx\sum_{i=1}^{n-1}\omega_{i}f(x_i)$$

### 1.1.左边为啥能约等于右边呢？

这是根据拉格朗日插值法进行的推导计算。对于拉格朗日插值法的直观理解推荐看[知乎马同学的回答](https://www.zhihu.com/question/58333118/answer/262507694)。

拉格朗日插值法构造了穿过已知的一组点的曲线的函数表达式。

那么对于一个定积分问题，我们可以简化成求解穿过a与b两个点的曲线与X轴的面积。


![Trapezoidal_rule_illustration](https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Trapezoidal_rule_illustration.png/220px-Trapezoidal_rule_illustration.png)

即 $$f(x)$$ 这条曲线，可以根据a与b，采用拉格朗日插值法**近似**表示为 $$P_1(x)=\frac{(x-x_1)}{x_0-x_1}f(x_0)+\frac{(x-x_0)}{(x_1-x_0)}f(x_1)$$，其中$$x_0=a$$，$$x_1=b$$

将$$P_1(x)$$带入求解定积分（这部分的具体推导可以[翻墙看The Math Guy的视频](https://www.youtube.com/watch?v=zuFYaHE0twI)）。

$$\int_a^b f(x)\mathrm{d}x\approx\frac{1}{(x_1-x_0)}\int_{x_0}^{x_1}[(x-x_0)f(x_1)-(x-x_1)f(x_0)]\mathrm{d}x$$

最后结果等于 $$\frac{x_1-x_0}{2}[f(x_1)+f(x_0)]$$，将$$\frac{x_1-x_0}{2}$$ 看作 $$\omega_{i}$$，假设我们已知a,b以及a,b之间一系列的点，最终可以根据拉格朗日插值法得到牛顿-柯特斯公式。

上面简化成a与b两点的例子的结果就是梯形公式$$\int_a^b f(x)\mathrm{d}x\approx\frac{b-a}{2}[f(b)+f(a)]$$
简化成a,$$\frac{a+b}{2}$$,b的三点的结果，就是辛普森公式 $$\int_a^b f(x)\mathrm{d}x\approx\frac{b-a}{6}[f(a)+4f(\frac{a+b}{2})+f(b)]$$


### 1.2.那么复化（composite）是什么意思呢 [^1]？

应用高阶牛顿-科特斯公式计算积分时，会出现数值不稳定的情况（[龙格现象（Runge's phenomenon）]（https://en.wikipedia.org/wiki/Runge's_phenomenon)），而低阶公式往往因为积分步长过大使得离散误差变大，因此，为了提高求积公式的精度，可以把积分区间分成若干个子区间，在每个子区间上使用低阶求积公式，然后将结果加起来，这种方法称为**复化求积法**。

将区间[a,b]划分为n等分，步长为$$h=\frac{b-a}{n}$$，节点为$$x_i=a+ih$$， $$i=1,2,...,n+1$$，在每个子区间$$[x_i,x_{i+1}]$$使用梯形公式得：

$$\int_a^b f(x)\mathrm{d}x \approx \sum_{i=1}^{n}\int_{x_i}^{x_{i+1}}f(x)\mathrm{d}x = \frac{h}{2}[f(a)+2\sum_{i=1}^{n-1}f(a+ih)+f(b)]$$, 其中 $$h=\frac{b-a}{n}$$

根据复化梯形公式的推导，同理可得复化辛普森公式为：

$$\int_a^b f(x)\mathrm{d}x \approx \frac{h}{6}\sum_{i=1}^{n-1}[f(x_i)+4f(x_{i+\frac{1}{2}})+f(x_{i+1})]$$, 其中 $$h=\frac{b-a}{n}$$

上面这个公式对于n的取值有一些条件，辛普森法则是根据三个点的位置来推定曲线的函数表达形式，这时需要要求整个区间被分割成**偶数份**[^2]，即n是偶数，公式可以写成$$\int_a^b f(x)\mathrm{d}x \approx \frac{h}{6}\sum_{j=1}^{\frac{n}{2}}[f(x_{2j-2})+4f(x_{2j-1})+f(x_{2j})]$$。

## 2.复化辛普森求积分

终于到了程序的部分，求$$\frac{\sin(x)}{x}$$ 从a到b的积分。

```cpp
#include<math.h>
#include<stdio.h>
#include<stdlib.h>
void main()
{   int n;//定义节点数 
    double a,b;//定义左右节点 
    printf("No.0001复化辛普森求积分(Simpson)\n\n输入节点数：");
    scanf("%d",&n);
    n=n-1; //计算几等分数 
    printf("输入左端点："); 
    scanf("%lf",&a); 
    printf("输入右端点：");
    scanf("%lf",&b); 
   	double pi=3.1415927;
	n=n-1; //计算几等分数 
	double	h=(b-a)/(2*n);//计算步长
	int i,j;
	double x[2*n],y[2*n],t1=0,t2=0,t;
	x[0]=a; 
    x[2*n]=b;
	y[0]=1;//需要手动修改在左端点的值 
	y[2*n]=sin(pi/2)/(pi/2);//需要手动修改在右端点的值
	for(i=1;i<=2*n-1;i++) 
    {
        if(i*h<=b)x[i]=x[0]+i*h;
        }
	for(j=1;j<=2*n-1;j++)
	{
		y[j]=sin(x[j])/x[j];//需要手动修改
     	}
	for(i=1;i<=n;i++)
	{
        t1=t1+4*y[2*i-1];
        }
	for(i=1;i<=n-1;i++)
	{
	t2=t2+2*y[2*i];
    	}
	t=h/3*(y[0]+y[2*n]+t1+t2);//求积分 
	printf("\n步长h：%.7lf\n\n积分值t：%.7lf\n\n",h,t);
	printf("输出相对应的xy值:\n");
    for(i=0;i<=2*n;i++)
	printf("y=%.7lf---x=%.7lf\n",y[i],x[i]);
   	system("pause");
}

```

## 3.复化梯形求积分


接上，仍就求$$\frac{\sin(x)}{x}$$ 从a到b的积分。

```c

#include<math.h>
#include<stdio.h>
#include<stdlib.h>
void main()
{   int n;//定义节点数 
    double a,b;//定义左右节点 
    printf("No.0002复化梯形求积分\n\n输入节点数：");
    scanf("%d",&n);
    n=n-1; //计算几等分数 
    printf("输入左端点："); 
    scanf("%lf",&a); 
    printf("输入右端点：");
    scanf("%lf",&b); 
   	double pi=3.1415927;
	
	double	h=(b-a)/n;//计算步长
	int i,j;
	double x[n+1],y[n+1],t1=0,t;
	x[0]=a; 
    x[n]=b;
	y[0]=1;//需要手动修改在左端点的值 
	y[n]=sin(pi/2)/(pi/2);//需要手动修改在右端点的值
	for(i=1;i<=n-1;i++) 
    {
        if(i*h<=b)x[i]=x[0]+i*h;
        }
	for(j=1;j<=n-1;j++)
	{
		y[j]=sin(x[j])/x[j];//需要手动修改
     	}
	for(i=1;i<=n-1;i++)
	{
        t1=t1+y[i];
        }
	t=h*(0.5*y[0]+0.5*y[n]+t1);//求积分 
	printf("\n步长h：%.7lf\n\n积分值t：%.7lf\n\n",h,t);
	printf("输出相对应的xy值:\n");
    for(i=0;i<=n;i++)
	printf("y=%.7lf---x=%.7lf\n",y[i],x[i]);
   	system("pause");
}

```

其实上面的程序写得都很烂，没有参考文献中的这个好。


```c

#include<stdio.h>
#include<math.h>
double Function(double x)//所要计算积分的函数f(x)
{
    if(x==0)//sin(x)/x在0处的取值为1
        return 1;
    else
        return sin(x)/x;
}
//复化梯形公式
double Trapz(double a,double b,int n)
{
    double h=(b-a)/n;
    double T=0;
    for(int i=1;i<n;i++)
    {
        T=T+Function(a+i*h);
    }
    T*=2;
    T=(Function(a)+Function(b)+T)*h/2;
    return T;
}
//复化辛普森公式
double MulripleSimpson(double a,double b,int n)
{
    double h=(b-a)/n;
    double T=0;
    for(int i=0;i<n;i++)
    {
        T=T+Function(a+i*h)+4*Function(a+(i+0.5)*h)+Function(a+(i+1)*h);
    }
    T=T*h/6;
    return T;
}
void main()
{
    printf("使用复化梯形公式可得：%f\n",Trapz(0,1,8));
    printf("使用复化辛普森公式可得：%f\n",MulripleSimpson(0,1,4));
}

```

当年为了做这个作业，我的还搞了个整合代码（网上找了的程序，修改了一下），还包含了中矩形公式。

```cpp
//数值分析--数值积分公式 
#include"iostream.h"
#include"math.h"
double c[10][10];
double f(double x)
{
  double sum=0;
  if(x==0) return 1;
  sum=sin(x)/x;//计算公式 
  return sum;
}
void initcotes(double c[][10])
{
  c[1][0]=c[1][1]=0.5;
  c[2][0]=c[2][2]=1.0/6.0;c[2][1]=2.0/3.0;
  c[3][0]=c[3][3]=1.0/8.0;c[3][1]=c[3][2]=3.0/8.0;
  c[4][0]=c[4][4]=7.0/90.0;c[4][1]=c[4][3]=16.0/45.0;c[4][2]=2.0/15.0;
  c[5][0]=c[4][5]=19.0/288.0;c[5][1]=c[5][4]=25.0/96.0;c[5][2]=c[5][3]=25.0/144.0;
}
int Trapezoid(double a,double b)
{
  cout<<"梯形公式的结果："<<(b-a)*(f(a)+f(b))/2<<endl;
  return 1;
}
int MidRect(double a,double b)
{
  cout<<"中矩形公式的结果："<<(b-a)*f((b+a)/2)<<endl;
  return 1;
}
int NewtonCotes(double a,double b)
{ 
  int n,k;double h;
  cout<<"请输入n的值（n值最多到5）：";
  cin>>n;
  if(n>=6)
  cout<<"注意n值最多到5"<<endl;
  else{ 
  h=(b-a)/double(n);
  double sum=0;
  for(k=0;k<=n;k++)
   sum+=c[n][k]*f(a+k*h);
  cout<<"牛顿-柯特斯公式的结果："<<(b-a)*sum<<endl;}
  return 1;
}
int STrapezoid(double a,double b)
{ 
  int n,k,q;double h;
  cout<<"1--复化梯形公式"<<endl;
  cout<<"2--复化辛普森求积公式"<<endl;
  cout<<"输入你想进行的操作：";
  cin>>q;  
  cout<<"请输入n的值：";
  cin>>n;
  h=(b-a)/double(n);
  double sum=0;
  sum+=(f(a)+f(b));
  for(k=1;k<=n-1;k++)  sum+=2*f(a+k*h);
 if(q==1)
 {
  cout<<"复化梯形公式的结果："<<(h/2)*sum<<endl;
  return 1;
 }
  for(k=0;k<n;k++)
   sum+=4*f(a+(k+0.5)*h);
  cout<<"复化辛普森求积公式的结果："<<(h/6)*sum<<endl;
  return 1;
}
void main()
{ cout<<"No.0003数值分析--数值积分公式"<<endl;
  double a,b;
  int p;
  cout<<"请输入积分的下限：";
  cin>>a;
  cout<<"请输入积分的上限：";
  cin>>b;
  initcotes(c);
  while(1)
  {
    cout<<"0--退出"<<endl;
 cout<<"1--梯形公式"<<endl;
 cout<<"2--中矩形公式"<<endl; 
 cout<<"3--牛顿柯特斯公式:"<<endl; 
 cout<<"4--复化公式"<<endl;
 cout<<"输入你想进行的操作:";
 cin>>p;
 switch(p)
 {
 case 1:Trapezoid(a,b);break;
 case 2:MidRect(a,b);break;
 case 3:NewtonCotes(a,b);break;
 case 4:STrapezoid(a,b);break;
 }
 if(p==0)  break;
  }
}
```


参考资料

[^1]: [【数值分析】复化积分公式](https://blog.csdn.net/tengweitw/article/details/43311685)
[^2]: [Simpson's Rule: the Formula and How it Works](https://www.freecodecamp.org/news/simpsons-rule/)
