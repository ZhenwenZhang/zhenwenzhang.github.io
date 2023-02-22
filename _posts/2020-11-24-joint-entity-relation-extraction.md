---
title: "A Frustratingly Easy Approach for Joint Entity and Relation Extraction"
tags:
  - 实体识别
  - 关系抽取
  - 联合建模
  - 神经网络与深度学习
---

#### 作者

Zexuan Zhong, Danqi Chen. Department of Computer Science, Princeton University

#### 论文下载地址

[https://arxiv.org/pdf/2010.12812.pdf](https://arxiv.org/pdf/2010.12812.pdf)

#### 摘要

End-to-end relation extraction aims to identify named entities and extract relations between them simultaneously. Most recent work models
these two subtasks jointly, either by unifying them in one structured prediction framework, or multi-task learning through shared representations. In this work, we describe a very simple approach for joint entity and relation extraction, and establish the new stateof-
the-art on standard benchmarks (ACE04, ACE05, and SciERC). Our approach essentially builds on two independent pre-trained encoders and merely uses the entity model to provide input features for the relation model. Through a series of careful examinations, we validate the importance of learning distinct contextual representations for entities and relations, fusing entity information at the input layer of the relation model, and incorporating global context. Finally, we also present an efficient approximation to our approach which requires only one pass of both encoders at inference time, obtaining a 8-16x speedup with a small accuracy drop.

#### 作者提出的问题

端到端的关系抽取旨在识别命名实体并抽取实体之间的关系，大多数研究工作将其视为两个子任务，要么通过一种结构联合建模，要么通过共享表示的方式进行多任务学习。

#### 方法

作者提出了一种非常简单的用于实体识别和关系抽取的联合建模方法，并在(ACE04, ACE05, and SciERC)等数据集上取得了SOTA。作者构建了两个独立的预训练编码器，并且仅使用实体识别模型给关系抽取模型提供输入特征。通过一系列的实验，作者验证了学习实体和关系的不同上下文表示形式，在关系模型的输入层融合实体信息以及合并全局上下文的重要性。最后，作者对他们的方法提出了一种有效的近似方法，该方法在推理时仅需要两个编码器通过一次，即可获得8-16倍的加速比，并且精度下降很小。

#### 为什么流水线的方式表现如此好？
1. 实体模型和关系模型获取到的上下文信息应该是不一样的，共享语义表示会损害其性能。 
2. 在关系识别模型中融合实体信息（实体边界和类型）是非常重要且有效的。 
3. 利用跨句子的语义信息对两个任务都是有益的。 
4. 强大的预训练语言模型可以为下游任务带来更好的收益。 

#### 模型结构

![联合抽取模型](/assets/images/4/model.png)

#### 损失函数

![损失函数](/assets/images/4/loss.png)