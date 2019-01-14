---
layout: post
title: "dl-with-python Chapter3"
description: "dl"
category: dl
tags: [dl] 
---

{% include JB/setup %}

## 神经网络
### 3.2 感知机
- 将$y = \begin{cases} 0 & (b+w_1x_1 + w_2x_2 \le 0) \\\ 1 & (b+w_1x_1+w_2x_2 \gt 0) \end{cases}$改写成$y=h(b+w_1x_1+w_2x_2)$，其中$h(x) = \begin{cases} 0 & (x \le 0) \\ 1 & (x \gt 0)\end{cases}$,称$h(x)$为激活函数/阶跃函数。
#### 3.2.1 sigmoid函数
- sigmoid function ： $h(x) = \frac{1}{1 + exp(-x)}$
- !['sigmoid'](../images\sigmoid.png)
#### 3.2.2 阶跃函数的实现
- 简单的数学表达式:$h(x) = \begin{cases} 0 & (x \le 0) \\ 1 & (x \gt 0)\end{cases}$
#### 3.2.3 阶跃函数的图形
!['step'](../images\step.png)
#### 3.2.5 比较
- sigmoid函数平滑的曲线
- 当输入信号为重要信息时，阶跃函数和sigmoid函数都会输出较大的值
- 当输入信号为不重要信息时，两者都输出较小的值
#### 3.2.6 非线性函数
- 神经网络的激活函数必须使用非线性函数，因为使用线性函数的话，加深神经网络的层数没有意义
#### 3.2.7 ReLU 函数
- $h(x) = \begin{cases} x & (x > 0) \\ 1 & (x \le 0)\end{cases}$
- !['relu'](../images\relu.png)