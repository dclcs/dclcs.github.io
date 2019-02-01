---
title: "【Translate】Learning a Similarity Metric Discriminatively, with Application to Face Verification"
author: dcl
CreateTime: 2019-02-01 17:23:3 +0800
date: 2019-02-01 17:23:3 +0800
categoies: dl
---

翻译：Learning a Similarity Metric Discriminatively, with Application to Face Verification
<!--more-->
# 1.Introduction
传统的方法使用对抗的方法（discriminative methods）解决识别问题，例如神经网络或者SVM，通常需要所有的类别（categories）提前知道。这些方法同样需要所有类别的训练例子都可以被使用。更重要的是，这些方法本质上受限于相当少的类别个数。这些方法不适合那些类别比较大的应用，和那些在训练过程中只知道类别的一部分子集的应用。这些应用包括人脸识别和人脸认证：类别的数量可以是几百或者上千，然鹅只有很少的例子对于每个类别。解决这类问题的常见的方法是基于距离（distanced-based method）的方法，基于距离的方式通过计算两个模式（two patterns）或者一个的相似矩阵来进行认证或者识别或者计算 a library of stored prototypes.另外一种常见的作法是降维操作（reduced-dimension space),这个方法中一个类别的训练只需要很少的样本数。为了应用对抗的学习技巧到这类问题，我们必须设计出一个方法，这个方法能够从足够的数据中提取有关问题的信息，但是不需要每个类别的精准的信息。<br/>
本文提出的解决方法是从数据在学习相似矩阵(`learn a similarity metric from data`)。这个相似矩阵能够用来比较或者匹配之前没有见过的类别中样本（例如：在训练过程中没有的人脸）。我们提出一个新的对抗训练方法，用来寻来你相似矩阵。这个方法能够应用到类别的数量非常大或者类别中的例子不够再训练过程中的识别问题。<br/>
这个方法的核心思想就是寻找一个函数，这个函数将输入模式（input patterns）映射到目标空间（target space），并且目标空间中的单一距离（simple distance）（欧拉距离）近似于输入空间的“语义”距离。更准确的来说，给定一簇函数（a family of functions）$G_W(X)$（其中$W$是参数）,我们要求寻找一个参数$W$，并且如果$X_1,X_2$属于相似的类别，相似矩阵$E_W(X_1,X_2) = \mid\mid G_W(X_1) - G_W(X_2) \mid\mid$会很小，相反如果属于不同的类别会很大。这个系统从训练集中匹配进行训练（the system is trained on pairs of patterns taken from a trainning set)。损失函数在$X_1$和$X_2$属于相似类别时，最小化$E_W(X_1,X_2)$并且在$X_1$和$X_2$属于不同类别时，最大化$E_W(X_1, X_2)$。对于不同的$W$,$G_W(X)$没有做任何前提假设。因为对于同样的参数$W$,同样的函数$G$被用来处理一样的输入，相似矩阵时对称的。这被称作孪生结构(`siamese architecture`)<br/>
为了使用这种方法去搭建人脸识别系统，我们首先训练模型产生输出向量，这些向量在处理来自同一个人的照片会很接近，处理来自不同人的照片会很远。这个模型能够被用做相似矩阵在一个新的人脸的照片。<br/>
这个方法提出的一个非常重要的观点是我们用完全的自由在选择$G_W(X)$。尤其是我们将会使用那些设计好去提取输入的几何失真的架构，例如卷积神经网络。产生的相似矩阵将会非常健全产生非常少的区别。<br/>
因为目标空间的维度非常小并且自然距离对于不相关的输入是不变的，我们能够轻松的从非常小的样本量中估计每个新的类别的概率模型。
## 1.1 之前的工作
