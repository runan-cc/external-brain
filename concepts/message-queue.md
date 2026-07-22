---
title: 消息队列
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [messaging, distributed, architecture]
sources: []
confidence: high
---

# 消息队列 (Message Queue)

## 定义

消息队列是**异步通信**的中间件——生产者发送消息，消费者接收处理。它解耦了服务之间的直接调用，提供缓冲、削峰和可靠性保证。

## 为什么需要 MQ

| 问题 | MQ 答案 |
|------|---------|
| 服务间直接调用耦合严重 | 生产者不直接调消费者 |
| 流量尖峰打垮下游 | MQ 缓冲削峰填谷 |
| 下游故障导致请求丢失 | MQ 持久化、重试 |
| 响应太慢 | 异步处理，立即返回 |
| 一对多消费 | Pub/Sub 广播 |

## 核心概念

| 概念 | 说明 |
|------|------|
| Producer | 发送消息 |
| Consumer | 接收并处理消息 |
| Broker | 中间人，管理消息传递 |
| Queue | 点对点：一条消息一个消费者 |
| Topic | 发布-订阅：一条消息多个消费者 |
| Partition | Kafka 分片，并行消费 |
| Consumer Group | 同一组内每个 partition 只分配给一个消费者 |
| Offset | 消费位置标记 |

## 消息投递保证

| 语义 | 含义 |
|------|------|
| At most once | 可能丢，不重复（最快） |
| At least once | 不丢，可能重复（需幂等处理） |
| Exactly once | 不丢不重（最复杂，有性能代价） |

## 主流 MQ

### Kafka
- **日志型**：消息持久化到磁盘，顺序读写极快
- 高吞吐（百万 msg/s），适合流处理和数据管道
- Partition + Consumer Group 实现并行
- 主要场景：日志聚合、事件溯源、流计算

### RabbitMQ
- **队列型**：消息投递后删除
- AMQP 协议标准，路由灵活（Exchange/Binding/Routing Key）
- 适合：任务分发、RPC、应用解耦
- 比 Kafka 更"传统"的 MQ

### 对比

| 维度 | Kafka | RabbitMQ |
|------|-------|----------|
| 吞吐量 | 百万/秒 | 万/秒 |
| 消息持久化 | 默认持久化到磁盘 | 可选持久化 |
| 消息回放 | ✅ 支持 | ❌ |
| 协议 | 自研 | AMQP, MQTT, STOMP |
| 路由 | 简单（Topic） | 丰富（Exchange 类型） |
| 延时 | ~2ms | <1ms |
| 适合 | 大数据流、Event Sourcing | 任务队列、RPC |

## 关键问题

| 问题 | 处理方式 |
|------|----------|
| 重复消费 | 幂等设计（唯一 ID 去重） |
| 消息丢失 | ACK + 持久化 + 多副本 |
| 消息积压 | 增加 Partition/Consumer、临时扩容 |
| 顺序消费 | 同一 key → 同一 Partition |
| 死信队列 (DLQ) | 处理失败的消息隔离分析 |

## 关系

- [[distributed-systems]]
- [[cap-theorem]] — Kafka 是 CP 还是 AP？
- [[ci-cd]] — MQ 是微服务架构的神经系统
