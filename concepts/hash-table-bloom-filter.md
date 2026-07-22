---
title: Hash Table & Bloom Filter
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [data-structure, hash, algorithm]
sources: []
confidence: high
---

# 哈希表与布隆过滤器

## 哈希表

### 定义

哈希表是通过**哈希函数将键映射到数组索引**的数据结构，理想情况下 O(1) 插入/删除/查找。是计算机科学中最实用的发明之一——数据库索引、缓存、集合、字典都基于它。

### 哈希函数

| 函数 | 特点 |
|------|------|
| FNV-1a | 简单快速 |
| MurmurHash3 | 分布好、非加密 |
| xxHash | 极快，大数据哈希 |
| SipHash | 防止 Hash DoS 攻击 |
| SHA-256 | 加密级（慢，不用于哈希表） |

### 碰撞解决

#### 1. 拉链法 (Separate Chaining)

```
Index 0: [K1→V1] → [K5→V5]
Index 1: [K2→V2]
Index 2: [K3→V3] → [K6→V6] → [K8→V8]
Index 3: [K4→V4]
```

每个桶是一个链表（或红黑树）。[[java]] HashMap 在桶长度 >8 时转为红黑树。

#### 2. 开放寻址法 (Open Addressing)

碰撞时找下一个空位：

| 探测 | 公式 | 问题 |
|------|------|------|
| 线性探测 | `h(k) + i` | 主聚类 (primary clustering) |
| 二次探测 | `h(k) + i²` | 次聚类 |
| 双重哈希 | `h1(k) + i·h2(k)` | ✅ 最少聚类 |

**Robin Hood Hashing**：开放寻址 + 交换算法，方差最小化。[[rust]] `HashMap` 和 [[go]] `map` 用 Swisstable（Robin Hood 变体）。

### 负载因子与扩容

| load_factor | 行为 |
|-------------|------|
| > 0.75 | 扩容 (2x)，rehash 所有元素 |
| < 0.25 | 缩容（可选） |

### 攻击：Hash DoS

攻击者构造大量碰撞 key → 所有元素落入同一桶 → O(n²) 退化。

防御：SipHash（随机种子，无法预测碰撞）、[[rust]] 默认使用、Perl 曾因此受攻击。

## 布隆过滤器 (Bloom Filter)

### 定义

布隆过滤器是**概率性的集合结构**——用极少的空间回答"元素是否可能存在于集合中"。

- **可能存在**（有误报）✅
- **确定不存在**（无误报）✅

### 结构

```
m 个位数组 + k 个哈希函数

insert("cat"):
  h1("cat")=3 → bit[3]=1
  h2("cat")=7 → bit[7]=1
  h3("cat")=11→ bit[11]=1

contains("dog"):
  h1("dog")=3 → bit[3]=1 ✓
  h2("dog")=4 → bit[4]=0 ✗  → 确定不在
```

### 误报率

$$p \approx (1 - e^{-kn/m})^k$$

| m/n | k 最优 | 误报率 |
|-----|--------|--------|
| 8 | 5 | ~2% |
| 10 | 7 | ~0.8% |
| 16 | 11 | ~0.05% |

### 应用

| 应用 | 场景 |
|------|------|
| 缓存穿透防护 | 快速拒绝不存在的 key 请求 |
| Chrome 恶意 URL 过滤 | 本地布隆过滤器，查询量巨大 |
| CDN 缓存 | 判断 URL 是否已被缓存 |
| Bigtable / HBase / RocksDB | 判断 SSTable 是否有某 key |
| 区块链轻节点钱包 | 过滤非相关交易 |

### 局限性

- **不能删除**（Counting Bloom Filter 可）
- 不能获取实际值（只能测试成员）
- 误报率随填充率升高

## 关系

- [[data-structures-and-algorithms]]
- [[redis]] — Redis 有 Bloom Filter 模块
- [[cdn]]
