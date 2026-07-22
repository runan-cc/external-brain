---
title: Kafka
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [messaging, distributed, streaming]
sources: []
confidence: high
---

# Kafka

## 概览

Apache Kafka 是 LinkedIn 于 2011 年开源的**分布式流处理平台**，由 Jay Kreps 等人创建。它不是传统消息队列，而是**分布式提交日志**——以极高的吞吐量和持久性著称，是现代数据管道的核心基础设施。

## 架构

```
Producer ──→ [Broker 1] [Broker 2] [Broker 3] ──→ Consumer
                ↓           ↓           ↓
             Partition  Partition  Partition
             (有序日志)  (有序日志)  (有序日志)
```

## 核心概念

| 概念 | 说明 |
|------|------|
| Topic | 消息的逻辑分类 |
| Partition | Topic 的物理分片，有序、不可变 |
| Offset | 消息在 Partition 中的唯一序号 |
| Producer | 写入消息 |
| Consumer | 读取消息 |
| Consumer Group | 组内每个 partition 只有一个消费者 |
| Broker | Kafka 服务器节点 |
| Zookeeper / KRaft | 集群元数据管理 |

## 关键特性

- **持久化到磁盘**：消息写入后不删除，按时间/大小策略保留
- **顺序 I/O**：追加写 + 分段读，接近物理磁盘极限
- **零拷贝 (Zero-Copy)**：`sendfile()` 系统调优，减少 CPU 参与
- **水平扩展**：增加 Partition 和 Broker
- **消息回放**：任意重置 Offset 重新消费

## 应用场景

| 场景 | 模式 |
|------|------|
| 日志聚合 | 所有服务日志 → Kafka → ElasticSearch |
| 事件溯源 | 所有状态变化作为事件流 |
| 流计算 | Kafka Streams / Flink 实时处理 |
| CDC (Change Data Capture) | 数据库变更 → Kafka → 下游 |
| 消息队列 | 替代 RabbitMQ 高吞吐场景 |
| Metrics 收集 | 监控数据管道 |

## 关键配置

| 参数 | 说明 |
|------|------|
| `acks=all` | 所有 ISR 确认后才认为写入成功 |
| `min.insync.replicas` | 最少同步副本数 |
| `retention.ms` | 消息保留时间 |
| `compression.type` | 消息压缩类型 |
| `enable.idempotence` | 幂等 Producer，防止重复 |

## 关系

- [[message-queue]]
- [[distributed-systems]]
- [[distributed-consensus]] — KRaft 替代 ZK
