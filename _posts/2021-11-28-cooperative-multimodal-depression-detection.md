---
title: Coperrative Multimodal Approach to Depression Detection in Twitter
tags:
  - Reinforcement Learning
  - Depression Detection
  - Social Media
---

- ### 论文信息

    Gui, Tao, Liang Zhu, Qi Zhang, Minlong Peng, Xu Zhou, Keyu Ding, and Zhigang Chen. "Cooperative multimodal approach to depression detection in Twitter." In Proceedings of the AAAI Conference on Artificial Intelligence, vol. 33, no. 01, pp. 110-117. 2019.

- ### 摘要

    The advent of social media has presented a promising new opportunity  for  the  early  detection  of  depression.  To  do  so effectively,  there are  two  challenges  to  overcome. The  firstis  that  textual  and  visual  information  must  be  jointly  considered  to  make  accurate  inferences  about  depression.  The second challenge is that due to the variety of content types posted  by  users,  it  is  difficult  to  extract  many  of  the  relevant indicator texts and images. In this work, we propose the use of a novel cooperative multi-agent model to address these challenges. From the historical posts of users, the proposed method  can  automatically  select  related  indicator  texts  and images. Experimental results demonstrate that the proposed method outperforms state-of-the-art methods by a large margin (over 30% error reduction). In several experiments and examples, we also verify that the selected posts can successfully indicate user depression, and our model can obtained arobust performance in realistic scenarios.

    社交媒体技术的发展为抑郁症的早期发现带来了新的契机。为了有效地进行社交媒体抑郁症识别，通常面临着两个方面的挑战。第一个挑战是文本和图像信息必须联合建模才能更精确的预测抑郁症；第二个挑战是由于用户在社交媒体平台发布的内容多样化，抽取相关的文本和图像标记信息比较难。在本文中，我们提出了一种创新性的协作多代理模型以解决这些问题，这种多代理协作模型可以自动地从用户发布的历史信息中选择相关的文本和图像信息。在几个实验和例子中，我们也验证了所选的帖子可以成功地表明用户的抑郁情绪，并且我们的模型可以在现实场景中获得稳健的性能。

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