---
title: SIGIR 2021｜A Novel Summarization Boosted DeepFramework for Depression Detection on Social Media
tags:
  - 抑郁症检测
  - 社交媒体计算
---


- ### 论文信息

    Zogan, Hamad, Imran Razzak, Shoaib Jameel, and Guandong Xu. "DepressionNet: Learning Multi-modalities with User Post Summarization for Depression Detection on Social Media." In Proceedings of the 44th International ACM SIGIR Conference on Research and Development in Information Retrieval, pp. 133-142. 2021.

- ### 摘要

    Twitter is currently a popular online social media platform whichallows users to share their user-generated content. This publicly-generated user data is also crucial to healthcare technologies be-cause the discovered patterns would hugely benefit them in severalways. One of the applications is in automatically discovering mentalhealth problems, e.g., depression. Previous studies to automaticallydetect a depressed user on online social media have largely reliedupon the user behaviour and their linguistic patterns includinguser’s social interactions. The downside is that these models aretrained on several irrelevant content which might not be crucialtowards detecting a depressed user. Besides, these content have anegative impact on the overall efficiency and effectiveness of themodel. To overcome the shortcomings in the existing automaticdepression detection methods, we propose a novel computationalframework for automatic depression detection that initially selectsrelevant content through a hybrid extractive and abstractive sum-marization strategy on the sequence of all user tweets leading toa more fine-grained and relevant content. The content then goesto our novel deep learning framework comprising of a unifiedlearning machinery comprising of Convolutional Neural Network(CNN) coupled with attention-enhanced Gated Recurrent Units(GRU) models leading to better empirical performance than exist-ing strong baselines.

- ### 论文试图解决什么问题？
    
    - 图像信息和文本信息的联合建模
    - 抑郁症相关信息（图片和文本）的提纯

- ### 这是否是一个全新的问题？

    否

- ### 问章要验证一个什么科学假设？

    用户生成社交媒体内容多样，并不是所有的用户内容都对抑郁症检测具有积极作用，作者在文中重点探索了抑郁症相关信息的提纯。

- ### 论文中提到的解决方案关键是什么？

    作者创新性地提出了利用强化学习思想实现抑郁症相关文本和图像信息的筛选

- ### 论文中的实验是怎么设计的？

    - 分别设置了基于文本、图像和文本图像融合的实验
    - 分析了提纯后文本的主题词（基于词频）
    - 鲁棒性分析：不同规模下提取结果结果的抑郁检测实验比较

- ### 用于定量分析的数据集是什么？代码是否开源？

    - Shen等人基于Twitter在2017年提出的Textual Depression Dataset
    - 复旦大学张奇团队基于上述文本数据，抓取了图片数据，构建了一个全新的多模态数据集
    - 未找到开源代码和数据集

- ### 论文中的实验及结果有没有很好的支持需要验证的科学假设？

    论文中的实验和结果验证了作者提出的科学假设

- ### 问章到底有什么贡献？

    - 相比基于层叠注意力机制的编码方法，作者提出的强化学习的方法一定程度上更合理、更具有说服力
    - 降低了计算难度
    - 提供了一种新思路

- ### 下一步呢？有什么工作可以继续深入？

    - 多模态信息融合中图像信息发挥的具体作用探索
    - 图文相关性和无关性探索
