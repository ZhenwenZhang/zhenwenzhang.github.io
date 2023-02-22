---
title: Document-Level Relation Extraction with Reconstruction
tags:
  - Information Extraction
  - Relation Extraction
  - GNN
---

**Background:** In document-level relation extraction (DocRE), graph structure is generally used to encode relation information in the input document to classify the relation category between each entity pair, and has greatly advanced the DocRE task over the past several years. However, the learned graph representation universally models relation information between all entity pairs regardless of whether there are relationships between these entity pairs. Thus, those entity pairs without relationships disperse the attention of the encoder-classifier DocRE for ones with relationships, which may further hind the improvement of DocRE.

**Methods:** To alleviate this issue, we propose a novel encoder-classifierreconstructor model for DocRE. The reconstructor manages to reconstruct the ground-truth path dependencies from the graph representation, to ensure that the proposed DocRE model pays more attention to encode entity pairs with relationships in the training. Furthermore, the reconstructor is regarded as a relationship indicator to assist relation classification in the inference, which can further improve the performance of DocRE model.

**Results:** Experimental results on a large-scale DocRE dataset show that the proposed model can significantly improve the accuracy of relation extraction on a strong heterogeneous graph-based baseline. The code is publicly available at https://github.com/xwjim/DocRE-Rec.

<!-- **Our contributions:**  -->
<!-- 1. evaluating state-of-the-art clinical BERT models on the classication of lifestyle factors in clinical notes of patients with AD 
2. using weak supervision to overcome the burdensome task of creating a hand-labeled dataset. -->

<!-- ![模型图](/assets/images/11/model.png)

![数据示例](/assets/images/11/dataset_example.png)

![实验结果](/assets/images/11/results.png) -->