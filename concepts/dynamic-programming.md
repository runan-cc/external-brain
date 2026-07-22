---
title: 动态规划
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [algorithm, technique, optimization]
sources: []
confidence: high
---

# 动态规划 (Dynamic Programming)

## 定义

动态规划（DP）是将**重叠子问题**分解并缓存结果的算法设计范式。核心思想：不问一个问题两次——用空间换时间。由 Richard Bellman 于 1950 年代提出。

## 两个必要条件

1. **最优子结构**：问题的最优解包含子问题的最优解
2. **重叠子问题**：递归过程中同一子问题被多次计算

## 两种实现方式

### Top-Down（记忆化递归）
```python
memo = {}
def fib(n):
    if n <= 1: return n
    if n not in memo:
        memo[n] = fib(n-1) + fib(n-2)
    return memo[n]
```

### Bottom-Up（迭代表格）
```python
def fib(n):
    dp = [0] * (n+1)
    dp[1] = 1
    for i in range(2, n+1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]
```

## 经典问题

| 问题 | 状态定义 | 复杂度 |
|------|----------|--------|
| 斐波那契 | `dp[i] = dp[i-1] + dp[i-2]` | O(n) |
| 0-1 背包 | `dp[i][w] = max(dp[i-1][w], val[i] + dp[i-1][w-wt[i]])` | O(nW) |
| 最长公共子序列 (LCS) | `dp[i][j] = dp[i-1][j-1]+1 or max(dp[i-1][j], dp[i][j-1])` | O(mn) |
| 编辑距离 (Levenshtein) | 类似 LCS，考虑插入/删除/替换 | O(mn) |
| 最长递增子序列 (LIS) | `dp[i] = max(dp[j] + 1) for j < i and a[j] < a[i]` | O(n²) / O(n log n) |
| 硬币找零 | `dp[i] = min(dp[i-c]+1)` | O(nm) |
| 矩阵链乘法 | `dp[i][j] = min(dp[i][k] + dp[k+1][j] + cost)` | O(n³) |

## DP 优化技巧

| 技巧 | 适用场景 |
|------|----------|
| 滚动数组 | 只需前一行/前一列，O(n) → O(1) 空间 |
| 状态压缩 | 状态可由整数位表示 |
| Monotonic Queue | dp 递推涉及区间最值 |
| 斜率优化 (CHT) | dp[i] = min(a[j]*x[i] + b[j]) |
| Divide and Conquer DP | 满足决策单调性 |

## DP vs 贪心 vs 分治

| 范式 | 重叠子问题 | 最优子结构 | 典型问题 |
|------|-----------|-----------|----------|
| DP | ✅ | ✅ | 背包、LCS |
| 贪心 | ❌ | ✅ | Dijkstra, Huffman |
| 分治 | ❌ | ✅ | 归并排序 |

## 关系

- [[data-structures-and-algorithms]]
- [[graph-theory]] — 图上的 DP
