---
title: '图的存储结构'
tags: 
  - 数据结构与算法分析
  - 图
---

## 邻接矩阵
* 概念
  - 用一个一维数组存储顶点信息，用一个二维数组存储图中边的信息（顶点之间的邻接关系）.  
  - 对于不带权图而言，顶点之间有边存在则在矩阵中用1表示.
  - 对于带权图而言，顶点之间有边存在则在矩阵中用边的权值表示.

<div align='center'>
  <img src="/assets/images/3/graph1.jpg">
  <p>图1 无向图及其邻接矩阵</p>
</div>

<div align='center'>
  <img src="/assets/images/3/graph2.jpg">
  <p>图2 有向图及其邻接矩阵</p>
</div>

<div align='center'>
  <img src="/assets/images/3/graph3.jpg">
  <p>图3 网及其邻接矩阵</p>
</div>

* 结构定义实现
  
```c
#define MaxVertexNum 100 //顶点数目最大值
typedef char VertexType; //顶点的数据类型
typedef int EdgeType; //顶点的数据类型
typedef struct{
  VertexType Vex{MaxVertexNum}; //顶点表
  EdgeType Edge{MaxVertexNum}{MaxVertexNum}; // 邻接矩阵
  int vexnum, arcnum; //图的当前顶点树和弧数
}Mgraph;
```

* 性质
  - 无向图的邻接矩阵一定是一个唯一的对称矩阵.
  - 无向图邻接矩阵第i行（列）非零元素个数是第i个顶点的度.
  - 有向图邻接矩阵第i行（列）非零元素个数是第i个顶点的出（入）度.
  - 稠密图适合邻接矩阵的存储表示.
  - 邻接矩阵表示法的空间复杂度是$O\left (n^{2} \right )$，n是图中顶点个数.
  - 设图G的邻接矩阵是A，则$A^{n}$的元素$A^{n}\left [ i\right ]\left [ j\right ]$表示从顶点i到顶尖j的长度为n的路径的数目.

## 邻接表
* 概念
  - 当存储的图为稀疏图时，邻接矩阵存储方式显然会浪费大量的存储空间，而图的邻接表法结合了顺序存储和链式存储方法，大大减少了这种不必要的浪费.
  - 邻接表法由顶点表和边表实现，顶点表存储图中顶点元素信息，边表存储与该顶点连通顶点的边信息.

<div align='center'>
  <img src="/assets/images/3/graph4.jpg">
  <p>图4 顶点表和边表结点结构</p>
</div>

<div align='center'>
  <img src="/assets/images/3/graph5.jpg">
  <p>图5 无向图的邻接表表示法</p>
</div>

<div align='center'>
  <img src="/assets/images/3/graph6.jpg">
  <p>图6 有向图的邻接表表示法</p>
</div>

* 结构定义实现

```c
#define MaxVertexNum 100 //顶点数目最大值
typedef struct ArcNode{  //边表结点
  int adjvex; //该弧所指向顶点的位置
  struct ArcNode *next; //指向下一条弧的指针
  // InfoType info; //网的边权值
}ArcNode;
typedef struct VNode{  //顶点表结点
  vertextype data; //顶点信息
  ArcNode *first; //指向第一条依附该顶点的弧的指针
}VNode, AdjList[MaxVertexNum];
typedef struct{
  AdjList vertices; //邻接表
  int vexnum, arcnum; //图的顶点数和弧数
}ALgraph; //ALGraph是以邻接表存储的图类型

```

* 性质
  - 若图为无向图，则所需的存储空间为$O\left ( \left \| V\right \| + 2\left \| E\right \|\right )$.
  - 若图为有向图，则所需的存储空间为$O\left ( \left \| V\right \| + \left \| E\right \|\right )$.
  - 邻接表法适用于稀疏图.
  - 邻接表法容易查找给定顶点的邻边，花费时间为$O\left(n\right)$，n是单链表的长度.
  - 图的邻接表表示不唯一（因为各结点的链接次序是任意的）.
  - 有向图的邻接表表示中，求一个顶点的出度只需计算其邻接表中的结点个数.
  
## 十字链表
  十字链表是有向图的一种链式存储结构，解决了有向图邻接表表示法中只能计算出度问题。
<div align='center'>
  <img src="/assets/images/3/graph7.jpg">
  <p>图7 十字链表存储结点结构</p>
</div>

    tailvex（尾域）：指示弧尾在图中的位置.
    headvex（头域）：指示弧头在图中的位置.
    hlink（链域）：指向弧头相同的下一条弧.
    tlink（链域）：指向弧尾相同的下一条弧.
    info：指向该弧的相关信息.

    data：存储顶点的相关信息.
    firstin：指向以该顶点为弧头的下一个弧结点.
    firstout：指向以该顶点为弧尾的下一个弧结点.

<div align='center'>
  <img src="/assets/images/3/graph8.jpg">
  <p>图8 十字链表表示法</p>
</div>

* 结构定义实现

```c
#define MaxVertexNum 100 //顶点数目最大值
typedef struct ArcNode{  //边表结点
  int tailvex, headvex; //该弧的头尾结点
  struct ArcNode *hlink, *tlink; //分别指向弧头相同和弧尾相同的结点
  // InfoType info; //相关信息指针
}ArcNode;
typedef struct VNode{  //顶点表结点
  vertextype data; //顶点信息
  ArcNode *firstin, *firstout; //指向第一条入弧和出弧
}VNode;
typedef struct{
  VNode xlist[MaxVertexNum]; //邻接表
  int vexnum, arcnum; //图的顶点数和弧数
}GLgraph; //GLGraph是以十字链表表存储的图类型

```

    图的十字链表表示不是唯一的，但是一个十字链表表示确定一个图。

## 邻接多重表

图的邻接表表示容易求结点和边的各种信息，但在邻接表中求两个顶点之间是否存在边而对边执行删除操作时，需要分别在两个顶点的边表中遍历，效率较低。

<div align='center'>
  <img src="/assets/images/3/graph9.jpg">
  <p>图9 邻接多重表存储结点结构</p>
</div>

    mark：标志域，标记该边是否被搜索过.
    ivex、jvex：该边依附的两个顶点在图中的位置.
    ilink：指向下一条依附于顶点ivex的边.
    jlink：指向下一条依附于顶点jvex的边.
    info：指向和边有关的各种信息的指针域.

    data：存储顶点的相关信息.
    firstedge：指示第一条依附于该顶点的边.

* 结构定义实现

```c
#define MaxVertexNum 100 //顶点数目最大值
typedef struct ArcNode{  //边表结点
  bool mark; //访问标记
  int ivex, jvex; //分别指向该弧的两个顶点
  struct ArcNode *ilink, *jlink; //分别指向两个顶点的下一条边
  // InfoType info; //相关信息指针
}ArcNode;
typedef struct VNode{  //顶点表结点
  vertextype data; //顶点信息
  ArcNode *firstedge; //指向第一条依附于该顶点的边
}VNode;
typedef struct{
  VNode adjmulist[MaxVertexNum]; //邻接表
  int vexnum, arcnum; //图的顶点数和弧数
}AMLgraph; //AMLGraph是以邻接多重表表存储的图类型

```
