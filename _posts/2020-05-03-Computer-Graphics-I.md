---
published: ture
layout: post
title: "计算机图形学I--基础画线"
author: Yu
categories: 可视信息
tags:
- "Bresenham's line algorithm"
- "Digital Differential Analyzer"
---

为什么我今天这么闲，可以更水这么多篇博客，那是因为昨天在家办公感觉比在办公室还累，所以索性不干了。`(* ￣︿￣)`

本篇内容所有程序都是MATLAB/GNU Octave上运行的。

注意：有没有最后的`end`可能是上面两个编译环境的区别，但是我没有安装MATLAB，所以没法测试MATLAB现在的函数组成中是否仍旧不带最后一个`end`。

## 数值微分法画线

众所周知，在屏幕上连续的点组成了线条。那么如何在计算机中模拟这些由“点”生成的线呢，这就是计算机图形学要研究的内容，其中最简单的一个问题就是画直线。

数值微分法（ Digital Differential Analyzer，DDA）是一种处理此种问题的经典算法。

算法思想：

1. 给定一条线段的起点$$(x_1, y_1)$$和终点$$(x_2, y_2)$$，分别计算在两轴上的差值 $$\Delta y = y_{2} - y_{1}$$ 和 $$\Delta x = x_{1} - x_{2}$$。
2. 比较$$\Delta y$$和$$\Delta x$$二者谁比较大，大的那一个就作为遍历的总步数。$$steps = max(\Delta x, \Delta y)$$。我的程序中简化了这个部分，直接把x作为主序方向。
3. 计算在x和y方向上单步的步距。 $$d_x = \frac{\Delta x}{steps}$$，$$d_y = \frac{\Delta y}{steps}$$。我的程序里只计算了y方向的单步距离，x方向一直是“进1”。
4. 我的程序中根据$$x_0$$和$$x_1$$的大小决定划线的方向，y增长的部分是根据斜率和目前点的位置来计算的。这个过程涉及大量的浮点运算，效率上是比较低的。

```matlab
function [Xdata Ydata]=DDALine(x0,y0,x1,y1)
% DDALine(8,9,2,6)
% DDALine(2,6,8,9)
% DDALine(1,9,6,5)
% DDALine(6,5,1,9)
deltaX=x1-x0;
deltaY=y1-y0;
if deltaX~=0&&deltaY~=0
    Slope=double(deltaY)/double(deltaX);
    CurrentY=double(y0);
    j=1;
    if x0<x1
        for CurrentX=int8(x0):int8(x1)
                plot(CurrentX,int8(CurrentY-0.5),'* r');
                Xdata(j)=CurrentX;
                Ydata(j)=int8(CurrentY-0.5);
                hold on;
                
                CurrentY=Slope+CurrentY;
                j=j+1;
        end
    end
     if x0>x1
        for CurrentX=int8(x0):-1:int8(x1)
            plot(CurrentX,int8(CurrentY-0.5),'* r');
            Xdata(j)=CurrentX;
            Ydata(j)=int8(CurrentY-0.5);
            hold on;
            
            CurrentY=-Slope+CurrentY;
            j=j+1;
        end
    end
    title('DDAline');
    xlabel('x');
    ylabel('y');
    hold on
end
if deltaX==0&&deltaY~=0
    plot(x1,min(y0,y1):max(y0,y1),'* r');
end
if deltaX~=0&&deltaY==0
    plot(min(x0,x1):max(x0,x1),y0,'* r');
end
grid on;
end
```
## Bresenham's line algorithm

Bresenham line's algorithm 是DDA的一种改进算法。它与DDA相比有质量和效率的两点改进：

1. 以y方向为例，Bresenham line 根据斜率的方向，决定每一个点是离$$y_1$$还是$$y_2$$近，从而给出下一个点的位置究竟是y+1还是y-1。
2. 由于上述原因，该方法避免了大量的浮点小数计算。

```matlab
function  [a,k]=Bresenhamline(x0,y0,x1,y1)
% Bresenhamline(8,9,2,6)
% Bresenhamline(2,6,8,9)
% Bresenhamline(1,9,6,5)
% Bresenhamline(6,5,1,9)
dx=x1-x0;
dy=y1-y0;

d1=abs(2*dx);
d2=abs(2*dy);
x=x0;y=y0;

plot(x,y,'*');
a=[x y];
k=1;
if(abs(dx)>=abs(dy))
    e=-abs(dx);
while abs(x)~=abs(x1)
    if(dx>=0) x=x+1;end
    if(dx<0) x=x-1;end
    e=e+d2;
    if e>0
        if(dy>=0)y=y+1;end
        if(dy<0)y=y-1;end
        e=e-d1;          
    end
    hold on;
    a=[a;x y];k=k+1;
    hold on;
    plot(x,y,'*');
end
end
if(abs(dx)<abs(dy))
    e=-abs(dy);
while abs(y)~=abs(y1)
    if(dy>=0) y=y+1;end
    if(dy<0) y=y-1;end
    e=e+d1;
    if e>0
        if(dx>=0) x=x+1;end
            if(dx<0) x=x-1;end
        e=e-d2;          
    end
    hold on;
    a=[a;x y];k=k+1;
    hold on;
    plot(x,y,'*');
end
end
hold on;
grid on;
end
```


