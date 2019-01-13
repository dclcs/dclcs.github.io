---
layout: post
title: "dl-with-python Chapter2"
description: "dl"
category: dl
tags: [dl]
---

{% include JB/setup %}


## 感知机
### 2.1 感知机是什么
- 接受多个信号，输出一个信号
- 0 代表“不传递信号”；1 代表“传递信号”
- !['da'](../images\per.png)
- $w_1、w_2$权重， $x_1、x_2$输入信号, $y$输出信号
- $(w_1x_1, w_2x_2)$为传递的信号的总和，只有这个总和超过某个界限值，$y$才输出1，这个界限值为`阈值`
- $y = \begin{cases} 0 , & {w_1x_1+w_2x_2 \le \theta} \\ 1 , & {w_1x_1+w_2x_2 \gt \theta}\end{cases}$

### 2.2 简单逻辑电路
- 与门
    - $(w_1, w_2, \theta) = (0.5, 0.5, 0.7)$
- 与非门和或门
    - 与非门：$(w_1, w_2, \theta) = (-0.5, -0.5, -0.7)$
    - 或门: $(w_1, w_2, \theta) = (0.5, 0.5, 0.2)$

### 2.3 感知机的实现
#### 2.3.1 简单实现
#### 2.3.2 导入权重和偏置
$y = \begin{cases}0,& {b + w_1x_1 + w_2x_2 \le \theta} \\ 1, & {b + w_1x_1 + w_2x_2 \gt \theta} \end{cases}$<br>
其中,$b= -\theta$
### 2.4 感知机的缺陷
- 与门<br>
!['and'](../images\and.jpg)
- 与非门<br>
!['nand'](../images\nand.jpg)
- 或门<br>
!['or'](../images\or.jpg)
- 异或门<br>
!['xor'](../images\xor.jpg)
    - 可以看出异或门不能用上面的方法区分开来

### 2.5 多层感知机
!['多层感知机'](../images\perce.png)