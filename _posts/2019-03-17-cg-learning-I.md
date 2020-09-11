---
title: "Image Conv and Edge Detection"
author: dcl
categoies: CG
CreateTime: 2019-03-17 17:23:3 +0800
date: 2019-03-17 17:23:3 +0800
---
Computer Vision & Computational Photography 学习
<!--more-->

# Linear Filter

## Image filtering

- $g(i,j) = \sum_{k,l}f(i+k, j+l)h(k,l)$
    - $g$为`output Image`
    - $f$为`Input Image`
    - $h$为`kernel Image`
    - `input`和`kernel`对应相乘相加

!['img'](../images\cg_1.png)

## Conv

- $g(i,j) = \sum_{k,l}f(i-k, j-l)h(k,l) = \sum_{k,l}f(k,l)h(i-k,j-l) = f * h$
    - `input`和翻转后的`kernel`对应相乘相加
    - 卷积具有交换:$I \bigotimes f = f \bigotimes I$
        - Proof：$g[m,n] = I \bigotimes f = \sum_{k, l}I(m-k, n-l) * f(k, l)$
        - let $k^{'} = m - k, l^{'} = n - l$；then $k = m - k^{'}, l = n - l^{'}$
        - $g[m, n] = \sum_{k^{'}, l^{'}}I(k^{'}, l^{'}) * f(m - k^{'}, n - l^{'}) = f \bigotimes I$
    - 卷积的输出的Size

## 填塞（边界效应）

- 角点处的像素会变黑，因为卷积核超出原始图像边界时，原始图像边界外的部分被认为有效的，并且用0填塞
- 采取的措施：
    - 0填塞
    - 常数填塞
    - 夹取填塞
    - （圆形）重叠填塞（重复或者平铺）
    - 镜像填塞
    - 延长

!['img'](../images\cg_2.png)