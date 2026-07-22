---
title: REST API
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [api, protocol, architecture, networking]
sources: []
confidence: high
---

# REST API

## 定义

REST（Representational State Transfer）是 Roy Fielding 于 2000 年提出的**软件架构风格**，用于设计网络 API。RESTful API 通过 HTTP 方法和资源 URL 进行通信，是目前最广泛的 API 设计模式。

## 核心原则

| 原则 | 说明 |
|------|------|
| 资源导向 | 一切皆资源，通过 URL 标识（如 `/users/123`） |
| HTTP 方法语义 | GET（读取）、POST（创建）、PUT（更新）、DELETE（删除） |
| 无状态 | 每个请求包含所有需要的信息，服务器不保存客户端状态 |
| 统一接口 | 标准的资源操作方式 |
| 分层架构 | 客户端不知道是否直连服务器或经过中间层 |

## 设计最佳实践

- **名词而非动词**：`GET /users` ✅ vs `GET /getUsers` ❌
- **版本控制**：URL (`/v1/users`) 或 Header (`Accept: version=1`)
- **分页**：`?page=2&limit=50` 或 cursor-based
- **错误码语义化**：`200 OK`, `201 Created`, `400 Bad Request`, `404 Not Found`, `500 Internal Error`
- **HATEOAS**（可选）：响应中包含可用的操作链接

## REST vs GraphQL

参见 [[rest-vs-graphql]]

## 相关概念

- [[graphql]] — GraphQL 查询语言
- [[grpc]] — gRPC 高性能 RPC 框架
- [[http]] — HTTP 协议基础
