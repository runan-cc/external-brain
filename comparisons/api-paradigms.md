---
title: API 范式三国杀: REST vs GraphQL vs gRPC
created: 2026-07-22
updated: 2026-07-22
type: comparison
tags: [comparison, api, protocol, networking]
sources: []
confidence: high
---

# API 范式三国杀: REST vs GraphQL vs gRPC

## 比什么

三种主流 API 设计范式：传统 REST、查询优先的 GraphQL、高性能的 gRPC。

## 比较

| 维度 | [[rest-api]] | [[graphql]] | [[grpc]] |
|------|-------------|------------|------|
| 数据格式 | JSON | JSON | Protobuf (二进制) |
| 传输协议 | HTTP/1.1 或 HTTP/2 | HTTP/1.1 或 HTTP/2 | HTTP/2 |
| 性能 | ★★★ | ★★☆ | ★★★★★ |
| 人类可读 | ✅ | ✅ | ❌ (需工具) |
| 浏览器支持 | ✅ 原生 | ✅ 原生 | ⚠️ gRPC-web |
| 灵活度 | 低 (服务器定义) | 高 (客户端定义) | 中 (proto 定义) |
| 代码生成 | 手动/OpenAPI | 手动/GraphQL Codegen | ✅ 自动生成 |
| 流式数据 | ❌ (需 SSE) | ✅ Subscription | ✅ 原生双向流 |
| 强类型 | ❌ | ✅ Schema | ✅ Proto |
| 缓存 | HTTP 原生缓存 | 需要额外工具 | 较复杂 |
| 学习曲线 | 低 | 中 | 中高 |
| 生态成熟度 | 极高 | 高 | 中高 |

## 选择指南

| 场景 | 推荐 | 原因 |
|------|------|------|
| 公开 API / 第三方消费 | REST | 生态最成熟，文档最丰富 |
| 移动端 / 复杂前端页面 | GraphQL | 一次获取所需数据 |
| 微服务内部通信 | gRPC | 低延迟、高吞吐 |
| 实时数据推送 | GraphQL Sub / gRPC stream | 原生支持 |
| 小团队快速原型 | REST | 最简单 |
| 多语言系统 | gRPC | 一份 proto → 多语言 |

## 趋势

- GraphQL 在 To-C 前端的采用率增长，但 To-B 和内部服务仍以 REST 为主
- gRPC 在微服务架构中渗透率上升
- 实际架构常混合使用：REST 对外 + gRPC 对内

## 总结

三种范式不是替代关系。根据场景选择，而非追求统一。

## 相关

- [[rest-api]]
- [[rest-vs-graphql]]
- [[grpc]]
