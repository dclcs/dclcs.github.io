---
title: "1.1 PRML Introduction"
author: dcl
categoies: PRML
CreateTime: 2019-01-05 17:23:3 +0800
date: 2019-01-05 17:23:3 +0800
---
PRML
<!--more-->

### 1.1 多项式曲线拟合
$\mathbf x = (x_1, x_2, x_3....,x_N)^T: 训练集，N为\mathbf x的观测值\\ \mathbf t = (t_1, t_2, t_3....,t_N)^T: 对于\mathbf x的值$

多项式函数：$y(x, \mathbf w) = w_0 +w_1x +.. + w_Mx^M = \sum_{j=0}^Mw_jx^j$

损失函数:$E(\mathbf w) = \frac12\sum_{n=1}^N\{y(x_n, \mathbf w) - t_n\}^2$

平方根(RMS)：$E_{RMS} = \sqrt{2E(\mathbf w^*)/N}$

通过贝叶斯方法可以避免过拟合。

正则化：$\overline E(\mathbf w)=\frac12\sum_{n=1}^N(y(x_n,\mathbf w) - t_n)^2+\frac\lambda2\mid\mid\mathbf w\mid\mid^2$

其中$\mid\mid\mathbf w\mid\mid^2 = \mathbf w^T \mathbf w = w_0^2 + w_1^2+...+w_M^2$ , $\lambda$控制
