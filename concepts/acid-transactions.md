---
title: ACID Transactions
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [database, architecture]
sources: []
confidence: high
---

# ACID Transactions（ACID 事务）

## 定义

ACID 是关系型数据库事务的四个核心属性，确保数据库操作在并发和故障下仍保持一致性。

## 四个属性

| 属性 | 含义 | 实现方式 |
|------|------|----------|
| **Atomicity** (原子性) | 要么全做，要么全不做 | Undo Log (回滚) |
| **Consistency** (一致性) | 事务前后数据满足所有约束 | 约束检查 + 原子性/隔离性保证 |
| **Isolation** (隔离性) | 并发事务互不干扰 | 锁 + MVCC |
| **Durability** (持久性) | 提交后即使崩溃也不丢失 | WAL (Write-Ahead Log) + Checkpoint |

## 隔离级别 (Isolation Levels)

| 级别 | 脏读 | 不可重复读 | 幻读 |
|------|------|-----------|------|
| Read Uncommitted | ✅ | ✅ | ✅ |
| Read Committed | ❌ | ✅ | ✅ |
| Repeatable Read | ❌ | ❌ | ✅/❌ (PG 中无) |
| Serializable | ❌ | ❌ | ❌ |

**脏读**：读到未提交的事务修改  
**不可重复读**：同一事务中两次读值不同（被其他事务 UPDATE）  
**幻读**：同一事务中两次范围查询结果不同（被其他事务 INSERT）

**PostgreSQL 默认 Repeatable Read，MySQL/InnoDB 默认 Repeatable Read 且通过间隙锁防幻读。**

## MVCC（多版本并发控制）

现代数据库（PostgreSQL, MySQL InnoDB）通过维护数据的多版本实现高并发：
- 读不阻塞写，写不阻塞读
- 每个事务看到的是数据的快照（snapshot）
- 通过事务 ID 和可见性规则判断哪个版本可见

## 相关概念

- [[sql]]
- [[postgresql]]
- [[sql-vs-nosql]]
