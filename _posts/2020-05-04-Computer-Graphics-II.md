---
published: ture
layout: post
title: "计算机图形学II--基础填充几何变换"
author: Yu
categories: 可视信息
tags:
- Scanline rendering
---

[昨天没写完](http://yulijia.net/cn/%E5%8F%AF%E8%A7%86%E4%BF%A1%E6%81%AF/2020/05/03/Computer-Graphics-I.html)，今天补上后半部分。现在回想起来计算机图形学是我本科时期上的最有意思的一门课程，其他解方程如果没有联系到实际问题，实在是太枯燥了。为啥我们的本科数学教科书不能改改，从更加应用的方向讲起呢。

## 扫描线算法

扫描线算法(Scanline rendering, Scanline alghorithm)主要用途是填充在屏幕上显示的几何图形。这个方法就是一个点一个点、一条线一条线，像扫描一样，把一个多边形的内部填满。
要想填充多边形内部的所有像素，需要找到一种合适的规则，能够沿着一个方向，一个像素不漏地把多边形内部填满，同时不污染多边形外部。于是上世纪六十年代，人们发明了一条水平方向的扫描线，它从$$y=0$$开始，判断与多边形的交点，这些交点把扫描线分成了若干段，之后判断哪些“段”在多边形内部，哪些“段”在多边形外部，然后把内部的部分着色，完成后，令$$y=y+1$$，即扫描线上移一格，重复之前的操作，直到扫描线不再与多边形的任何部分相交。


![ScanLine](https://i.imgur.com/i7tDkvh.gif)

我的这个程序里用Bresenham’s line 的方法画多边形的边，然后用扫描线算法判断哪些像素是在多边形内部。


```matlab
function scanline(x,y)
%测试数据：
% x=[10 50 30]./2;y=[30 20 70]./2;
% x=[10 30 50 20]./2;y=[20 10 50 70]./2;
% x=[20 50 110 110 50 20]./5;y=[20 10 30 80 50 70]./5;
% x=[20 25 210 110 80 20 50]./5;y=[20 5 60 80 50 70 35]./5;
% x=[20 25 100 210 110 80 20 50]./5;y=[20 5 40 30 80 50 70 35]./5; 

n=length(x);
kk=1;
A=[0,0];
x=[x,x(1)];
y=[y,y(1)];
for i=1:n
[a,k]=Bresenhamline(x(i),y(i),x(i+1),y(i+1));%画边
kk=kk+k;
A=[A;a];
end
A=A(2:kk,:);
m=kk-1;

y0=min(A(:,2));
y1=max(A(:,2));

yy=y0;
datayy=[inf inf];
while yy<y1
    k=0;
    for i=1:m
        if A(i,2)==yy
            k=k+1;
            D(yy,k)=A(i,1);         
        end
    end
    d0=min(D(yy,1:k));
    d1=max(D(yy,1:k));
    for j=d0:d1-1
%          pause(0.001);
%         plot(j,yy,'ro');
        datayy=[datayy;j yy];
    end   
    yy=yy+1;
end


x0=min(A(:,1));
x1=max(A(:,1));

xx=x0;
dataxx=[inf inf];
while xx<x1
    k=0;
    for i=1:m
        if A(i,1)==xx
            k=k+1;
            D(xx,k)=A(i,2);         
        end
    end

    d0=min(D(xx,1:k));
    d1=max(D(xx,1:k));
    for j=d0:d1-1
%          pause(0.001);
%         plot(xx,j,'ro');
        dataxx=[dataxx;xx j];
    end    
    xx=xx+1;
end

if size(dataxx(:,1))>size(dataxx(:,1))
    for i=2:size(dataxx(:,1))
        for j=2:size(datayy(:,1))
            if dataxx(i,1)==datayy(j,1) && dataxx(i,2)==datayy(j,2)
                plot(dataxx(i,1),dataxx(i,2),'ro');
                 pause(0.001);
            end
        end
    end
else
    for i=2:size(datayy(:,1))
        for j=2:size(dataxx(:,1))
            if datayy(i,1)==dataxx(j,1) && datayy(i,2)==dataxx(j,2)
                plot(datayy(i,1),datayy(i,2),'ro');
                 pause(0.001);
            end
        end
    end
end

end
```

## 其他图形变换

最终我为了展示自己所有的画图方法，搞了个大demo程序，把所有画线和几何图形的变换都囊括在一张图里。程序里可能还有些bug。
这其中包括：旋转变化，平移变换，比例变换，对称变换（关于x轴），错切变换，相对(2,2)点的旋转变换。

错切变换（transvection）是啥？就是把矩形变成平行四边形的变换。



![demo](https://i.imgur.com/Iqxrvi9.png)

```matlab
function demo
    figure
    subplot(4,2,1)   
    [Dx Dy]=DDALine(4,6,8,10)%DDALine(x(1),y(1),x(2),y(2))
    [X2]=Bresenhamline(1,2,6,7)%Bresenhamline(x(1),y(1),x(2),y(2))
    Bx=X2(:,1);
    By=X2(:,2);  
%----------------------------------------------    
    %二维几何变换
    s=45;
    T=[cos(s) sin(s) 0;
       -sin(s) cos(s) 0;
       0 0 1];
    title('旋转变换(逆时针)');
    xlabel('x');
    ylabel('y'); 
   for i=1:size(Dx(:))
       z=[double(Dx(i)) double(Dy(i)) 1];
       z=z*T;
       XX(i)=z(1);
       YY(i)=z(2);
       plot(XX,YY,'*- k')
   end
   for i=1:size(Bx(:))
       z=[double(Bx(i)) double(By(i)) 1];
       z=z*T;
       XXX(i)=z(1);
       YYX(i)=z(2);
       plot(XXX,YYX,'*- y')
   end
%----------------------------------------------    
   subplot(4,2,2)
    T=[1 0 0;
       0 1 0;
       4 5 1];
   
   for i=1:size(Bx(:))
       z=[double(Bx(i)) double(By(i)) 1];
       z=z*T;
       XXX(i)=z(1);
       YYX(i)=z(2);
        plot(XXX,YYX,'*- g')
        title('平移变换');
        xlabel('x');
        ylabel('y'); 
   end
   hold on
   plot(Bx,By,'* b');
%----------------------------------------------
   subplot(4,2,3)
    T=[2 0 0;
       0 2 0;
       0 0 1];
   
   for i=1:size(Bx(:))
       z=[double(Bx(i)) double(By(i)) 1];
       z=z*T;
       XXX(i)=z(1);
       YYX(i)=z(2);
        plot(XXX,YYX,'*- g')
        title('比例变换');
        xlabel('x');
        ylabel('y'); 
   end
   hold on
   plot(Bx,By,'* b');
%----------------------------------------------
   subplot(4,2,4)
    T=[1 0 0;
       0 -1 0;
       0 0 1];
   
   for i=1:size(Bx(:))
       z=[double(Bx(i)) double(By(i)) 1];
       z=z*T;
       XXX(i)=z(1);
       YYX(i)=z(2);
        plot(XXX,YYX,'*- g')
        title('对称变换(关于x轴)');
        xlabel('x');
        ylabel('y'); 
   end
   hold on
   plot(Bx,By,'* b');
%----------------------------------------------
   subplot(4,2,5)
    T=[0 -1 0;
       -1 0 0;
       0 0 1];
   
   for i=1:size(Bx(:))
       z=[double(Bx(i)) double(By(i)) 1];
       z=z*T;
       XXX(i)=z(1);
       YYX(i)=z(2);
        plot(XXX,YYX,'*- g')
        title('对称变换(关于y=-x轴)');
        xlabel('x');
        ylabel('y'); 
   end
   hold on
   plot(Bx,By,'* b');
   %----------------------------------------------
   subplot(4,2,6)
    T=[1 -1 0;
       2 1 0;
       0 0 1];
   zx=[1 5 3 1];
   zy=[3 4 0 3];
   clear XXX
   clear YYX
   for i=1:size(zx(:))
       z=[double(zx(i)) double(zy(i)) 1];
       z=z*T;
       XXX(i)=z(1);
       YYX(i)=z(2);
        plot(XXX,YYX,'*- g')
        title('错切变换');
        xlabel('x');
        ylabel('y'); 
   end
   hold on
   plot(zx,zy,'*- b');
   %----------------------------------------------
   subplot(4,2,7)
    T1=[1 0 0;
       0 1 0;
       -2 -2 1];
   T=[cos(s) sin(s) 0;
       -sin(s) cos(s) 0;
       0 0 1];
   clear XXX
   clear YYX
   for i=1:size(Bx(:))
       z=[double(Bx(i)) double(By(i)) 1];
       z=z*T1*T*(-1*T1);
       XXX(i)=z(1);
       YYX(i)=z(2);
        plot(XXX,YYX,'*- g')
        title('相对(2,2)点的旋转变换');
        xlabel('x');
        ylabel('y'); 
   end
   hold on
   plot(Bx,By,'* b');

end
```
