---
title: Distributed Consensus
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [distributed, algorithm, architecture]
sources: []
confidence: high
---

# 分布式共识 (Distributed Consensus)

## 定义

分布式共识是**多个节点就某个值达成一致**的过程。它是复制状态机的基础——所有分布式数据库、协调服务和区块链都依赖共识算法。

## FLP 不可能定理

> 在异步系统中，即使只有一个节点可能故障，也不存在**确定性**的共识算法能在有限时间内完成。

注意："异步"意味着消息延迟无上限（互联网就是异步的）。FLP 说不存在**绝对保证**终止的共识算法——但实践中可通过超时、随机化等方式在概率上可行。

## 核心算法

### Paxos (Leslie Lamport, 1989/1998)

| 角色 | 职责 |
|------|------|
| Proposer | 提出 proposal |
| Acceptor | 投票接受/拒绝 proposal |
| Learner | 学习已达成共识的值 |

**两阶段：**
1. **Prepare/Promise**：Proposer 发 prepare(n)，Acceptor 承诺不接受 < n 的 proposal
2. **Accept/Accepted**：Proposer 发 accept(n, v)，多数 Acceptor 接受 → 共识达成

问题：理解困难，工程化复杂（Paxos Made Simple 实际上并不"simple"）。

### Raft (Ongaro, 2014)

**目标：可理解性 > 性能。** 已成为分布式系统的标准共识算法。

| 概念 | 说明 |
|------|------|
| Leader | 处理所有客户端请求，发 log 给 Follower |
| Follower | 被动复制 Leader 的 log |
| Candidate | 选举期间的临时状态 |
| Term | 逻辑时钟，每次选举递增 |
| Log Entry | `(term, index, command)` |
| Committed | 被多数节点复制的 entry，保证不丢失 |

**Leader 选举：**
```
Follower 超时 → 变 Candidate → term++
→ 请求投票（RequestVote）→ 获多数票 → 成为 Leader
→ 发送心跳（AppendEntries）维持 Leader 地位
```

**日志复制：**
```
Leader 收到写 → 追加到本地 log → 发送给所有 Follower
→ 多数确认 → commit → 通知 Follower commit → 响应客户端
```

### Zab (ZooKeeper Atomic Broadcast)
ZooKeeper 的共识协议，类似 Raft 但更早。

## 共识算法的应用

| 应用 | 共识算法 |
|------|----------|
| etcd (Kubernetes) | Raft |
| Consul | Raft |
| ZooKeeper | Zab |
| TiKV (TiDB) | Raft |
| CockroachDB | Raft |
| MongoDB (replica set) | Raft（自研变体） |
| Bitcoin | PoW（工作量证明） |
| Ethereum (PoS) | Gasper (Casper FFG + LMD-GHOST) |

## 关系

- [[cap-theorem]] — 共识算法实现 CP 系统
- [[distributed-systems]]
- [[kubernetes]] — etcd (Raft) 是 k8s 的大脑
