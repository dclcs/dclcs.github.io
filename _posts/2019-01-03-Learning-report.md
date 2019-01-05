---
layout: post
title: "2019/01/05图形深度学习Introduction"
description: "图形深度学习"
category: 图形深度学习
tags: [图形深度学习]
---

{% include JB/setup %}

### `1.` CG中的表达
- 图片 像素
- Volume（体） 体素
- Meshes    点、边、面
- 动画  骨骼、
- 点云
- 物理仿真


### `2.` 计算机图形中的问题
- Analysis

    - 特征检测(图形特征和point features)
        
        $\R^{m\times m} \to \Z$
    - 去躁,光滑。。。

        $\R^{m\times m} \to \R^{m\times m}$
    - Embedding, Distance computation

        $\R^{m\times m, m\times m} \to \R^d$

- synthesis

    - 渲染

        $ \R^{m\times m} \to \R^{m\times m} $
    - 动画

        $\R^{3m \times t} \to \R^{3m}$
    - 物理仿真

        $\R^{3m \times t} \to \R^{3m}$
    
    - 产生模型

        $\R^d \to \R^{m \times m}$



### `3.` 目标:学会一个参数化函数

$$f_\theta : X \to Y$$

$\theta:$ 函数参数，$X:$ source domain(源空间), $Y:$ 目标空间, 这是需要学习到的


#### `例子`
- 图形分类

$$f_\theta: \R^{w\times h\times c} \to \{0, 1,2,..., k-1\}$$]

$w\times h\times c:$ 图形的维度，长、宽、通道；$k:$ 类别数

- 图形合成

$$f_\theta: \R^n \to \R^{w\times h\times c}$$
$n:$ latent variable count；$w\times h\times c:$ 图形的维度，长、宽、通道


### `4.` 数据驱动算法

- 监督算法

graph LR

    A-->B
    B-->C
    C-->D
    D-->A
