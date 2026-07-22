---
title: 数据库索引详解
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [database, index, performance, sql]
sources: []
confidence: high
---

# 数据库索引详解

## 定义

数据库索引是**加速数据检索的辅助数据结构**——类似书的目录，让数据库不用扫描全表就能找到需要的行。索引是数据库性能优化的第一利器。

## B+Tree 索引（默认）

大多数数据库的默认索引类型：

```
        [30 | 70]                 ← 内部节点（只存 key）
       /    |    \
  [10|20] [40|50|60] [80|90]     ← 更多内部节点
  / |  \     ...       ...        ← 叶子节点链接
[→|→|→]←→[→|→]←→[→|→|→]        ← 叶子：key+data+链表
```

| 特性 | B+Tree |
|------|--------|
| 范围查询 | ✅ 优秀（叶子链表） |
| 等值查询 | ✅ O(log n) |
| 前缀匹配 (LIKE 'abc%') | ✅ |
| 排序 | ✅ 天然有序 |
| 插入/删除 | O(log n)，可能分裂/合并 |

## 索引类型

### 聚簇索引 (Clustered) vs 非聚簇索引

| 维度 | 聚簇索引 | 非聚簇索引 |
|------|---------|-----------|
| 数据存储 | 索引叶子 = 数据行本身 | 索引叶子 = 指向数据的指针 |
| 每表数量 | 1 个（MySQL InnoDB） | 多个 |
| 查找路径 | 索引 → 直接拿到数据 | 索引 → 回表 → 数据 |
| 空间 | 数据即索引 | 额外空间 |

MySQL InnoDB：PRIMARY KEY = 聚簇索引。没有显式 PK，用第一个 UNIQUE 或内部 `row_id`。

### 覆盖索引 (Covering Index)

查询需要的列**全部在索引中** → 不回表。

```sql
-- 索引: (user_id, created_at)
SELECT user_id, created_at FROM orders WHERE user_id = 5;
-- 不需要回表！直接从索引读取。
```

### 复合索引与最左前缀

```sql
CREATE INDEX idx_a_b_c ON t (a, b, c);

-- 用到索引:
WHERE a = 1               -- ✅ a
WHERE a = 1 AND b = 2     -- ✅ a,b
WHERE a = 1 AND b > 2     -- ✅ a,b (范围后断)
WHERE a = 1 AND c = 3     -- ✅ a (c 不能跳过 b)

-- 不用索引:
WHERE b = 2               -- ❌ 跳过 a
WHERE c = 3               -- ❌ 跳过 a,b
```

### 其他索引类型

| 类型 | 数据库 | 用途 |
|------|--------|------|
| Hash Index | PG, MySQL Memory | 等值查询 ❌ 范围查询 |
| GIN | PG | 全文搜索、JSONB、数组 |
| GiST | PG | 几何、全文、自定义 |
| BRIN | PG | 大表的顺序数据块摘要 |
| Bitmap Index | Oracle | 低基数列（性别、状态） |
| Spatial (R-Tree) | PG/MySQL | 地理空间查询 |

## JOIN 算法

| 算法 | 原理 | 条件 |
|------|------|------|
| Nested Loop | 外层每行 × 内层扫描 | 任意（最朴素） |
| Block Nested Loop | 批量外层 + 内层扫描 | 无合适索引 |
| **Index Nested Loop** | 外层每行 × 内层索引用 | ✅ 内层 JOIN 列有索引 |
| **Hash Join** | 用哈希表匹配 | 等值连接 (PG 9.2+, MySQL 8.0+) |
| Merge Join | 两支边排序各自归并 | 二者都有序（ORDER/GROUP 用） |

> 经验：等值 JOIN 优先期望 Hash Join；有索引时 Index Nested Loop 也很快。

## 索引不好的副用

| 问题 | 说明 |
|------|------|
| 写放大 | 每个 INSERT/UPDATE/DELETE 都要更新索引 |
| 空间占用 | 索引也是数据（可能超过原始数据） |
| 查询计划错误 | 优化器可能选错索引 |
| 碎片 | B+Tree 更新导致页分裂，需 REINDEX |

## 索引设计原则

1. **WHERE / JOIN / ORDER BY / GROUP BY 列优先加索引**
2. **高选择性的列优先**（性别→低，用户 ID→高）
3. **多用覆盖索引避免回表**
4. **不要盲目给每个列加索引**
5. **用 EXPLAIN 验证索引是否被使用**

## 关系

- [[sql]]
- [[postgresql]]
- [[tree-structures]] — B+Tree
