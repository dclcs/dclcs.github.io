---
title: "PRML Course Learning"
author: dcl
categoies: PRML
CreateTime: 2019-03-18 17:23:3 +0800
date: 2019-03-18 17:23:3 +0800
---
PRML Course 学习

# Introduction To Machine Learning

## 机器学习：What，Why，and How？

### What

- 通过经验自动改善算法的表现
- 通常意味着需要手动定义一个模型，并且用数据拟合模型参数

### Why

- 现实世界很复杂以至于很难手动找到解决方案

### 曲线拟合：回归和模型选择

- 多项式曲线拟合
    - Loss Function
    - overfitting
        - Regularization
        - DataSet Size
    - Validation Set
        - Cross-validation  
- 总结
    - 我们需要模型对新数据有好的泛化能力
        - 在训练集上训练模型
        - 在测试集上测量模型的表现能力
    - 选择什么样的模型？
        - 训练损失较低的
            - 但是不能选取最低的训练损失的模型
        - 使用验证集
        - 交叉验证
        - 使用正则化
        - 得到更多的数据

### 决策理论： ML ， LOSS FUNCTIOn， MAP？

- 给定一个样本$\mathbb x$，决定`class(`$C_k$`)`是来自哪个类
    - Maximum Likelihood
    - Minimum Loss/Cost(e.g misclassication rate) 
    - Maximum Aposteriori

- Decision: Maximum Likelihood
    - 从训练数据中得到统计信息：$p(x, t)$或者$p(x\mid C_k)$
    - 确定册数输入$x$的最优值$t$： $t = {argmax}_k\{ p(x \mid C_j)\}$，其中$p(x\mid C_k)$为似然（`likelihood`）

- Decision: Minimum Misclassication Rate
    - $p(mistake)=p(x \in \mathcal R_1, \mathcal C_2) + p(x \in \mathcal R_2, \mathcal C_1) = \int_{\mathcal R_1}p(x, \mathcal C_2)dx + \int_{\mathcal R_2}p(x, \mathcal C_1)dx$
    - $p(mistake) = \sum_k \sum_j \int_{\mathcal R_j}p(x, \mathcal C_k)dx$
!['img'](../images\prml_1.png)

- Decision: Minimum Loss/Cost
    - 错误分类率： $\mathcal R = {argmin}_{\{\mathcal R_i \mid i \in \{1,..., K\}\}}\{\sum_k\sum_j\mathcal L(\mathcal R_j, \mathcal C_k)\}$
    - 带有权重的损失函数：$\mathcal R = {argmin}_{\{\mathcal R_i \mid i \in \{1,..., K\}\}}\{\sum_k\sum_j$<font color="r">$\mathbf W_{j,k}$</font>$\mathcal L(\mathcal R_j, \mathcal C_k)\}$

- Decision: Maximum Aposteriori (MAP)
    - 贝叶斯理论： $p\{A \mid B\} = \frac{p\{B \mid A\}P\{A\}}{p\{B\}}$


### 概率论

- 硬币模型
    - 假设投硬币服从bernoulli ： $p(h) = \mu, p(t) = 1 - \mu$，且每次投硬币相互独立
    - 给出数据集：$\mathcal D = \{x_1, x_2,...x_N\}$,heads：$x_i = 1$, tails: $x_i = 0$
        - 数据的`likelihood`为$p(\mathcal D \mid \mu) = \prod^N_{n=1}p(x_n \mid \mu) = \prod_{n=1}^{N}\mu ^{x_n}(1 - \mu)^{1 - x_n}$
    - 最大相似估计
        - 选择$\mu$来最大化`likelihood`：$\mu_{ML} = argmax_{\mu}p(\mathcal D \mid \mu)$
        - 或者：$\mu_{ML} = argmax_{\mu}lnp(\mathcal D \mid \mu)$
        - `Log-likelihood`: $lnp(\mathcal D \mid \mu) = \sum_{n=1}^Nx_nln \mu + (1-x_n)ln(1-\mu)$
        - 求导，令值为0：$\frac{d}{d \mu}lnp(\mathcal D \mid \mu) = \sum_{n=1}^Nx_n\frac{1}{\mu} - (1-x_n)\frac{1}{1 - \mu} = \frac{1}{h} - \frac{1}{1 - \mu}t \Rightarrow \mu = \frac{h}{t + h}$
    - 贝叶斯学习:
        - $\mathbf P(\mu \mid \mathcal D) = \frac{P(\mathcal D \mid \mu)P(\mu)}{P(\mathcal D)}$
        - $P(\mu \mid \mathcal D) = P(\mathcal D \mid \mu)P(\mu) = \prod_{n=1}^N\mu^{x_n}(1-\mu)^{1-x_n}\mu^{a-1}(1-\mu)^{b-1} = \mu^h(1-\mu)^t\mu^{a-1}(1-\mu)^{b-1}=\mu{h + a - 1}(1 - \mu)^{t + b -1}$
        - $\mu_{MAP} = argmax_{\mu}P(\mu \mid \mathcal D)$ 为点估计