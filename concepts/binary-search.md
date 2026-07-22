---
title: Binary Search & Search Algorithms
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [algorithm, search, optimization]
sources: []
confidence: high
---

# 二分查找与搜索算法

## 二分查找 (Binary Search)

### 基本形式

```python
def binary_search(arr, target):
    lo, hi = 0, len(arr) - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        if arr[mid] == target: return mid
        elif arr[mid] < target: lo = mid + 1
        else: hi = mid - 1
    return -1
```

| 特性 | 值 |
|------|-----|
| 复杂度 | O(log n) |
| 前提 | 有序数组 |
| 比较次数 | ⌊log₂ n⌋ + 1 |

### 关键变体

```python
# 第一个 ≥ target 的位置 (lower_bound)
while lo < hi:
    mid = (lo + hi) // 2
    if arr[mid] < target: lo = mid + 1
    else: hi = mid

# 第一个 > target 的位置 (upper_bound)
while lo < hi:
    mid = (lo + hi) // 2
    if arr[mid] <= target: lo = mid + 1
    else: hi = mid
```

> ⚠️ 90% 的二分查找 bug 出自边界条件。推荐用 `[lo, hi)` 半开区间统一思路。

### 应用（不只是找数字）

| 应用 | 搜索空间 |
|------|----------|
| 平方根 | `square(x)` 在 `[0, x]` 上二分 |
| 二分答案 | "最小的能使条件成立的 X" |
| 无序数组峰值 | 局部极大值 O(log n) |
| 旋转排序数组 | 旋转点 + 二分 |
| 两个有序数组的中位数 | 二分较短数组 |

## 二分答案（Binary Search on Answer）

```python
# "分割数组使最大和最小" → 二分这个最小值
l, r = max(arr), sum(arr)
while l < r:
    mid = (l + r) // 2
    if can_split(arr, mid, k):
        r = mid  # 可以更小
    else:
        l = mid + 1
return l
```

## A* 搜索

[[graph-theory]] 的智能搜索：`f(n) = g(n) + h(n)`

- **g(n)**：起点到 n 的实际代价
- **h(n)**：n 到终点的**启发式估计**（不能高估，否则不保证最优）

| 场景 | 启发式 h(n) |
|------|------------|
| 网格寻路 | 曼哈顿距离 / 欧氏距离 |
| 拼图 (15-puzzle) | 曼哈顿距离和 |
| 导航 | 直线距离 |

> Dijkstra = A* with h(n) = 0

## 三分查找

求单峰函数极值的 O(log n) 算法（二分是单调函数）。

## 其他搜索算法

| 算法 | 场景 | 复杂度 |
|------|------|--------|
| 指数搜索 | 无界有序空间 | O(log n) |
| 插值搜索 | 均匀分布数据 | O(log log n) 平均 |
| 跳表搜索 | Skip List | O(log n) |
| 双调搜索 | 双调序列（先增后降） | O(log n) |

## 关系

- [[sorting-algorithms]] — 二分搜索需要有序数据
- [[graph-theory]] — A* / Dijkstra
- [[algorithmic-paradigms]] — 分治
