---
title: 算法设计范式
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [algorithm, technique, design]
sources: []
confidence: high
---

# 算法设计范式

## 定义

算法设计范式是**解决问题的通用策略模板**——不是具体算法，而是教你如何构造算法的方法论。掌握范式比记具体算法更重要。

## 分治法 (Divide and Conquer)

| 步骤 | 说明 |
|------|------|
| Divide | 把大问题分解为同类小问题 |
| Conquer | 递归解决子问题 |
| Combine | 合并子问题的解 |

| 算法 | 分解方式 |
|------|----------|
| [[sorting-algorithms\|归并排序]] | 二分数组 |
| [[sorting-algorithms\|快速排序]] | 按 pivot 划分 |
| 二分查找 | 折半 |
| Strassen 矩阵乘法 | 7 个子矩阵 |
| FFT | 奇偶分解 |

## 贪心算法 (Greedy)

每一步做**当前看起来最优**的选择，不回溯。

| 问题 | 贪心策略 |
|------|----------|
| Dijkstra 最短路径 | 选择最近的未处理节点 |
| Huffman 编码 | 合并频率最低的两棵树 |
| Activity Selection | 选择最早结束的活动 |
| 最小生成树 (Kruskal/Prim) | 选最小权边 |

**贪心不一定最优**（背包问题贪心不如 DP），但正确时通常极快。

## 回溯法 (Backtracking)

**尝试所有可能**，剪枝排除无望的分支。

```python
def backtrack(state):
    if is_solution(state):
        record(state)
        return
    for choice in candidates(state):
        if is_valid(choice):
            make_choice(state, choice)
            backtrack(state)
            undo_choice(state, choice)
```

| 问题 | 类型 |
|------|------|
| N 皇后 | 经典回溯 |
| 数独求解器 | 精确覆盖 + 回溯 |
| 全排列 | 组合构造 |
| 子集问题 | 选/不选 |

## 分支限界 (Branch and Bound)

回溯 + 上下界估计——**curse + bound 剪枝**。

```
if lower_bound(current) ≥ global_best:
    prune  # 不可能比已有解更好
```

| 应用 |
|------|
| 0-1 背包精确解 |
| TSP (旅行商问题) |
| 任务分配问题 |

## 双指针/滑动窗口

| 技术 | 描述 | 案例 |
|------|------|------|
| 双指针 | 左右指针向中间或同向移动 | 反转数组、两数之和、快速排序划分 |
| 滑动窗口 | 维护可变大小的窗口 | 最长无重复子串、子数组和 |

## 前缀和

```python
prefix[i] = sum(arr[0..i])
# 任意区间和：sum(arr[i..j]) = prefix[j] - prefix[i-1]
```

O(1) 查询任意区间和，O(n) 预处理。扩展到二维（矩阵区域和）。

## 位运算技巧

| 操作 | 代码 |
|------|------|
| 判断奇数 | `n & 1` |
| 除去最低位 1 | `n & (n-1)` |
| 获取最低位 1 | `n & -n` |
| 异或去重 | `a ^ a = 0, a ^ 0 = a` |
| 交换两数 | `a ^= b; b ^= a; a ^= b` |

→ 位掩码常用于：权限管理、状态压缩 DP、布隆过滤器

## 关系

- [[dynamic-programming]]
- [[sorting-algorithms]]
- [[tree-structures]]
- [[graph-theory]]
