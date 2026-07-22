---
title: 数据结构与算法
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [algorithm, data-structure, programming]
sources: []
confidence: high
---

# 数据结构与算法

## 定义

数据结构是数据的组织方式，算法是解决问题的步骤。二者是计算机科学的基石——**程序 = 数据结构 + 算法**。

## 核心数据结构

| 结构 | 操作复杂度 | 特点 |
|------|-----------|------|
| Array | O(1) 随机访问 | 定长，连续内存 |
| Linked List | O(1) 插入/删除 | 动态，非连续 |
| Stack | LIFO | push/pop, 函数调用栈 |
| Queue | FIFO | enqueue/dequeue, BFS |
| Hash Table | O(1) 平均 | key-value，碰撞用链地址/开放寻址 |
| Binary Tree | O(log n) 平衡 | 搜索、排序、表达 |
| Heap | O(log n) | 优先队列，堆排序 |
| Graph | - | 邻接表/矩阵，DFS/BFS/最短路径 |

## 核心算法

### 排序
| 算法 | 平均复杂度 | 稳定性 |
|------|-----------|--------|
| Quick Sort | O(n log n) | 不稳定 |
| Merge Sort | O(n log n) | 稳定 |
| Heap Sort | O(n log n) | 不稳定 |
| Timsort | O(n log n) | 稳定（Python/Java 默认） |

### 搜索
- **二分查找**：O(log n)，有序数组
- **BFS**：最短路径（无权图），队列
- **DFS**：路径查找/拓扑排序，栈/递归
- **A\***：启发式搜索，游戏寻路

### 经典算法
- **动态规划 (DP)**：分解为子问题，避免重复计算（背包、LCS、编辑距离）
- **贪心**：每步选局部最优（Dijkstra、Huffman）
- **分治**：分解 → 解决 → 合并（归并排序、快速排序）
- **回溯**：试错 + 剪枝（N 皇后、数独）

## 复杂度分析

- **Big O**：最坏情况上限
- **Ω (Omega)**：最好情况下限
- **Θ (Theta)**：紧确界
- **空间复杂度**：额外内存开销

## 经典问题

| 问题 | 方法 |
|------|------|
| 最长公共子序列 (LCS) | DP |
| 0-1 背包 | DP |
| 最短路径 | Dijkstra / Bellman-Ford / Floyd-Warshall |
| 最小生成树 | Prim / Kruskal |
| 字符串匹配 | KMP / Rabin-Karp / Sunday |
| 约瑟夫环 | 链表/数学公式 |

## 相关概念

- [[big-o-notation]]
- [[dynamic-programming]]
- [[graph-theory]]
