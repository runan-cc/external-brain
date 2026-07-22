---
title: 字符串匹配算法
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [algorithm, string, search]
sources: []
confidence: high
---

# 字符串匹配算法

## 定义

字符串匹配问题：给定文本 T 和模式串 P，在 T 中找出所有 P 的出现位置。从文本编辑器到生物信息学，这是最基础的计算问题之一。

## 算法对比

| 算法 | 预处理 | 匹配 | 空间 | 特点 |
|------|--------|------|------|------|
| Brute Force | 0 | O(n·m) | O(1) | 简单，小数据够用 |
| KMP | O(m) | O(n) | O(m) | 经典教学算法 |
| Boyer-Moore | O(m) | O(n/m) 最好 | O(k) | 实践中极快 |
| Rabin-Karp | O(m) | O(n) 期望 | O(1) | 多模式匹配 |
| Aho-Corasick | O(m·k) | O(n) | O(m·k) | 多模式 Trie + 失败指针 |
| Z-Algorithm | O(m) | O(n+m) | O(n+m) | 简洁方便 |

## KMP (Knuth-Morris-Pratt)

核心思想：**利用已匹配的信息跳过无用比较**。

```python
def kmp(text, pattern):
    lps = compute_lps(pattern)  # Longest Prefix Suffix
    i = j = 0
    while i < len(text):
        if text[i] == pattern[j]:
            i += 1; j += 1
            if j == len(pattern):
                return i - j  # found
        elif j > 0:
            j = lps[j-1]      # 跳过！
        else:
            i += 1
```

`lps[i]` = 模式串 P[0..i] 的最长相同前后缀长度。

| pattern | lps |
|---------|-----|
| "aaaa"  | [0,1,2,3] |
| "abab"  | [0,0,1,2] |
| "abc"   | [0,0,0] |

## Boyer-Moore

KMP 的反向思维：**从右向左匹配**，利用坏字符和好后缀规则，大幅跳过。

- 对英语文本通常 O(n/m)，越长的 pattern 越快
- 许多实际 `grep`、浏览器 `Ctrl+F` 使用

## 多模式匹配：Aho-Corasick

Trie（前缀树）+ 失败指针（类似 KMP 的 lps）：
- 预处理所有模式到 Trie 中
- 文本扫一遍，同时匹配所有模式
- 网络入侵检测 (Snort)、DNA 序列分析、垃圾过滤

## 模糊匹配

| 算法 | 误差 | 复杂度 |
|------|------|--------|
| Levenshtein Distance | 插入/删除/替换 | O(n·m) DP |
| Hamming Distance | 只允许替换 | O(n) |
| Damerau-Levenshtein | +相邻字符交换 | O(n·m) |
| Needleman-Wunsch | 全局对齐，gap 处罚 | O(n·m) 生物信息 |

## 正则表达式匹配

见 [[regular-expressions]]——底层实现通常用 NFA/DFA 模拟。

## 关系

- [[regular-expressions]]
- [[dynamic-programming]] — 编辑距离 / 模糊匹配
