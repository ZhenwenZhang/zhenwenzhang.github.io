---
title: 图的应用
categories: [DataStructure]
tags: [graph]
render_with_liquid: false
---

## 最小生成树（Minimum-Spanning-Tree, MST）
  1. 一个连通图的最小生成树是图的极小连通子图，它包含图中所有的顶点，并且只含尽可能少的边。
  2. 对于生成树来说，若砍去它的一条边，则会使生成树变成非连通图；若给它增加一条边，则会形成图中的回路。


```c
最小生成树通用实现算法：
GENERATE_MST(G){
  T=NULL;
  while T 未形成一棵生成树；
    do 找到一条最小代价边(u,v)并且加入T后不会产生回路；
      T = T∪(u,v);
}
```

* Prim算法
  <div align='center'>
    <img src="/assets/images/3/graph10.jpg">
    <p>图1 Prim算法构造最小生成树过程</p>
  </div>

  Prim算法的时间复杂度是$O\left ( \left \| V\right \|^{2}\right )$.
  {: .notice--danger}

* Kruskal算法
  <div align='center'>
    <img src="/assets/images/3/graph11.jpg">
    <p>图2 Kruskal算法构造最小生成树过程</p>
  </div>

  Kruskal算法的时间复杂度是$O\left ( \left \| E\right \| log\left \| E\right \|\right )$.
  {: .notice--danger}

## 最短路径
* Dijkstra算法求单源最短路径问题
  
  求带权有向图中某个顶点到其余各顶点的最短路径时，最常用的是Dijkstra算法。

  算法步骤：
  - 初始化：先找到源点到各顶点的直达路径。
  - 选择：从这些路径中找到一条长度最短的路径。
  - 更新：对其余各条路径进行更新。
  
  <div align='center'>
    <img src="/assets/images/3/graph12.jpg">
    <p>图3 Dijkstra算法求单源最短路径问题</p>
  </div>

  Dijkstra算法的时间复杂度$O\left ( \left \| V\right \|^{3}\right )$.
  {: .notice--danger}

* Floyd算法求各顶点之间最短路径问题
  
  求图中所有顶点之间的最短路径也可以将Dijkstra算法循环执行n次（n为图中顶点的总数）实现。

  算法步骤：
  - 逐个顶点试探。
  - 在所有可能的路径中选择一条路径长度最短的。

  <div align='center'>
    <img src="/assets/images/3/graph13.jpg">
    <p>图4 Floyd算法求各顶点之间最短路径问题</p>
  </div>

  Floyd算法时间复杂度$O\left ( \left \| V\right \|^{3}\right )$.
  {: .notice--danger}

## 拓扑排序

- 有向无环图：若一个有向图中不存在环，则称为有向无环图，简称DAG图。
- AOV网：若用DAG图表示一个工程，其顶点表示活动，用有向边$\left \langle V_{i},V_{j}\right \rangle$表示活动$V_{i}$必须在活动$V_{j}$之前这样的一种关系，则将这种有向图称为顶点表示活动的网络，记为AOV网。
- 在计算机科学领域，有向图的拓扑排序是其顶点的线性排序，使得对于从顶点$u$到顶点$v$的每个有向边中，顶点$u$总排在顶点$v$之前，即满足如下条件：  
  1. 每个顶点出现且只出现一次。
  2. 若存在一条从顶点$u$到顶点$v$的路径，那么在序列中顶点$u$出现在顶点$v$的前面。
- 在拓扑排序算法处理DAG图时需要注意以下几点：
  - 入度为0的顶点，表示没有前驱活动或者前驱活动已经完成的顶点。
  - 若一个顶点有多个直接后继，则拓扑排序的结果通常不唯一；若多个顶点已经排序有序的拓扑序列中，则每个顶点有唯一的前驱后继关系，此时的拓扑排序结果是唯一的。
  - 如果一个图的邻接矩阵是三角矩阵，则可能存在拓扑序列。

  <div align='center'>
    <img src="/assets/images/3/graph14.jpg">
    <p>图5 有向图G</p>
  </div>

  对于图5中的有向图G进行拓扑排序，所有的拓扑序列是？

  - ABCFDEG
  - ABDCFEG
  - ABDCEFG
  - ABCDFEG
  - ABCDEFG
  
  拓扑排序的算法时间复杂度是$O\left (\left \| V\right \| +\left \| E\right \| \right )$。
  {: .notice--danger}

## 关键路径（Critical Path）

- 在带权有向图中，以顶点表示事件，以有向边表示活动，以边上的权值表示完成该活动需要的时间，则称这种用边表示活动的网络为AOE网。
- AOE网具有如下性质：
  - 只有在某顶点表示的事件发生后，从该顶点出发的各种有向边比碍事的活动才能开始。
  - 只有进入某一顶点的各有向边所代表的活动都结束时，该顶点比碍事的事件才能发生。
  - AOE网中只有一个入度为0的点，称为源点，表示整个工程的开始；只有一个出度为0的顶点，称为汇点，表示整个工程的结束。
- 关键路径、关键活动：从源点到汇点的所有路径中，具有最大路径长度的路径称为关键路径；关键路径上的活动称为关键活动。

关键活动参量定义：

1. 事件$V_{k}$的最早发生时间$V_{e}\left(k\right)$
   
    源点表示事件的最早发生时间是$V_{e}\left(源点\right)=0$，计算时按从前往后的顺序计算，加上边权值后找最大值。
2. 事件$V_{k}$的最迟发生时间$V_{l}\left(k\right)$
   
   $V_{l}\left(汇点\right)=V_{e}\left(汇点\right)$，计算时按从后往前的顺序计算，减去边权值后找最小值。
3. 活动$a_{i}$的最早开始时间$e\left(i\right)$
   
   活动的起点表示的事件最早发生的事件，$e\left(i\right)=V_{e}\left(k\right)$。
4. 活动$a_{i}$的最迟开始时间$l\left(i\right)$
   
   活动的终点表示的事件的最迟发生时间与该活动所需时间之差，$l\left(i\right)=V_{i}\left(j\right)-Weight$。

求关键路径的算法步骤如下：
1. 求AOE网中所有事件的最早发生时间$V_{e}\left(\right)$。
2. 求AOE网中所有事件的最迟发生时间$V_{l}\left(\right)$。
3. 求AOE网中所有活动的最早开始时间$e\left(\right)$。
4. 求AOE网中所有活动的最早开始时间$l\left(\right)$。
5. 求AOE网中所有活动的差额$d$，找出$d=0$的活动构成关键路径。

  <div align='center'>
    <img src="/assets/images/3/graph15.jpg">
    <p>图6 求解关键路径的过程</p>
  </div>

对于关键路径，需要注意以下几点：

1. 关键路径上的活动的都是关键活动，是决定整个工程的关键因素，可以通过加快关键活动来缩短整个工程的工期。
2. 网中的关键路径并不唯一，对于有多条关键路径的网，只提高一条关键路径上的关键活动速度并不能缩短整个工程的周期，只有加快那些包括在关键路径上关键活动才能达到缩短工期的目的。