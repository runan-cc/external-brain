---
title: Tree Data Structures
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [data-structure, algorithm, tree]
sources: []
confidence: high
---

# Tree Data Structures (树形数据结构)

## 定义

树是**层级化的非线性数据结构**——每个节点有零个或多个子节点。它是计算机科学中最通用的数据结构之一：文件系统、数据库索引、编译器 AST、HTML DOM 都是树。

## 基本概念

| 术语 | 说明 |
|------|------|
| Root | 顶层根节点 |
| Leaf | 无子节点的节点 |
| Depth | 从根到该节点的边数 |
| Height | 从该节点到最深叶子的边数 |
| Degree | 子节点数 |
| 二叉树 | 每个节点最多 2 个子节点 |

## 二叉搜索树 (BST)

```python
# 左 < 根 < 右
class BST:
    def search(self, val):
        node = self.root
        while node:
            if val == node.val: return node
            elif val < node.val: node = node.left
            else: node = node.right
        return None
```

| BST 变体 | 平衡方式 | 最坏深度 | 特点 |
|----------|----------|----------|------|
| 普通 BST | 无 | O(n) | 退化即链表 |
| **AVL Tree** | 旋转（平衡因子 ±1） | O(log n) | 严格平衡，查询快 |
| **Red-Black Tree** | 着色 + 旋转 | O(log n) | 插入/删除比 AVL 快 |
| **B-Tree** | 多路平衡 | O(log n) | 数据库/文件系统索引 |
| B+ Tree | B-Tree + 叶子链表 | O(log n) | 范围查询，数据库标配 |
| Splay Tree | 访问时旋转到根 | 均摊 O(log n) | 缓存最近访问 |

## Red-Black Tree 五大性质

1. 每个节点是红色或黑色
2. 根是黑色
3. 所有叶子 (NIL) 是黑色
4. **红节点的子节点必须是黑色**（不能有两个连续红）
5. 从任意节点到其后代叶子的每条路径上，黑节点数量相同

→ 性质 4+5 保证最长路径 ≤ 2×最短路径，从而保证 O(log n)

## B-Tree 和 B+Tree

| 维度 | B-Tree | B+ Tree |
|------|--------|---------|
| 数据存储 | 所有节点 | 只在叶子 |
| 内部节点 | 存 key + data | 只存 key（索引） |
| 叶子间链接 | 无 | 链表（范围查询极快） |
| 使用 | 文件系统 | MySQL InnoDB, PostgreSQL |

### 为什么数据库爱 B+ Tree？
1. 叶子链表 → 范围查询 O(log n + k)，连续 I/O
2. 内部节点只存索引 → 一个节点存更多 key → 树更矮 → 更少磁盘 I/O
3. 所有数据在叶子 → 统一层级

## Trie (前缀树)

用于字符串检索和前缀匹配。

```
    *
   / \
  a   i
 / \    \
t   p    n
    /     \
   p       n (→ "inn")
  (→ "app")
```

- 插入/查询：O(L)，L = 字符串长度
- 应用：搜索自动补全、IP 路由最长前缀匹配、拼写检查
- 内存占用大，可用 Radix Tree (压缩 Trie) 优化

## 堆 (Heap)

| 类型 | 根 | 插入 | 删根 | 用途 |
|------|-----|------|------|------|
| Min Heap | 最小 | O(log n) | O(log n) | 优先队列 |
| Max Heap | 最大 | O(log n) | O(log n) | 堆排序 |
| Binary Heap | 完全二叉树实现 | — | — | 最简单实现 |
| Fibonacci Heap | 更平摊 | O(1) 均摊 | O(log n) | Dijkstra 加速 |

## 跳表 (Skiplist)

概率性的有序数据结构——多层链表，每层是下层的"快速通道"。
- 查询/插入/删除：O(log n) 期望
- 比平衡树简单、并发友好
- **Redis Sorted Set 底层实现**
- LevelDB/RocksDB 的 MemTable

## 关系

- [[sorting-algorithms]] — 堆排序
- [[data-structures-and-algorithms]]
- [[postgresql]] — B+ Tree 索引
- [[redis]] — Skiplist
