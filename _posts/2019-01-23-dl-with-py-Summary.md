---
title: "【deep learning】dl-with-python-Summary"
author: dcl
CreateTime: 2019-01-19 17:23:3 +0800
date: 2019-01-19 17:23:3 +0800
categoies: dl
---

Summary of Chapter 1-5
DataSet : Mnist
Architecture: Two Layer network, Two Affine ,Activation: Relu and the last layer is softmax, loss is cross-entropy
<!--more-->

### 目标
<b>用两层网络实现</b>
### 架构
- LayerOne    :   `Input([图片展开向量], )`<br>
    - Weights: 
    - Bais
    - Activation: `Relu`<br>
- LayerTwo
    - Weights: 
    - Bais
    - Activation : `Relu`
- Output
    - Softmax
- Loss
    - crossentropy
### Details
#### 全连接层
- forward : $Y = WX + b$
- backward : 
    - 传递参数：`out`$=\frac{dL}{dY}$<br>
$\frac{dL}{dX} = \frac{dL}{dY} * \frac{dY}{dX} = dout * W^T$<br>
$\frac{dL}{dW} = \frac{dL}{dY} * \frac{dY}{dW} = X^T * dout$<br>
$\frac{dL}{db} = \frac{dL}{dY} * \frac{dY}{db} = dout * 1$<br>
#### ReLu层
- $y =\begin{cases} x, & x \ge 0 \\\ 0 , & x \lt 0\end{cases}$
- $\frac{\partial y}{\partial x} = \begin{cases} 1, & x \ge 0 \\\ 0 , & x \lt 0\end{cases}$
- `mask = x <= 0` 
- forward : `out[mask] = 0`
- backward : `dout[mask] = 0`

#### Softmax With CrossEntropy 层
- softmax:
    - $y_k = \frac {exp(a_k)}{\sum_{i=1}^n exp(a_i)}$
        - 改进：$y_k = \frac {exp(a_k)}{\sum_{i=1}^n exp(a_i)} = \frac {Cexp(a_k)}{C\sum_{i=1}^n exp(a_i)} = \frac {exp(a_k + logC)}{\sum_{i=1}^n exp(a_i + logC)}= \frac {exp(a_k + C^{'})}{\sum_{i=1}^n exp(a_i + C^{'})}$
- crossentropy:
    - $\mathbf E = -\sum_kt_klogy_k$,$y_k$是正确输出，$t_k$是正确理解标签，并且$t_k$中只有正确解标签为1，其他均为0（one-hot表示）