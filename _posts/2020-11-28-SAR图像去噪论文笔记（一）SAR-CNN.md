---
layout:     post
title:      SAR图像去噪论文笔记（一）SAR-CNN
subtitle:   
date:       2020-11-28
author:     HSH
header-img: img/OIP.png
catalog: true
---

论文链接：[SAR IMAGE DESPECKLING THROUGH CONVOLUTIONAL NEURAL NETWORKS](https://arxiv.org/pdf/1704.00275.pdf)

这篇论文发表是在2017年，算是比较古老了，指标与最新的论文相去甚远，但是作为初学者，我认为仍然有值得学习的地方，至少在一些基础问题的处理上大家都是一样的。

## 简介

在这之前的方法：小波收缩、稀疏表示和非局部滤波，都依赖于图像和噪声详细的统计模型，但是对于不同的传感器、不同的视角等多种因素的影响造成数据之间的差异，是模型的稳定性降低

使用机器学习方法避免对噪声模式的复杂建模，直接学习数据的隐式表达，对于同类型的新数据可以方便地去除噪声

在数据有限的情况下通过**残差学习**(residual learning)保证更快地收敛

本文的创新在于率先尝试了**深度学习**的方法，并且对比传统的等传统算法进步了很多，在网络结构和损失函数的设计上也别有用心

此外对于乘性噪声的处理和ad hoc建立数据的方法值得斟酌

## 网络结构

模仿《Be-yond a Gaussian Denoiser: Residual Learning of Deep CNNfor Image Denoising》这篇论文，17层卷积层，每层有64个3×3的卷积核，其中还有批规范化处理。

![img](https://i.bmp.ovh/imgs/2020/11/5efca1821b180aaa.png)

为了处理乘性的噪声，对图像先做对数变换，转化成加性噪声，再有指数变换回去。

## 损失函数设计

![](http://latex.codecogs.com/gif.latex?L(\theta)=\sum_{i=1}^N {\rm log[cosh}(R_{\theta}({\rm log}\ y_i)+c-{\rm log}\frac{y_i}{x_i})])

其中x_i表示干净图像，y_i表示有噪声的图像，R_θ(log  y_i)代表CNN的输出，c是对数噪声的非零均值。这样的设计或许比L2范数的损失函数要好一些。

通过损失函数还可以看出，训练的目标不是干净图像，而是噪声图像，干净图像由原图像减去噪声图像再做指数变换得到。这也就是作者采用的**残差学习**（residual learning），在数据比较少的时候可以有效地加快收敛速度。

## 数据生成策略：ad hoc方法

假设同一地点有很多不同时间的图像，干净图像通过对这些时间图像取平均得到，并且只保留时间上比变化不大的区域。（化整为零的思想，c的来由）这样就有了噪声图片和对应的干净版本作为ground truth用于训练，于是就有了下面完整的训练流程图：

![img](https://i.bmp.ovh/imgs/2020/11/f90ecbe38ac7db26.png)

## 测试

分别对人工合成的类SAR数据和真实SAR数据做了实验。

对于合成数据，本身有ground truth，采用PSNR（峰值信噪比）和SSIM（结构相似性）比较重建图像与原始图像的相似程度，评估去噪效果。

![](https://i.bmp.ovh/imgs/2020/11/bafffb2c26c61c04.png)

对于真实SAR数据，每组图片有25个时间分量，可以使用上文提到的ad hoc方法，可见事先对数据集的研究也是很重要的。有ENL(equivalent number of looks，等效视数)和*αβ*率。

![](https://i.bmp.ovh/imgs/2020/11/20721114eb6be71b.png)

## 总结

优点：

+ 使用残差学习提高训练速度
+ log-exp方式处理乘性噪声
+ 损失函数的设计
+ ad hoc生成干净图像的方法

缺点：

+ 没有详细说明对SAR图像的针对性设计（或者没有考虑）
+ 数据生成策略的普适性不强，满足条件的数据集太少
+ 测试指标需要进一步研究