---
title: 分布式系统
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [distributed, architecture, systems]
sources: []
confidence: high
---

# 分布式系统

## 定义

分布式系统是**通过网络连接的多个独立计算机**协同工作，对外表现为单一系统的集合。互联网、云服务、区块链都是分布式的实例。

## 为什么需要分布式

| 原因 | 说明 |
|------|------|
| 扩展性 (Scalability) | 单机能力有上限，需横向扩展 |
| 容错 (Fault Tolerance) | 单机故障不影响整体服务 |
| 地理分布 | 全球用户需要就近访问 |
| 成本 | 多台廉价机器 > 一台超级计算机 |

## 核心挑战

### 时钟与时间
分布式节点之间没有全局时钟，NTP 同步有误差。
- **逻辑时钟 (Lamport Clock)**：通过消息传递推导偏序关系
- **向量时钟 (Vector Clock)**：检测因果关系和并发冲突

### 一致性模型

| 模型 | 保证 | 性能 |
|------|------|------|
| 强一致性 (Linearizability) | 写立即对所有读者可见 | 低 |
| 顺序一致性 (Sequential) | 所有操作看起来按某全局顺序 | 中 |
| 因果一致性 (Causal) | 因果关系被遵守 | 中高 |
| 最终一致性 (Eventual) | 最终会一致 | 高 |

### 分布式事务
跨多个数据节点的 ACID 事务：
- **2PC (Two-Phase Commit)**：Prepare → Commit，阻塞协议
- **3PC**：2PC + 超时避免阻塞，但引入新问题
- **Saga**：长事务拆为小事务+补偿

## 故障模式

| 故障类型 | 说明 |
|----------|------|
| Crash-stop | 节点崩溃再也不恢复 |
| Crash-recovery | 崩溃后恢复（最实际） |
| Omission | 消息丢失/延迟 |
| Byzantine | 任意恶意行为（最难处理） |

## 关键模式

| 模式 | 说明 |
|------|------|
| 复制 (Replication) | 数据复制到多节点（主从、多主、无主） |
| 分片 (Sharding) | 数据按规则分布到不同节点 |
| 领导人选举 | 见 [[distributed-consensus]] |
| Gossip 协议 | 节点随机交换信息，最终一致（Cassandra, Consul） |
| Quorum | 读/写需多数节点确认（R + W > N） |

## 关系

- [[cap-theorem]]
- [[distributed-consensus]]
- [[acid-transactions]]
- [[kubernetes]]
