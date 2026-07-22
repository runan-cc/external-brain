---
title: Sorting Algorithms
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [algorithm, sorting, optimization]
sources: []
confidence: high
---

# 排序算法 (Sorting Algorithms)

## 定义

排序算法将无序序列按某种顺序重新排列。它是计算机科学中被研究最透彻的问题之一——理解排序算法的权衡是算法设计的入门课。

## 比较排序

| 算法 | 平均 | 最坏 | 空间 | 稳定 | 特点 |
|------|------|------|------|------|------|
| Bubble Sort | O(n²) | O(n²) | O(1) | ✅ | 教学用，别生产用 |
| Insertion Sort | O(n²) | O(n²) | O(1) | ✅ | 小数据 / 近似排序时很快 |
| Selection Sort | O(n²) | O(n²) | O(1) | ❌ | 简单，交换次数少 |
| Merge Sort | O(n log n) | O(n log n) | O(n) | ✅ | 分治经典，适合链表 |
| Quick Sort | O(n log n) | O(n²) | O(log n) | ❌ | 实践中最快的通用排序 |
| Heap Sort | O(n log n) | O(n log n) | O(1) | ❌ | 原地，缓存不友好 |
| Timsort | O(n log n) | O(n log n) | O(n) | ✅ | [[python]] 和 Java 默认排序 |

## 快速排序剖析

```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    mid  = [x for x in arr if x == pivot]
    right= [x for x in arr if x > pivot]
    return quicksort(left) + mid + quicksort(right)
```

| 变体 | 策略 |
|------|------|
| 三数取中 | 选 pivot 避免最坏退化 |
| 三路快排 | 大量重复元素时 O(n) |
| 混合排序 | 小数组切插入排序（Timsort 思想） |

## 非比较排序（线性时间）

| 算法 | 复杂度 | 条件 |
|------|--------|------|
| Counting Sort | O(n + k) | 整数、范围已知 |
| Radix Sort | O(d(n + k)) | 按位分桶 |
| Bucket Sort | O(n) | 数据均匀分布 |

> 下界：比较排序的最坏复杂度**不能低于 Ω(n log n)**。但非比较排序可以突破这个下界！

## 为什么生产环境用 Timsort？

- **利用现实数据的特点**：数据往往部分有序
- 找到已排序的 run（块），对 run 进行合并
- 小 run 用二分插入排序
- 最坏 O(n log n)，最好 O(n)（已排序直接跳过）
- 稳定排序

## 选择指南

| 场景 | 推荐 |
|------|------|
| 标准库默认 | Timsort (Python/Java/Android) / Introsort (C++ std::sort) |
| 极简实现 | Quick Sort + 三数取中 |
| 链表 | Merge Sort（天然适合） |
| 原地 + 稳定 | Block Sort |
| 外部排序 | 多路归并（大文件分块排再合并） |

## 关系

- [[data-structures-and-algorithms]]
- [[dynamic-programming]]
- [[python]]
