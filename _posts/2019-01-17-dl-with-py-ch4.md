---
layout: post
title: "dl-with-python Chapter4"
description: "dl"
category: dl
tags: [dl] 
---

{% include JB/setup %}


### 4.2 损失函数
- 损失函数表示神经网络性能的“恶劣”程度的指标。
#### 4.2.1 均方误差
- $\mathbf E = \frac 12 \sum_k(y_k - t_k)^2$,$y_k$表示神经网络的输出，$t_k$表示监督数据，$k$表示数据的维数
- 将正确理解标签表示为1， 其他标签表示为0的表示方法为<b>one-hot</b>表示
#### 4.2.2 交叉熵误差
- $\mathbf E = -\sum_kt_klogy_k$,$y_k$是正确输出，$t_k$是正确理解标签，并且$t_k$中只有正确解标签为1，其他均为0（one-hot表示）
#### 4.2.3 mini-batch 学习
- 前面的是针对单个数据的损失函数，所有数据的损失函数之和$\mathbf E = -\frac1N\sum_n\sum_kt_{nk}logy_{nk}$,这里数据有N个， $t_{nk}$表示第n个数据的第k个元素的值
- 从训练数据中选出一批数据（称为mini-batch），然后对每个mini-batch进行学习
#### 4.2.4 mini-batch版交叉熵误差??
### 4.3 数值微分
### 4.3.1
- $\frac{df(x)}{dx} = \lim_{h\to 0}\frac{f(x+h) - f(x)}{h}$
- 舍入误差：省略小数的精细部分而造成最终的误差
- 中心差分：以$x$为中心，计算左右的差分
- 利用微小的差分求导数的过程为数值微分。基于数学式的推导求导数的过程为解析微分，“真导数”

### 4.4 梯度
- $(\frac{\partial f}{\partial x_0}, \frac{\partial f}{\partial x_1})$偏微分的汇总的向量为梯度
#### 4.4.1 梯度法
- $\begin{cases} x_0 = x_0 - \eta \frac{\partial f}{\partial x_0} \\ x_1 = x_1 - \eta \frac{\partial f}{\partial x_1}\end{cases}$, $\eta$为学习率


### 4.5 学习算法实现
- mini-batch
- 计算梯度
- 更新参数
- 重复