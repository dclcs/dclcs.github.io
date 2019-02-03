---
title: "【Translate】Learning to Compare Image Patches via Convolutional Neural Networks"
author: dcl
CreateTime: 2019-02-03 17:23:3 +0800
date: 2019-02-03 17:23:3 +0800
categoies: dl
---

翻译:<br>
Learning to Compare Image Patches via Convolutional Neural Networks
<!--more-->

### Abstract
这篇文章我们展示了如何直接从图片信息（例如：不需要存储人为设计的特征）产生一个相似函数，这个相似函数是用来解决比较两张图片的问题，这个问题是很多cv问题的基本问题。为了加密这个函数，我们采取了一个基于卷积网络的模型，这个用变化的图片进行训练。训练完成后，我们探索和学校多种神经网络结构，这些结构我们应用于这项工作。我们展示了这个方法，这个方法能优于几个问题和一些基准数据库的`state-of-art`。<br>

### 1. Introduction
