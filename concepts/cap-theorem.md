---
title: CAP Theorem
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [distributed, database, architecture, theorem]
sources: []
confidence: high
---

# CAP 定理

## 定义

CAP 定理（Brewer's Theorem）由 Eric Brewer 于 2000 年提出，是分布式系统理论的基本约束：

> 分布式系统中，**一致性（C）、可用性（A）、分区容错性（P）** 三者最多只能同时满足两个。

## 三个属性

| 属性 | 含义 | 违反的后果 |
|------|------|-----------|
| **C**onsistency（一致性） | 所有节点在同一时刻看到相同数据 | 读到旧数据 |
| **A**vailability（可用性） | 每个请求都得到非错误的响应 | 请求失败/超时 |
| **P**artition Tolerance（分区容错） | 网络分区时系统继续工作 | 系统不可用 |

## 不可能三角

```
       C (一致性)
       /\
      /  \
     /    \
    /  ?   \
   /________\
  A          P
(可用性)    (分区容错)

你只能选两个：CP 或 AP（P 不能放弃）
```

**为什么 P 不能放弃？** 在分布式系统中，网络分区不可避免。放弃 P 意味着网络一断就整体不可用——不可接受。所以实际选择是 **CP** 或 **AP**。

## CP 系统（一致性 + 分区容错）

网络分区时：牺牲可用性，保证数据一致。

| 系统 | 说明 |
|------|------|
| ZooKeeper | 强一致性协调服务 |
| etcd | Kubernetes 配置存储 |
| HBase | 列族数据库 |
| MongoDB（默认）| 单 primary 写入 |

## AP 系统（可用性 + 分区容错）

网络分区时：允许临时不一致，保证服务可用。

| 系统 | 说明 |
|------|------|
| Cassandra | 最终一致性 |
| DynamoDB | 可配置最终/强一致性 |
| CouchDB | 最终一致性 |
| Riak | 高可用 KV 存储 |

## CA 系统

单机数据库（MySQL, PostgreSQL）——没有分布式，所以天然满足 CA。一旦分布式部署（主从复制），**网络分区时就变成了 CP 或 AP**。

## PACELC 扩展

CAP 没有考虑**无分区时的权衡**。PACELC 定理补充：

> **P**artition: choose **A**vailability or **C**onsistency  
> **E**lse: choose **L**atency or **C**onsistency

没有分区时，也要在延迟和一致性间权衡。

## 实践中的 CAP

> CAP 是光谱，不是开关。

- PostgreSQL 主从：正常情况下 CA，主从切换时短暂 CP
- Cassandra：tuneable consistency（可调写/读 quorum 达到不同 CAP 平衡）
- Spanner (Google)：通过 TrueTime (原子钟) 实现"外部一致"，接近 CAP 的突破

## 关系

- [[acid-transactions]] — ACID 是单机的，CAP 是分布式的
- [[distributed-consensus]] — Raft/Paxos 实现 CP
- [[sql-vs-nosql]]
