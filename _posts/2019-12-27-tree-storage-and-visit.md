---
title: 树的存储与遍历
categories: [数据结构与算法分析]
tags: [树]
render_with_liquid: false
---


## 树的存储结构
树有多种存储方式，既可以采用顺序存储结构，又可采用链式存储结构。常用以下3种存储结构：
* 双亲表示法：使用连续空间来存储每个结点，同时在每个结点中增设一个伪指针指示其双亲结点在数组中的位置。
<div align='center'>
  <img src="/assets/images/3/tree9.jpg">
  <p>图1 双亲表示法</p>
</div>

```c
#define MAX_TREE_SIZE 100       //树中最多结点数
typedef struct{                 //树的结点定义
  ElemType data;                //数据元素
  int parent;                   //双亲位置域
}PTNode;
typedef struct{                 //树的类型定义
  PTNode nodes[MAX_TREE_SIZE]; //双亲表示
  int n;                       //结点数
} PTree;
```

* 孩子表示法：将每个结点的孩子结点用单链表链接起来形成一个线性结构，n个结点有n个孩子链表。
<div align='center'>
  <img src="/assets/images/3/tree10.jpg">
  <p>图2 孩子表示法</p>
</div>

* 孩子兄弟表示法：二叉树表示法，每个结点包括三部分内容：结点值、只想借点第一个孩子结点的指针，及指向结点下一个兄弟结点的指针。
<div align='center'>
  <img src="/assets/images/3/tree11.jpg">
  <p>图3 孩子兄弟表示法</p>
</div>

```c
typedef struct CSNode{          //树的结点定义
  ElemType data;                //数据元素
  struct CSNode *firstchild, *nextsibling; //第一个孩子和右兄弟指针                   
}CSNode, *CSTree;
```

## 二叉树的存储结构
  * 顺序存储结构：用一组地址连续的存储单元自上而下、自左至右存储完全二叉树上的结点元素。
    - 适用于满二叉树和完全二叉树的存储。
      - 既可以节省存储空间，又可以利用数组元素的下标值确定结点在二叉树中的位置，以及结点间的关系。
      - 空间利用率低

<div align='center'>
  <img src="/assets/images/3/tree4.jpg">
  <p>图4 二叉树的顺序存储结构</p>
</div>
  
  * 链式存储结构：用一个链表来存储一棵二叉树。
<div align='center'>
  <img src="/assets/images/3/tree5.jpg">
  <p>图5 二叉树的链式存储结构</p>
</div>

  二叉树的存储结构实现：

  ```c
  typedf struct BiTNode{
    ElemType data;
    struct BiTNode *lchild, rchild;
  } BiTNode, *BiTree;
  ```

## 二叉树的遍历
树的遍历，即按某种顺序依次访问树中的结点，使其均被访问一次。一般按如下三种遍历方式访问：
  * 先序遍历（preOrder）：按DLR（根->左子树->右子树）顺序递归访问二叉树。

  ```c
  void PreOrder(BiTree T){
    if (T != NULL){
      visit(T);
      PreOrder(T->lchild);
      PreOrder(T->rchild);
    }
  }
  ```

图5二叉树的先序遍历序列：ABDFCE
{: .notice--warning}

  * 中序遍历（InOrder）：按LDR（左子树->根->右子树）顺序递归访问二叉树。
  
  ```c
  void InOrder(BiTree T){
    if (T != NULL){
      InOrder(T->lchild);
       visit(T);
      InOrder(T->rchild);
    }
  }
  ```
图5二叉树的中序遍历序列：BFDACE
{: .notice--warning}

  * 后序遍历（PostOrder）：按LRD（（左子树->右子树->根）顺序递归访问二叉树。
  
  ```c
  void PostOrder(BiTree T){
    if (T != NULL){
      PostOrder(T->lchild);
      PostOrder(T->rchild);
      visit(T);
    }
  }
  ```
图5二叉树的后序遍历序列：FDBECA
{: .notice--warning}

  * 层次遍历（LevelOrder）：从第一层开始按层次自上而下、自左至右访问访问二叉树。
  
  ```c
  void LevelOrder(BiTree T){
    InitQueue(Q);
    BiTree p;
    EnQueue(Q,T);
    while(!isEmpty(Q)){
      DeQueue(Q,p);
      visit(p);
      if(p->lchild != NULL)
        EnQueu(Q, p->lchild);
      if(p->rchild != NULL)
        EnQueu(Q, p->rchild);
    }
  }
  ```
图5二叉树的层次遍历序列：ABCDEF
{: .notice--warning}

## 二叉树的构造
* 由二叉树的先序和中序遍历序列可以唯一地确定一棵二叉树。
  
  例题：已知一棵二叉树的后序序列为DABEC，中序序列为DEBAC，则先序序列为CEDBA。  
  <div align='center'>
    <img src="/assets/images/3/tree6.jpg">
    <p>图6 由后序和中序确定二叉树</p>
  </div>
* 由二叉树的中序和后序遍历序列可以唯一地确定一棵二叉树。

  例题：已知一棵二叉树的先序序列为ABCDEF，中序序列为CBAEDF，则后序序列为CBEFDA。
  <div align='center'>
    <img src="/assets/images/3/tree7.jpg">
    <p>图7 由先序和中序确定二叉树</p>
  </div>

* 由二叉树的层序和后序遍历序列可以唯一地确定一棵二叉树。
  
  例题：已知一棵二叉树的层次序列为ABCDEF，中序序列为BADCFE，则先序序列为ABCDEF。
  <div align='center'>
    <img src="/assets/images/3/tree8.jpg">
    <p>图8 由层序和中序确定二叉树</p>
  </div>

## 树、森林与二叉树的转换
* 树转换为二叉树
<div align='center'>
  <img src="/assets/images/3/tree12.jpg">
  <p>图9 树转换为二叉树</p>
</div>

记忆口诀：兄弟相连留长子。
{: .notice--warning}

* 二叉树转换为树  
<div align='center'>
  <img src="/assets/images/3/tree13.jpg">
  <p>图10 二叉树转换为树</p>
</div>

记忆口诀：左孩右右连双亲。
{: .notice--warning}

* 二叉树转换为森林
    - 若二叉树非空，则二叉树的根及其左子树为第一棵树的二叉树形式，二叉树的根的右子树又可视为除第一棵树外的森林转换后的二叉树，以同样的方法，以此类推即可得到原始森林。
    - 需要注意的是：经过上述操作形成的子树仍为二叉树，需要将其转换为树。 
<div align='center'>
  <img src="/assets/images/3/tree14.jpg">
  <p>图10 二叉树转换为森林</p>
</div>

* 森林转换为二叉树
    - 将森林中的每棵树转换为二叉树，然后将每棵树的根相连，最后以第一棵子树的根为根节点将整棵树顺时针旋转45度。
<div align='center'>
  <img src="/assets/images/3/tree15.jpg">
  <p>图11 森林转换为二叉树</p>
</div>

记忆口诀：树变二叉根相连。
{: .notice--warning}

* 树和森林的遍历
  * 树的遍历  
    - 先根遍历：若树不空，则先访问根节点，然后依次先根遍历各棵子树。
    - 后根遍历：若树不空，则先依次后根遍历各棵子树，然后访问根节点。
    - 层次遍历：若树不空，则自上而下自左至右访问树中每个结点。
  * 森林的遍历  
    - 先序遍历：访问森林中第一棵树的根节点；先序遍历第一可树中根节点的子树森林；先序遍历除去第一棵树之后剩余的树构成的森林。
    - 中序遍历：中序遍历第一棵树的根节点的子树森林；访问第一棵树的根节点；中序遍历除去第一棵树之后剩余的树构成的森林。