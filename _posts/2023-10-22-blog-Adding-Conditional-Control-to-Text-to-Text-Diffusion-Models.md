---
title: 'Adding Conditional Control to Text-to-Image Diffusion Models'
date: 2023-10-22
permalink: /posts/2023/10/22/Adding Conditional Control to Text-to-Image Diffusion Models/
tags:
  - DeepLearning
  - Diffusion Model
---

- **论文链接：**[https://arxiv.org/abs/2302.05543](https://arxiv.org/abs/2302.05543)
- **会议：** ICCV23 Best Paper
- **Keywords**： Deeplearning, Diffusion Model

---

# Abstract

提出了一种新的神经网络模型 ControlNet 支持额外添加控制条件来控制预训练的扩散模型。
ControlNet 以 end-to-end 的方式学习特定任务的
条件，即使训练的数据集很小(<50k)，也可以得到一个**稳健的模型**。
此外，训练一个 ControlNet 和微调一个扩散模型的速度一样快，在个人的设备上即可训练；如果训练资源足够，则该模型可以扩展到大量的(millions to billons)数据集中。
论文中指出，像稳定扩散这样的大型扩散模型可以用 ControlNet 进行扩充，以支持边缘图、分割图、关键点等条件输入。这可能会丰富控制大型扩散模型的方法，并进一步促进相关应用。

# 1. Introduction

1. 从 text-to-image 引出问题：

   1. 基于 prompt 的控制是否满足我们的需求？
   2. 在图像处理的许多任务中，都有着明确的公式，大模型能否应用于这些任务？
   3. 应该构建什么样的模型去处理广泛的问题条件和用户控制？
   4. 在特定的任务中，大模型是否能保留从数十亿张图片中获得的优势和能力？

2. ControlNet 将一个大型扩散模型的权值克隆成一个"trainable copy"和一个"locked copy"
   1. trainable copy: 保留了从数十亿张图片中学习到的网络能力
   2. locked copy: 在特定任务的数据集上进行训练，以学习控制条件


3. trainable copy 和 locked copy 使用一张名为 zero convolution 的特殊卷基层进行连接

*具体的内容在后面的 Method 部分有详细讲述*

# 2. Related Work

## 2.1 HyperNetwork and Neural Network Structure
起源于神经语言处理方法，**训练一个小的 RNN 来影响一个大的神经网络权值。**
> 引用文献：
> D. Ha, A. M. Dai, and Q. V. Le. Hypernetworks. In International Conference on Learning Representations, 2017.

## 2.2 Diffusion Probabilistic Model

## 2.3 Text-to-Image Diffusion

将扩散模型应用到 Text-to-Image 的任务当中，通常使用 CLIP 等预训练的语言模型将输入编码为潜在向量来实现。

## 2.4 Personalization,Customization, and Control of Pretrained Diffusion Model

## 2.5 Image-to-Image Translation

指出 ControlNet 与 Image-to-Image Translation 是不同的任务。

# 3. Method

$$y = F(x;\theta)$$
上式指，神经网络 $F$ 使用一组参数 $\theta$ 将 $x$ 映射到 $y$ 中。
ControlNet 的做法是：
1. 锁定 $\theta$ 中的所有参数，然后将其克隆到可训练的副本 $\theta_c$ 中，使用条件向量 $c$ 进行训练。（文章中将原始参数和新参数分别称为：locked copy, trained copy；**制作这样的副本而不是直接训练原始权值的动机是为了在数据集较小时避免过拟合，并保持从数十亿张图像中学习的大型模型的能力**）
2. 连接神经网络块的是一种独特的卷基层，称为"zero convolution",即权值和偏差都为零的 $1\times1$ 的卷基层。

模型图如下，
<img src="/images/blog/Adding-Conditional-Control-to-Text-to-Text-Diffusion-Models/截屏2023-10-22 21.56.50.png">

神经网络块的 train copy 和 locked copy 的所有输入和输出都与不存在 ControlNet 时的输入和输出一致。也就是说，当一个 ControlNet 应用于某些神经网络块时，**在进行任何优化之前，不会对深层神经特征造成任何影响。** 任何神经网络块的功能、功能和结果质量都得到了完美的保存，任何进一步的优化都将变得与微调一样快(与从头开始训练这些层相比)。
