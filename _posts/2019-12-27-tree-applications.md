---
title: Application of Tree
categories: [DataStructure]
tags: [tree]
render_with_liquid: false
---

## 二叉排序树

<div align='center'>
  <img src="/assets/images/3/tree16.jpg">
  <p>图1 二叉排序树</p>
</div>

* 二叉排序树的定义  
   二叉排序树，又称二叉查找树，具有以下特点：  
   - 若左子树非空，则左子树上所有结点关键字值小于根节点的关键字值。
   - 若右子树非空，则右子树上所有结点关键字值大于根节点的关键字值。
   - 左右子树本身分别是一棵二叉排序树。
  
  通过对二叉排序树中序遍历即可得到一个升序序列。
* 二叉排序树的查找  
    从根结点开始依次比较，若小于根结点的关键字值，则在左子树中查找；反之，则在右子树中查找。
* 二叉排序树的插入  
    若原二叉树非空，则直接插入结点；否则，若关键字小于根结点关键字，则插入左子树；反之，则插入右子树。
* 二叉排序树的构造  
    依次输入数据元素，根据二叉排序树的插入规则构建二叉排序树。
* 二叉排序树的删除  
    二叉排序树删除操作的实现过程按3种情况处理：  
    - 若删除的结点是叶结点，则直接删除。
    - 若删除的结点只有左（右）子树，则用其左（右）子树替换。
    - 若删除的结点既有左子树又有右子树，则使用被删除结点的直接前驱结点（左子树中值最大的结点）或直接后继结点（右子树中值最小的结点）代替。
<div align='center'>
  <img src="/assets/images/3/tree17.jpg">
  <p>图2 二叉排序树删除操作</p>
</div>

* 效率分析：
  - 高度为h的二叉排序树，插入和删除操作的运行时间都是$O\left (h  \right )$。最坏的情况下，形成的二叉排序树是一个倾斜的单支树。
  - 平均查找长度，主要取决于树的高度。

## 平衡二叉树
* 平衡二叉树的定义  
  插入和删除二叉树的结点时，任意结点的左右子树高度差不超过1，这样的树称之为平衡二叉树。
* 平衡二叉树的插入  
  每当在二叉树中插入（或删除）一个结点时，先检查其插入路径上的结点是否因为本次插入而不平衡。若不平衡，则调整其结构使其达到平衡状态。
* 平衡二叉树的查找  
  - 查找过程与二叉排序树相同。
  - 查找过程中，与关键字的比较次数不超过树的深度。
  - 含有n个结点的平衡二叉树的最大深度为$O\left ( {log_{2}}^{n} \right )$，因此平衡二叉树的平均查找长度为$O\left ( {log_{2}}^{n} \right )$。
  
## 哈夫曼树和哈夫曼编码
* 哈弗曼树的定义  
  在含有n个带权叶子结点的二叉树中，其中带权路径长度（WPL）最小的二叉树称为哈夫曼树，也称最优二叉树。
* 哈夫曼树的构造  
  - 给定n个带权结点，选取权值最小的两个结点作为新节点的左、右子树，新节点的权值为两个结点的权值之和。依次对剩余结点进行该操作，即可构造一棵哈弗曼树。
  - 权值越小的结点，路径长度越大；权值越大的结点，路径长度越小。
  - 构造过程中，共新建了n-1个结点（根结点），因此哈夫曼树中的结点总数为2n-1。

  例题：给定集合{3, 5, 6, 9, 12},其对应的哈夫曼树是？
<div align='center'>
  <img src="/assets/images/3/tree18.jpg">
  <p>图4 哈夫曼树的构造</p>
</div>

* 哈夫曼编码  
  