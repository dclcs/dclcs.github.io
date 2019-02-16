---
title: "【Summary】"
author: dcl
categoies: PRML
CreateTime: 2019-02-16 11:01:12
date: 2019-02-16 11:01:19
---
研究一年级上学期总结
<!--more-->
## 工作内容
### 一、SMPL
### 二、拟合SMPL
- 目的：为了使用我们自己扫描得人体
- 目前的阶段：
    - 替换原始模板中的`mesh`的点
    - 替换原始模板中人体`mesh`的关节点的坐标
    - 替换原始模板中人体`mesh`的权重
        - `mesh`的权重是每个点对每个关节点的权重值
- 目前未解决的问题
    - `mesh`的权重
    - 使用过的方法
        - [`pinocchio `](https://github.com/elrond79/Pinocchio)采用的方法
            - 该方法可以有效的计算每个骨骼
            - 但是我们需要的是关节点的权重
    - 即将使用的方法
        -  [`pinocchio `](https://github.com/elrond79/Pinocchio)中既然可以计算每个骨骼点的权重，也用到了`lbs`(`linear blend skinning`)，那么应该有每个点对关节点权重的计算
        - 阅读 [`pinocchio `](https://github.com/elrond79/Pinocchio)的代码找到如何计算关节点的权重的代码`snippets`
- 关于`lbs`的一些问题
    - [`pinocchio `](https://github.com/elrond79/Pinocchio)中关于`lbs`的计算是每个点到骨骼的权重
    - 相反的`SMPL`中`lbs`是每个点到关节点的权重
    - 如何处理这些问题是一个难题

<!-- ### 三、 -->