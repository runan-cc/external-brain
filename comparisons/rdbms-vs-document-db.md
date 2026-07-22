---
title: 关系型数据库 vs 文档型数据库
created: 2026-07-22
updated: 2026-07-22
type: comparison
tags: [comparison, database]
sources: []
confidence: high
---

# 关系型数据库 vs 文档型数据库

## 比什么

RDBMS (如 [[postgresql]]) vs Document DB (如 MongoDB)：两种最常用的数据库模型，区别在于数据模型、查询方式和扩展策略。

## 比较

| 维度 | RDBMS (关系型) | Document DB (文档型) |
|------|---------------|---------------------|
| 数据模型 | 表 (Table) — 行和列 | 集合 (Collection) — JSON 文档 |
| Schema | 严格（先定义后使用） | 灵活（Schema-on-read） |
| 关系 | JOIN（原生强支持） | 嵌套文档 / 手动查找 |
| 查询语言 | SQL（标准） | 专有查询 API |
| 事务 | ACID（全支持） | MongoDB 4.0+ 多文档事务（有性能代价） |
| 扩展 | 垂直为主，水平分库复杂 | 原生水平扩展（Sharding） |
| 一致性 | 强一致 | 可配置（最终/强一致） |
| 索引 | B-Tree, GIN, GiST, BRIN 等 | B-Tree, 复合, 文本, 地理空间 |
| 最佳场景 | 结构化、关系复杂、需要 JOIN | Schema 灵活、文档嵌套、快速迭代 |

## 选择指南

| 场景 | 推荐 |
|------|------|
| 数据结构清晰稳定 | RDBMS |
| 需求频繁变化、敏捷开发 | Document DB |
| 复杂查询、报表、JOIN | RDBMS |
| 数据是自然的 JSON 文档 | Document DB |
| 需要强事务 ACID | RDBMS（或 MongoDB 的事务模式下也可） |
| 极高写入吞吐 | Document DB（原生分片） |
| 数据分析/SQL 生态 | RDBMS |
| 微服务、每个服务独立 DB | 看具体服务需求 |

## 现代趋势

- **PostgreSQL JSONB** 模糊了界限：RDBMS 吃掉了文档 DB 的功能
- **MongoDB ACID** 模糊了反向界限：文档 DB 引入事务
- **多模型数据库**：一个数据库支持多种模型（ArangoDB, Cosmos DB）

## 总结

"不要因为觉得新潮就用 NoSQL/SQL。"用最合适的工具。PostgreSQL 能处理大部分需求——选它作为默认值，需要特殊能力时再引入专用。

## 相关

- [[sql-vs-nosql]]
- [[postgresql]]
- [[sql]]
