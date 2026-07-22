---
title: REST vs GraphQL
created: 2026-07-22
updated: 2026-07-22
type: comparison
tags: [comparison, api, protocol]
sources: []
confidence: high
---

# REST vs GraphQL

## 比什么

两种主流的 Web API 设计范式：传统 RESTful 架构 vs Facebook 2015 年发布的 GraphQL 查询语言。

## 比较

| 维度 | REST | GraphQL |
|------|------|---------|
| 数据获取 | 服务器定义返回结构 | 客户端指定需要的字段 |
| Over-fetching | 常见（返回多余数据） | 无（只返回请求的字段） |
| Under-fetching | 常见（需要多请求） | 无（单请求获取关联数据） |
| 端点 | 多个端点 (多个 URL) | 单一端点 (通常 /graphql) |
| 缓存 | HTTP 缓存原生支持 | 需要额外工具（Apollo, Relay） |
| 学习曲线 | 低 | 中（需学习 Schema 语言） |
| 文件上传 | 原生支持 (multipart) | 需要额外处理 |
| 错误处理 | HTTP 状态码 | 统一 200 + errors 字段 |
| 性能 | 简单场景更快 | N+1 问题需 DataLoader 解决 |
| 版本管理 | URL 版本 (/v1, /v2) | Schema 演进，无需版本号 |

## 选择建议

| 场景 | 推荐 |
|------|------|
| 简单 CRUD，接口结构稳定 | REST |
| 移动端/前端复杂数据需求 | GraphQL |
| 需要强 HTTP 缓存 | REST |
| 多个异构前端消费同一 API | GraphQL |
| 公开 API 给第三方 | REST（生态更成熟） |

## 总结

REST 和 GraphQL 不是替代关系，很多组织的 API 层同时使用两者。REST 简单可靠适合稳定接口，GraphQL 灵活强大适合复杂前端场景。选择取决于团队能力和消费端的复杂度。

## 相关

- [[rest-api]] — REST API 设计规范
- [[graphql]] — GraphQL 详解
