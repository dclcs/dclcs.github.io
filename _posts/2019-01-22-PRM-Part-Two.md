---
title: "1.2 PRML Introduction Probability Theory Part Two"
author: dcl
categoies: PRML
CreateTime: 2019-01-22 17:23:3 +0800
date: 2019-01-22 17:23:3 +0800
---
1.2 PRML Introduction Probability Theory Part Two
<!--more-->

### 贝叶斯概率
- 贝叶斯理论是将先验概率(`prior probability`)转换成后验概率(`posterior probability`)，通过包括由观察数据得到的证据(`evidence`)
- 以曲线拟合作为例子
    - 首先，在观察数据之前，对$\mathbf w$作为假设已知，并且$\bf w$服从先验概率$p(\bf w)$
    - 观察数据的影响可以有条件概率$p(\mathbf w \mid \mathcal D)$,其中$\mathcal D$是观察数据且$\mathcal D = \{t_1 ... t_N\}$
    - $p(\mathbf w \mid \mathcal D) = \frac{p(\mathcal D \mid \mathbf w)p(\mathbf w)}{p(\mathcal D)}$,其中$p(\mathbf w \mid \mathcal D)$为后验概率，并且$p(\mathcal D \mid \mathbf w)$为似然函数(`likelihood function`)
    - `posterior` $\sim$ `likelihood` $\times$ `prior`


### 高斯分布
- 单一变量
    - $\mathcal N(x\mid \mu, \sigma^2) = \frac{1}{(2\pi\sigma^2)^{\frac12}}exp\{-\frac{1}{2\sigma^2}(x-\mu)^2\}$,$\mu$为均值,$\sigma^2$为方差,将$\frac{1}{\sigma^2}$记为$\beta$
    - $\int^{\infty}_{-\infty}\mathcal N(x\mid \mu, \sigma^2)dx = 1$
    - $\mathbb E[x] = \int^{\infty}_{-\infty}\mathcal N(x\mid \mu, \sigma^2)xdx = \mu$
    - $\mathbb E[x^2] = \int^{\infty}_{-\infty}\mathcal N(x\mid \mu, \sigma^2)x^2dx = \mu^2 + \sigma^2$
    - $var[x] = \mathbb E[x^2] - \mathbb E[x]^2 = \sigma^2$
- 多个变量(用向量表示)
    - $\mathcal N(\mathbf x \mid \mathbf \mu, \mathbf \Sigma) = \frac{1}{(2\pi)^{\frac{D}{2}}}\frac{1}{\mid \mathbf \Sigma\mid^{\frac{1}{2}}}exp\{-\frac12(\mathbf x - \mathbf \mu)^T\mathbf \Sigma^{-1}(\mathbf x - \mathbf \mu)\}$,其中$\bf \mu$为$D$维向量的均值，$\bf \Sigma$为$D\times D$的矩阵为协方差,$\mid \mathbf \Sigma \mid$为矩阵的行列式
- 使用观察到的数据区决定概率分布中的参数的一个通用表准是<b>最大化似然函数</b>
- 假设每个$x_i$独立同分布(`iid`)
    - $p(\mathbf x \mid \mu, \sigma^2) = \prod_{n=1}^N\mathcal N(x_n \mid \mu, \sigma^2)$，用另外的形式表达写成,$lnp(\mathbf x \mid \mu, \sigma^2) = -\frac{1}{2\sigma^2}\sum_{n=1}^N(x_n - \mu)^2 - \frac{N}{2}ln\sigma^2 - \frac{N}{2}ln(2\pi)$
    - 最大化似然函数，那么可以得到$\mu_{ML} = \frac1N\sum_{n=1}^Nx_n$(样本均值),同理,$\sigma^2_{ML} = \frac1N\sum_{n=1}^N(x_n - \mu_{ML})^2$（样本方差）

### 贝叶斯曲线拟合
- 在曲线拟合问题中，给定$\bf w$和$\bf t$,我们的目标是给定一个新的$x$预测出$t$。也可以认为是，我们想估计分布$p(t\mid x, \mathbf x, \mathbf t)$.
- 这里我们假设$\alpha$和$\beta$事先给定，$p(t\mid x, \mathbf x, \mathbf t) = \int p(t\mid x, \mathbf w)p(\mathbf w\mid \mathbf x, \mathbf t)d\mathbf w$
    - 其中， $p(t\mid x, \mathbf w)$是$p(t\mid x, \mathbf w, \beta^{-1}) = \mathcal N(t\mid y(x, \mathbf w), \beta^{-1})$的简化形式