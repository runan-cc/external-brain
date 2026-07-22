---
title: SQL vs NoSQL
created: 2026-07-22
updated: 2026-07-22
type: comparison
tags: [comparison, database, architecture]
sources: []
confidence: high
---

# SQL vs NoSQL

## 比什么

两种数据库范式：关系型（SQL）和非关系型（NoSQL）。选择直接影响数据建模、查询方式和扩展策略。

## 比较

| 维度 | SQL (关系型) | NoSQL (非关系型) |
|------|-------------|-----------------|
| 数据结构 | 表 (行×列)，严格 Schema | 文档/键值/图/列族，灵活 Schema |
| 查询语言 | SQL (声明式，标准) | 各自专有 API |
| ACID 事务 | ✅ 强支持 | ⚠️ 部分支持 (MongoDB 4.0+) |
| 扩展方式 | 垂直扩展为主 | 水平扩展为主（分片） |
| JOIN | ✅ 原生 JOIN | ❌ 需应用层 JOIN |
| 一致性 | 强一致性 (ACID) | 最终一致性 (BASE) |
| 性能 | 复杂查询优化更好 | 简单读写更快 |

## 主流选择

| 数据库 | 类型 | 适合场景 |
|--------|------|----------|
| PostgreSQL | SQL | 全能型，最推荐的关系型 |
| MySQL | SQL | Web 应用传统选择 |
| SQLite | SQL | 嵌入式/移动端/单机 |
| MongoDB | 文档型 | 灵活 Schema，JSON 数据 |
| Redis | 键值/缓存 | 极快读写，缓存/消息队列 |
| Cassandra | 宽列 | 高写入吞吐，时序数据 |
| Neo4j | 图 | 社交关系、推荐系统 |

## 选择指南

| 场景 | 推荐 |
|------|------|
| 数据关系复杂，需要 JOIN | SQL |
| Schema 不稳定/频繁变更 | NoSQL (文档型) |
| 需要强事务一致性 | SQL |
| 高并发简单读写 | NoSQL |
| 数据分析/报表 | SQL |
| 图关系分析 | Neo4j 等图数据库 |

## 现代趋势

- **PostgreSQL** 一家通吃：JSONB 支持文档存储，时序扩展，全文搜索
- **NewSQL**：TiDB、CockroachDB 等，在保持 SQL 语义的同时实现水平扩展
- **多模型数据库**：一个数据库支持多种数据模型

## 总结

不要教条。当 PostgreSQL 能覆盖 90% 需求时，它就是正确答案。只有明确需要 NoSQL 特性时才引入额外复杂度。

## 相关

- [[postgresql]]
- [[mongodb]]
- [[redis]]
