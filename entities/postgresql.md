---
title: PostgreSQL
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [database, postgresql, sql, devops]
sources: []
confidence: high
---

# PostgreSQL

## 概览

PostgreSQL（简称 PG）是全球最先进的**开源关系型数据库**。由 Michael Stonebraker 于 1986 年在 UC Berkeley 启动。以严格遵循标准、扩展性和可靠性著称，是开发者最喜爱的数据库。

## 核心特性

| 特性 | 说明 |
|------|------|
| ACID 事务 | 完整支持，见 [[acid-transactions]] |
| MVCC | 无锁并发，读写不阻塞 |
| JSONB | 文档存储 + 索引，媲美 MongoDB |
| Full-Text Search | 内置全文搜索（可替代 Elasticsearch 小场景） |
| PostGIS | 地理空间数据扩展 |
| Extensions | 插件系统（pgvector, TimescaleDB, Citus） |

## PG vs MySQL

| 维度 | PostgreSQL | MySQL |
|------|-----------|-------|
| 标准遵循 | 严格 | 松散 |
| 并发 | MVCC（更好） | MVCC + 锁 |
| JSON | JSONB（更优） | JSON |
| 扩展性 | 极强（Extension） | 较弱 |
| 默认用户 | postgres | root |
| 适合场景 | 复杂查询、分析 | 简单读写、传统 Web |

## 关键概念

- **VACUUM**：清理死元组，回收空间（PG 特有的维护操作）
- **WAL (Write-Ahead Log)**：先写日志再写数据，保证持久性
- **Tablespace**：物理存储管理
- **Role**：用户 + 组的统一概念
- **Partitioning**：表分区（Range, List, Hash）
- **Connection Pooling**：PgBouncer（外置）或内置连接池

## 生态扩展

| 扩展 | 用途 |
|------|------|
| pgvector | [[embedding]] 向量存储 |
| PostGIS | 地理信息系统 |
| TimescaleDB | 时序数据 |
| Citus | 水平分片（分布式） |
| pg_stat_statements | 查询性能分析 |

## 关系

- [[sql]]
- [[acid-transactions]]
- [[sql-vs-nosql]]
