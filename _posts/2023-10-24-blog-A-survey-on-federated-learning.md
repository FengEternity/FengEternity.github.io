---
title: 'A survey on federated learning'
date: 2023-10-25
permalink: /posts/2023/10/22/A survey on federated learning/
tags:
  - Deep Learning
  - Federaled learning
---

- **论文链接：**[https://www.sciencedirect.com/science/article/pii/S0950705121000381?via%3Dihub](https://www.sciencedirect.com/science/article/pii/S0950705121000381?via%3Dihub)
- **会议/期刊：** Knowledge-based systems *（CCFC* *SCI一区）*
- **Keywords**：Federaled learning, Privacy protection

# Abstract

联合学习是在一个**中央聚合器的协调下，多个客户机协作**解决机器学习问题的一种设置。该设置还允许分散训练数据，以确保每个设备的数据隐私。

联邦学习坚持两大思想:**局部计算和模型传输**，降低了传统集中式机器学习方法带来的一些系统隐私风险和成本。

客户端原始数据存储在本地，不允许交换和迁移。通过联合学习，每个设备使用本地数据进行本地训练，然后**将模型上传到服务器进行聚合**，最后服务器将模型更新发送给参与者，从而达到学习目标。本文从**数据划分、隐私机制、机器学习模型、通信体系结构和系统异构**五个方面系统地介绍了联邦学习的现有工作，为该领域的研究提供了一个全面的综述。

然后，梳理了联邦学习目前面临的挑战和未来的研究方向。最后，总结了现有联邦学习的特点，并分析了当前联邦学习的实际应用。


# 1. Introduction

## 1.1 Backgrounds of federated learning

需要解决的问题：
  - 数据安全
  - 数据孤岛（data islands）


联邦学习提供了一种隐私保护机制，可以有效地利用终端设备的计算资源对模型进行训练，防止隐私信息在数据传输过程中被泄露。

联邦学习主要通过交换经过加密处理的参数来保护用户隐私，而攻击者无法获取源数据。

$$联邦学习 = 分布式训练 + 隐私保护机制$$

联邦学习根据数据的分布可以分为：
  * 横向联邦学习：适用于两个数据集的用户特征重叠较多而用户重叠较少的情况。
  * 纵向联邦学习：两个数据集的用户特征很少重叠，但用户重叠较多的情况。
  * 联邦迁移学习：两个数据集的用户和用户特征很少重叠的情况

## 1.2 Challenges to dederated learning

1. 隐私保护
2. 数据量不足：每个移动设备上数据量可能不足
3. 统计异质性：节点设备上的数据可能是非独立同分布的


## 1.3 Main contributions

# 2. Related works

## 2.1 Definition of federated learning

<img src="/images/blog/A_survey_on_federated_learning/screenshot-20231025-191922.png">

步骤：
1. 服务器将初始模型发送到每个设备
2. 分布式设备使用本地数据进行训练
3. 服务器将收集到的本地模型聚合到全局模型，
4. 最后再将全局模型替换到分布式设备上


## 2.2 The development of federated learning

举例说明了什么是联邦学习，所以这部分的标题为什么叫 'development'？

# 3. Categorizations of federated learing

本节从数据分区、隐私机制、适用的机器学习模型、通信体系结构和解决异构问题的方法五个方面总结了联邦学习的分类。

<img src="/images/blog/A_survey_on_federated_learning/screenshot-20231025-193819.png">

## 3.1 Data partition

根据数据的样本空间和特征空间的不同分布模式，分为：横向联邦、纵向联邦和联邦迁移，如下图所示：

<img src="/images/blog/A_survey_on_federated_learning/screenshot-20231025-194055.png">

### 3.1.1 Horizontal federated learning

