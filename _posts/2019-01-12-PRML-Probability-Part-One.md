---
title: "1.2 PRML Introduction Probaility Theory (I)"
author: dcl
categoies: PRML
CreateTime: 2019-01-12 17:23:3 +0800
date: 2019-01-12 17:23:3 +0800
---

PRML : 1.2 PRML Introduction Probaility Theory (I)
<!--more-->

### Rules of Probability
$$sum \ \ rule: p(X) = \sum_Yp(X,Y) \\ product \ \ rule: p(X,Y) = p(Y\mid X)p(X)$$

其中， $p(X,Y)$为联合概率 ，"X和Y的概率"；<br>
$p(Y\mid X)$为条件概率，"在X给定的条件下， Y的概率"<br>
$p(X)$为边缘概率， "X的概率"<br>

### Bayes' theorem
$$\because \ \  p(X,Y) = p(Y,X) \\
p(X,Y) = p(Y\mid X)p(X) \\ p(Y ,X) = p(X \mid Y)p(Y) \\
\therefore \ \  p(Y\mid X) = \frac {p(X \mid Y)p(Y)}{p(X)}$$

使用`sum rule`得到$p(X) = \sum_Yp(X\mid Y)p(Y)$
原文：`We can view the denominator in Bayes' theorem as being the normalization constant required to ensure that the sum of the conditional probability on the lef-hand side of `$p(Y\mid X) = \frac {p(X \mid Y)p(Y)}{p(X)}$`over all values of Y equals one.`


### 概率密度（连续变量）
- $p(x \in (a, b)) = \int_a^bp(x)dx$表示的x的概率是a到b之前的面积
- 两个条件：
    - $p(x) \ge 0$
    - $\int^{\infty}_{-\infty}p(x)dx = 1$
- 考虑x变量的变化，$x = g(y)$, 则$f(x) = \overline f(y) = f(g(y))$;$x$对应的概率m密度为$p_x(x)$,$y$对应的概率密度为$p_y(y)$，$p_x(x)\delta x \simeq p_y(y)\delta y$。<br>

$$
p_y(y) = p_x(x)\mid\frac{dx}{dy} \mid = p_x(g(y))\mid g\prime(y)\mid
$$
- 根据积累分布函数(`cumulative distribution function`)x的概率存在于区间$(-\infty ,z)$,$\mathbf P(z) = \int_{-\infty}^zp(x)dx$,满足$\mathbf P\prime(z) = p(x)$
- 多个连续的变量$x_1...x_D$，能够记成一个向量$\mathbf x$,联合的概率密度为$p(\mathbf x) = p(x_1,x_2,...,x_D)$

$$
p(\mathbf x) \ge 0 \\
\int p(\mathbf x)d\mathbf x = 1
$$

- 如果$x$是一个离散的变量，那么$p(x)$有时被称为概率质量函数(`probability mass function`)
- `sum 、product and Bayes' theorem`同样适用于概率密度函数

$$
p(x) = \int p(x,y)dy \\
p(x, y) = p(y \mid x)p(x)
$$

### 期望和方差
- 在给定概率分布$p(x)$下的某个函数$f(x)$的平均值为$f(x)$的期望<br>

$$\mathbb E = \sum_xp(x)f(x) \\ \mathbb E[f] = \int p(x)f(x)dx \\ \mathbb E[f] \simeq \frac{1}{N}\sum_{n=1}^Nf(x_n) (N \to \infty)$$
- 多变量期望

$$\mathbb E_x[f(x,y)]$$
$$\mathbb E[f\mid y] = \sum_x p(x\mid y)f(x)$$

- $f(x)$方差的定义：$var[f] = \mathbb E[(f(x) - \mathbb E[f(x)])^2]$

$$var[f] = \mathbb E[f(x)^2] - \mathbb E[f(x)]^2 \\ var[f] = \mathbb E[x^2] = \mathbb E[x]^2$$

- 协方差：

$$
cov[x,y] = \mathbb E_{x,y}[\{ x - \mathbb E[x]\} \{ y - \mathbb E[y]\}] = \mathbb E_{x,y}[xy] - \mathbb E[x]\mathbb E[y] \\ 
 \ \\ cov[\mathbf x,\mathbf y] = \mathbb E_{\mathbf x,\mathbf y}[\{ \mathbf x - \mathbb E[\mathbf x]\} \{ \mathbf y^T - \mathbb E[\mathbf y^T]\}] = \mathbb E_{x,y}[\mathbf x\mathbf y^T] - \mathbb E[\mathbf x]\mathbb E[\mathbf y^T]
$$