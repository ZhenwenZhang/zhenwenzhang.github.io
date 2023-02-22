---
title: "Inferring Social Media Users’ Mental Health Status from Multimodal Information"
tags:
  - mental health
  - social media
  - multimodal analysis
  - machine learning
---

Worldwide, an increasing number of people are suffering from mental health disorders such as depression and anxiety. In the United States alone, one in every four adults suffers from a mental health condition, which makes mental health a pressing concern. In this paper, we explore the use of multimodal cues present in social media posts to predict users’ mental health status. Specifically, we focus on identifying social media activity that either indicates a mental health condition or its onset. We collect posts from Flickr and apply a multimodal approach that consists of jointly analyzing language, visual, and metadata cues and their relation to mental health. We conduct several classification experiments aiming to discriminate between (1) healthy users and users affected by a mental health illness; and (2) healthy users and users prone to mental illness. Our experimental results indicate that using multiple modalities can improve the performance of this classification task as compared to the use of one modality at a time, and can provide important cues into a user’s mental status.

[LREC 2020](https://www.aclweb.org/anthology/2020.lrec-1.772.pdf)

More specifically, we focus our efforts on two classification tasks. First, we aim to distinguish between healthy users and users affected by a mental health illness. Second, we attempt to discriminate between healthy users and mental illness prone users by identifying their mental illness
onset, defined as the time when they start using posts tags related to mental illnesses. We explore a large set of multimodal features that attempt to capture linguistic, visual, and behavioral aspects of users’ posting activity. We analyze feature significance using an effect size analysis to
identify which cues from which modality are indicative of mental health status. We also conduct several learning experiments where we explore the predictive power of the different visual, language, and posting activity features for the two classification tasks.

### 论文信息

![1](/assets/images/9/9.png)

### 数据采集对照（正常vs不正常）

![2](/assets/images/9/1.png)

### Sample Flickr posts

![3](/assets/images/9/2.png)

### 健康组与不健康组视觉特征比较

![4](/assets/images/9/3.png)

### 健康组与不健康组语言特征比较

![5](/assets/images/9/4.png)

### 健康组与不健康组的Post features对比

![6](/assets/images/9/5.png)

### 基于时序信息的发帖量统计

![7](/assets/images/9/6.png)

### 基于视觉和语言特征的分类F值比较

![8](/assets/images/9/7.png)

### 基于多模态特征的分类F值比较

![9](/assets/images/9/8.png)