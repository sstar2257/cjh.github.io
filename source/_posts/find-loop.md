---
title: 判断一个图是否存在环
date: 2019-04-11 15:23:27
updated: 2019-04-15 14:02:00
tags: graph
---

## 有向图

### 算法1
对于有向图进行拓扑排序可以判断是否存在环。  
对于有向图的拓扑排序，大家都知道的kahn算法：  
1. 计算图中所有点的入度，把入度为0的点加入栈
2. 如果栈非空：
   取出栈顶顶点a，输出该顶点值，删除该顶点
   从图中删除所有以a为起始点的边，如果删除的边的另一个顶点入度为0，则把它入栈
3. 如果图中还存在顶点，则表示图中存在环；否则输出的顶点就是一个拓扑排序序列

### 算法2
无向图的算法2

### 算法3
根据有向图的强连通分量算法，每个强连通分量中必定存在环，因为根据强连通分量的定义：从顶点 i 到 j 有一条路径，并且从 j 到 i 也有一条路径。求强连通分量的算法可以参考[维基百科](https://zh.wikipedia.org/wiki/强连通分量)。  

<!-- more -->
## 无向图
### 算法1
对于环1-2-3-4-1，每个节点的度都是2，基于此我们有如下算法（这是类似于有向图的拓扑排序）：  
1. 求出图中所有顶点的度；
2. 删除图中所有度<=1的顶点以及与该顶点相连的边，把与这些边相连的另一个顶点度减1；
3. 重复步骤2
4. 最后如果还存在未被删除的顶点，则表示有环，否则没有环。
时间复杂度为O（E+V），其中E、V分别为图中边和顶点的数目。  

### 算法2
深度优先遍历该图，如果在遍历的过程中，发现某个节点有一条边指向已经访问过的节点，并且这个已访问过的节点不是当前节点的父节点（这里的父节点表示dfs遍历顺序中的父节点），则表示存在环。但是我们不能仅仅使用一个bool数组来标志节点是否访问过。  
按照算法导论22.3节深度优先搜索中，对每个节点分为三种状态，白、灰、黑。开始时所有节点都是白色，当开始访问某个节点时该节点变为灰色，当该节点的所有邻接点都访问完，该节点颜色变为黑色。那么我们的算法则为：如果遍历的过程中发现某个节点有一条边指向颜色为灰的节点，那么存在环。  
算法时间复杂度也是O(E+V)。  

[原文连接](http://www.cnblogs.com/TenosDoIt/p/3644225.html)  

