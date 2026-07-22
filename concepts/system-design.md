---
title: 系统设计 (System Design)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [architecture, system-design, interview, scale]
sources: []
confidence: high
---

# 系统设计 (System Design)

## 定义

系统设计是**设计和规划大规模分布式系统的过程**——考虑扩展性、可用性、一致性、性能和成本。大厂面试的必考项，也是架构师的日常。

## 设计步骤

1. **澄清需求**：功能需求 vs 非功能需求（QPS、延迟要求、可用性）
2. **容量估算**：日活/DAU、QPS、存储量
3. **API 设计**：REST/GraphQL/gRPC 接口定义
4. **数据模型**：SQL vs NoSQL、表设计、索引
5. **高层架构**：画框图、确定关键组件
6. **深入细节**：瓶颈分析、扩展策略
7. **权衡总结**：为什么这样设计

## 经典系统设计题目

### 短链系统 (URL Shortener)

| 组件 | 方案 |
|------|------|
| ID 生成 | Base62 编码自增 ID / Snowflake / 预生成 |
| 存储 | ID → URL 映射（KV 最合适） |
| 缓存 | Redis，热点 URL 命中率 >99% |
| 301 vs 302 | 301 永久（浏览器缓存不计数），302 临时（每次计数） |
| 冲突处理 | 用已知唯一 ID（Snowflake、UUID v7） |

### 分布式 ID 生成器

| 方案 | 优点 | 缺点 |
|------|------|------|
| UUID v4 | 简单，无中心 | 128 位长、B-Tree 不友好 |
| UUID v7 | 时间序、B-Tree 友好 | 稍复杂 |
| Snowflake (Twitter) | 64 位、趋势递增 | 依赖时钟 |
| 号段模式 (Leaf) | 批量获取 ID 范围 | 需要号段分段 |

**Snowflake (64 位)**：
```
[41 位: 时间戳 ms] [5 位: 数据中心] [5 位: 机器] [12 位: 序列号]
```

### Rate Limiter (限流器)

| 算法 | 原理 | 特点 |
|------|------|------|
| Token Bucket | 令牌匀速生成，请求消耗令牌 | 允许突发 |
| Leaky Bucket | 请求入桶，匀速漏出处理 | 平滑 |
| Fixed Window | 每窗口 N 个请求 | 边界问题 |
| Sliding Window Log | 记录每个请求时间戳 | 精确但内存大 |
| Sliding Window Counter | 前窗口分数加权 | 近似 + 精确的平衡 |

### Feed 流系统

| 模式 | 原理 | 适合 |
|------|------|------|
| Pull (拉) | 查看时从关注的人拉取 | 粉丝少 (Instagram 早期) |
| Push (推) | 发帖时推到粉丝 inbox | 粉丝多 (Twitter) |
| Push+Pull | 名人 Push，普通人 Pull | 实际方案 (Twitter) |

### 秒杀系统 (Flash Sale)

| 策略 | 说明 |
|------|------|
| CDN 静态化 | 秒杀页面静态，减少后端 |
| 异步排队 | 请求入队，不直接打数据库 |
| Redis 库存 | 内存扣减库存，异步写回 DB |
| 限流 | 网关层+应用层双层限流 |
| 防黄牛 | 验证码、唯一 ID、设备指纹 |

## 通用扩展策略

| 策略 | 适用 |
|------|------|
| 垂直扩展 (Scale Up) | 加 CPU/内存（简单，有上限） |
| 水平扩展 (Scale Out) | 加节点（复杂，无上限） |
| 缓存 | Redis/Memcached |
| CDN | 静态资源地理分布 |
| 读写分离 | 读请求走从库 |
| 分库分表 | 数据水平拆分 |
| 异步处理 | 消息队列 + 后台处理 |

## 关键数字（Back of the Envelope）

| 数字 | 值 |
|------|-----|
| L1 Cache | ~1 ns |
| L2 Cache | ~5 ns |
| Memory | ~100 ns |
| SSD 随机读 | ~100 μs |
| HDD 随机读 | ~5-10 ms |
| 同数据中心 RTT | ~0.5 ms |
| 跨洲 RTT | ~100-200 ms |
| 1Gbps 网络 | ~125 MB/s |

这些数字决定了系统设计的每一步选择。

## 关系

- [[cap-theorem]]
- [[distributed-systems]]
- [[message-queue]]
- [[redis]]
- [[postgresql]]
