---
title: Redis
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [database, cache, performance]
sources: []
confidence: high
---

# Redis

## 概览

Redis (Remote Dictionary Server) 是 Salvatore Sanfilippo 于 2009 年创建的**内存数据结构存储**。以极快的读写速度和丰富的数据结构著称，是目前最流行的缓存和消息代理。

## 核心特性

- **内存存储**：微秒级读写延迟（~100K ops/s 单线程）
- **数据结构丰富**：不只是 Key-Value
- **持久化**：RDB 快照 + AOF 日志
- **主从复制 + Sentinel/Cluster**
- **Lua 脚本**：原子性执行

## 数据结构

| 数据结构 | 命令 | 应用 |
|----------|------|------|
| String | `SET/GET/INCR` | 缓存、计数器 |
| Hash | `HSET/HGET/HGETALL` | 对象存储 |
| List | `LPUSH/RPOP` | 消息队列、时间线 |
| Set | `SADD/SINTER/SUNION` | 标签、共同好友 |
| Sorted Set | `ZADD/ZRANGEBYSCORE` | 排行榜、延迟队列 |
| Stream | `XADD/XREAD/XREADGROUP` | 消息队列（Kafka 替代） |
| HyperLogLog | `PFADD/PFCOUNT` | 基数统计 |
| Bitmap | `SETBIT/BITCOUNT` | 签到、布隆过滤器 |
| Geospatial | `GEOADD/GEORADIUS` | 附近的人 |

## 应用场景

| 场景 | 实现 |
|------|------|
| 缓存 | 热点数据、会话存储 (session) |
| 分布式锁 | `SET lock NX EX 10` |
| 限流 | 滑动窗口 (Sorted Set) / 令牌桶 (List) |
| 实时排行榜 | Sorted Set |
| 消息队列 | List / Stream + Consumer Group |
| 附近的人 | Geo 命令 |

## 持久化与高可用

| 方式 | 特点 |
|------|------|
| RDB | 定时快照，恢复快，可能丢数据 |
| AOF | 追加每条写命令，更安全但文件大 |
| RDB + AOF | 混合使用 |
| Sentinel | 自动故障转移 |
| Cluster | 数据分片到 16384 个 slot |

## 常见陷阱

- **内存满了怎么办？** — 配置 maxmemory + 淘汰策略 (LRU/LFU)
- **缓存穿透** — 大量查询不存在的数据 → 布隆过滤器 / 缓存空值
- **缓存雪崩** — 大量缓存同时过期 → 随机 TTL
- **热 Key 问题** — 一个 key 被疯狂访问 → 本地缓存 / 多副本
- **Big Key** — 大 key 导致阻塞 → 拆分 / UNLINK 异步删除

## 关系

- [[postgresql]] — Redis 缓存 + PG 持久化
- [[distributed-systems]] — Sentinel/Cluster 是分布式
