---
layout: post
title: 基于Sobel算子图像边缘检测的MATLAB实现
date: 2013/09/24 05:49:13
categories: 
- 技术
tags: 
- MATLAB
---

MATLAB的edge函数只能处理灰度图或者黑白图（或者说imread之后得到的矩阵是个二维矩阵），而对RGB的真彩图是没法处理的，当然，也可以通过把RGB图先转化成灰度图再进行边缘检测。edge函数的输入参数就是imread之后的二维矩阵，和指示的字符串和限定方法的一些数值参数。edge函数支持六种经典边缘检测方法，分别是`Sobel Method`、`Prewitt Method`、`Roberts Method`、`Laplacian of Gaussian Method`、`Zero-cross Method`和`Canny Method`。至于具体算法，我就不清楚了，这里只给出matlab的实现方法：

源程序如下 

```
f=imread('1.jpg');
f=rgb2gray(f);
%转化成灰度图 
f=im2double(f);
%函数im2double 
将其值归一化到0～1之间 
%使用垂直Sobcl箅子．自动选择阈值 
[VSFAT Threshold]=edge(f, 'sobel','vertical');
%边缘探测 
figure,imshow(f),title(' 原始图像，');
%显示原始图像 
figure,imshow(VSFAT),title( '垂直图像边缘检测');
%显示边缘探测图像 
%使用水平和垂直Sobel算子，自动选择阈值 
SFST=edge(f,'sobel',Threshold);
figure,imshow(SFST),title('水平和垂直图像边缘检测');
%显示边缘探测图像 
%使用指定45度角Sobel算子滤波器，指定阂值 
s45=[-2 -1 0;
    -1 0 1;
    0 1 2];
SFST45=imfilter(f,s45,'replicate');
%功能：对任意类型数组或多维图像进行滤波。 
SFST45=SFST45>=Threshold;
figure,imshow(SFST45),title('45度角图像边缘检测') ;
%显示边缘探测图像 
```

 运行的结果图： 

![][1]

![][2]

![][3]

![][4]


[1]: https://ww3.sinaimg.cn/large/006tNc79gw1f511k9cucfj30nj0iqwg8

[2]: https://ww1.sinaimg.cn/large/006tNc79gw1f511kfyl0kj30nk0ictaf

[3]: https://ww4.sinaimg.cn/large/006tNc79gw1f511ko2cm8j30nh0ibgna

[4]: https://ww3.sinaimg.cn/large/006tNc79gw1f511kx0hplj30ng0ia79g
