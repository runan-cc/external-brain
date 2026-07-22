---
title: SQL (Structured Query Language)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [database, language, query]
sources: []
confidence: high
---

# SQL (Structured Query Language)

## 定义

SQL 是操作关系型数据库的标准声明式语言，1974 年由 IBM 提出。它描述"想要什么"而非"怎么做"，是目前最广泛使用的数据库查询语言。

## 核心分类

### DDL (Data Definition Language)
```sql
CREATE TABLE users (id INT PRIMARY KEY, name TEXT);
ALTER TABLE users ADD COLUMN email TEXT;
DROP TABLE users;
```

### DML (Data Manipulation Language)
```sql
SELECT * FROM users WHERE age > 18 ORDER BY name;
INSERT INTO users VALUES (1, 'Alice');
UPDATE users SET email = 'a@b.com' WHERE id = 1;
DELETE FROM users WHERE id = 1;
```

### DCL (Data Control Language)
```sql
GRANT SELECT ON users TO analyst;
REVOKE DELETE ON users FROM analyst;
```

## 关键概念

| 概念 | 说明 |
|------|------|
| JOIN | 合并多表数据 (INNER, LEFT, RIGHT, FULL, CROSS) |
| Index | 加速查询，B-tree / Hash / GIN / GiST |
| Transaction | ACID 保证：Atomicity, Consistency, Isolation, Durability |
| View | 虚拟表，封装复杂查询 |
| Window Function | `ROW_NUMBER()`, `RANK()`, `LAG()` 等分析函数 |
| CTE | `WITH ... AS ()` 公共表表达式，提升可读性 |

## 主流数据库方言

| 数据库 | SQL 方言 |
|--------|----------|
| PostgreSQL | PL/pgSQL |
| MySQL | MySQL SQL |
| SQLite | 最小化方言 |
| SQL Server | T-SQL |

## 相关概念

- [[sql-vs-nosql]]
- [[postgresql]]
- [[acid-transactions]]
