---
title: "dl-with-python Chapter3"
author: dcl
categoies: CG
CreateTime: 2019-01-14 17:23:3 +0800
---

deep learning with python

<!--more-->

## 神经网络
### 3.2 感知机
- 将$y = \begin{cases} 0 & (b+w_1x_1 + w_2x_2 \le 0) \\\ 1 & (b+w_1x_1+w_2x_2 \gt 0) \end{cases}$改写成$y=h(b+w_1x_1+w_2x_2)$，其中$h(x) = \begin{cases} 0 & (x \le 0) \\\ 1 & (x \gt 0)\end{cases}$,称$h(x)$为激活函数/阶跃函数。
#### 3.2.1 sigmoid函数
- sigmoid function ： $h(x) = \frac{1}{1 + exp(-x)}$
- !['sigmoid'](../images\sigmoid.png)
#### 3.2.2 阶跃函数的实现
- 简单的数学表达式:$h(x) = \begin{cases} 0 & (x \le 0) \\\ 1 & (x \gt 0)\end{cases}$
#### 3.2.3 阶跃函数的图形
!['step'](../images\step.png)
#### 3.2.5 比较
- sigmoid函数平滑的曲线
- 当输入信号为重要信息时，阶跃函数和sigmoid函数都会输出较大的值
- 当输入信号为不重要信息时，两者都输出较小的值
#### 3.2.6 非线性函数
- 神经网络的激活函数必须使用非线性函数，因为使用线性函数的话，加深神经网络的层数没有意义
#### 3.2.7 ReLU 函数
- $h(x) = \begin{cases} x & (x > 0) \\\ 1 & (x \le 0)\end{cases}$
- !['relu'](../images\relu.png)

### 3.3 多维数组的运算

### 3.4 三层神经网络的实现
- !['3-layer'](../images\3-layers.png)
#### 3.4.1 符号确认
-  <b>$w^{(1)}_{12}$</b>其中"$(1)$"表示权重和神经元的层号；右下角"$12$"分别表示后一次的神经元和前一次神经元的索引号。
- ![''](../images\detail-3.png)
#### 3.4.2 各层之间的传递
- ![''](../images\layer3.png)
- $a_1^{(1)} = w_{11}^{(1)}x_1 + w_{12}^{(1)}x_2 + b^{(1)}_1$
- $a_2^{(1)} = w_{21}^{(1)}x_1 + w_{22}^{(1)}x_2 + b^{(1)}_2$
- $\bf A^{(1)} = XW^{(1)} + B^{(1)}$,其中$\bf A^{(1)} = \begin{pmatrix} a_1^{(1)} & a_2^{(1)} & a_3^{(1)} & a_4^{(1)}\end{pmatrix}$，$\bf X = \begin{pmatrix} x_1 & x_2\end{pmatrix}$，$B^{(1)} = \begin{pmatrix} b_1^{(1)} & b_2^{(1)} & b_3^{(1)}\end{pmatrix}$，$\bf W^{(1)} = \begin{pmatrix} w_{11}^{(1)} & w_{21}^{(1)} & w_{31}^{(1)} \\\ w_{12}^{(1)} & w_{22}^{(1)} & w_{32}^{(1)} \end{pmatrix}$
- 输出层的激活函数用$\sigma()$代替

### 3.5 输出层的设计
- 一般而言，回归问题用恒等函数， 分类问题用softmax喊
#### 3.5.1 恒等函数与softmax函数
- 恒等函数会将输入按原样输出
- softmax函数: $y_k = \frac {exp(a_k)}{\sum_{i=1}^n exp(a_i)}$
#### 3.5.2 softmax的改进
- $y_k = \frac {exp(a_k)}{\sum_{i=1}^n exp(a_i)} = \frac {Cexp(a_k)}{C\sum_{i=1}^n exp(a_i)} = \frac {exp(a_k + logC)}{\sum_{i=1}^n exp(a_i + logC)}= \frac {exp(a_k + C^{'})}{\sum_{i=1}^n exp(a_i + C^{'})}$


[code](https://github.com/dclcs/deep_learning_with_python_code/blob/master/deep_learning_with_python_code_ch3.ipynb)