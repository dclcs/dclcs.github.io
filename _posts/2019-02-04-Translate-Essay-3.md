---
title: "【Translate】Siamese Network Features for Image Matching"
author: dcl
CreateTime: 2019-02-04 17:23:3 +0800
date: 2019-02-04 17:23:3 +0800
categoies: dl
---

翻译:<br>
Siamese Network Features for Image Matching
<!--more-->

### Abstract
通过一个大型数据库中找到匹配的图片在计算机视觉应用中扮演着重要作用，例如`SfM`(`structure-from-motion`)、多视角的`3D`重建（`multi-view 3D reconstruction`）、`image retrieval`和`image-based localisation`。本文中，我们提出通过表达基于特征向量（`feature vectors`）的神经网络来表达匹配和未匹配的图片对，其中的相似度用欧拉距离来测量。特征向量神经网络中学习获得，神经网络通过匹配和非匹配的图片对的标签来学校，神经网络构造一个基于孪生网络的对比的损失函数（`contrastive loss function`）。以前，孪生网络应用在人脸验证和匹配局部照片，但尚未应用于通用的图片恢复和整个图片的匹配。我们的实验结果显示相比通过图片分类网络得到的基线特征来说我们提出的特征检测方法的表现较好。特征获取的较好并且改善图片的新的`landmarks`的匹配，这些`landmarks`在训练过程并未得到。这说明训练数据中匹配和未匹配的标签时不完美的。考虑到图像检索应用，结果是有希望的，并且通过利用具有更准确的地面实况标签的更多训练图像对，存在进一步改进的潜力。

### 1.Introduction
目前