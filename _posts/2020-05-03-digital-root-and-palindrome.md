---
published: ture
layout: post
title: "树根和回文串"
author: Yu
categories: 编程原理
tags:
- 树根
- C++
---

还是那个[code文件夹](http://yulijia.net/cn/%E8%81%9A%E7%B1%BB%E4%B8%8D%E8%83%BD/2020/01/02/Write-code.html)里的东西，现在写代码的习惯里必须再增加一条，写明这个程序的作用。我整理了不少图形图像和online judge的程序，每次回想程序的用途都是一件非常麻烦的事情，有的时候根本就想不起来。


## 树根

这个问题非常的经典，具体的介绍可以参照[知乎](https://www.zhihu.com/question/30972581)中[leetcode.wang的介绍](https://leetcode.wang/leetcode-258-Add-Digits.html)

![DigitalRoot](https://i.imgur.com/9n8pfkZ.jpg)

对于给定的数字，将其每一位上的数字相加得到新的数字，一直重复这个过程，直到这个数小于10，将这个数输出。

原数是`n`，树根就可以表示成`(n-1) mod 9 + 1`。 主要的用途是计算模运算的同余，对于非常大的数字的情况下可以节省很多时间。数字根可作为一种检验计算正确性的方法。例如，两数字的和的数根等于两数字分别的数根的和。

当时做这道题的时候，想到了树根的问题，但是没有求出其表达式，因而采用了一个比较苯的办法来做计算，即排除数字9,在一个多位数字中，排除9和0的其他数字之和不影响最终的树根结果。那么我就在计算的时候默认排除了9和0的加法运算。

写了一大长串程序，其中的`char - '0'` 是ASCII运算，将字符转换成其对应的数字，<u>这个程序也是本篇文章中唯一可以正常运行的程序</u>。

```c
#include <stdio.h>
int main()
{
      unsigned long a=0,b=0;
      int flag=2;
      char c;
      while(1)
      {
              a=0;b=0;flag=2;
              c=getchar();
              if(c=='0') break;
              else
          {     a=a+(c-'0');
              while((c=getchar())!='\n')
          {
                 if(((c-'0')!=9)&&((c-'0')!=0))
                 {
                     a=a+(c-'0');                             
                 }
          }
         // c='0';
          while(flag>1)
          {    if(a>9)
              {
                  while(a!=0)
                  {    b=b+a%10;
                       a=a/10;
                  }
                  if(b>9) 
                  {
                      flag=2;
                      a=b;
                      b=0;
                  }
                  else{
                       flag=0;
                       a=b;
                       b=0;          
                       break;
                       }            
              }
              else
              {
                  break;
              }
          }
          printf("%d\n",a);
         }
      }  
}
```

谁知道其实答案如此简单<code>(⊙ˍ⊙)</code>。

```c
public int addDigits(int num) {
    return (num - 1) % 9 + 1;
}
```

## 回文串

这程序里有bug，目前无法自动停止。输入一串数字，判断这窜数字是否有回文结构。这个题目主要靠算法思想，但是我没什么思想，只会最简单的按位比较.

例如：输入123321，返回YES；输入123231,返回NO。

```c
#include <cstring>
#include<iostream>
using namespace std;
int isPalindrome(char str[])
{
    int len=strlen(str);
    int i,j;
    i=0;
    j=len-1;
    while(i<j)
    {
        if(str[i++]!=str[j--]) return 0;
    }
    return 1;
}
int main(){
    char str[10001];
    int n,i=0;
    cin>>n;
    while(i<=n-1)
    {   i=i+1;
        cin>>str;
        int a=0;
        a=isPalindrome(str);
        if(a==1) cout<<"YES"<<endl;
        else cout<<"NO"<<endl;
    }
    return 0;
}

```


## 其他

我忘记了这个程序是做什么的，程序名称是MaxArray，估计是个找最大array相关的程序。从这个例子中深刻的体会到，写代码注释的重要性。

```c
#include <stdio.h>
//#include <stdlib.h>
#define MAX 130
int maxSum(int b[], int n)
{
    int max = b[0];
    int sum = 0;
    for(int i = 0; i < n; ++i)
    {
        if(sum < 0) sum = b[i];
        else sum += b[i];
        if(sum > max) max = sum;
    }
    return max;
}

int solve(int a[][MAX], int n)
{
    int b[MAX];int i,j,k,sum,tmp;
    sum = a[0][0];
    for(i = 0; i < n; ++i)
    {
        for(k = 0; k < n; ++k) b[k] = 0;
        for(j = i; j < n; ++j)
        {
            for(k =0; k < n; ++k) b[k] += a[j][k];
            if(sum < (tmp = maxSum(b,n)) ) sum = tmp;
        }
    }
    return sum;
}

int main()
{
    int arr[MAX][MAX];
    int i,j,n;
    while(scanf("%d",&n)!=EOF)
    {
        for(i = 0; i < n; ++i)
            for(j = 0; j < n; ++j)
                scanf("%d",&arr[i][j]);
        printf("%d",solve(arr,n));
        break;
    }
  //  system("pause");
    return 0;
}

```
