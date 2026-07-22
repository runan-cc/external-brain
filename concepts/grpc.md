---
title: gRPC
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [protocol, api, networking, performance]
sources: []
confidence: high
---

# gRPC

## 定义

gRPC 是 Google 于 2016 年开源的**高性能 RPC 框架**，基于 HTTP/2 和 Protocol Buffers（protobuf）。它是微服务架构中 [[rest-api]] 的主要替代方案，尤其适合高性能和低延迟场景。

## 核心特性

- **Protocol Buffers**：二进制序列化，比 JSON 快 5-10 倍，体积小 3-10 倍
- **HTTP/2 多路复用**：单连接并发多请求，减少开销
- **流式调用**：支持四种模式（unary, server streaming, client streaming, bidirectional）
- **强类型 API 契约**：`.proto` 文件定义接口，自动生成多语言 client/server 代码
- **Deadline / Cancellation**：内置超时和取消机制

## Proto 示例

```protobuf
service UserService {
  rpc GetUser (GetUserRequest) returns (User);
  rpc ListUsers (ListUsersRequest) returns (stream User);
}

message GetUserRequest {
  int32 user_id = 1;
}

message User {
  int32 id = 1;
  string name = 2;
  string email = 3;
}
```

## gRPC vs REST

| 维度 | gRPC | [[rest-api]] |
|------|------|-------------|
| 序列化 | Protobuf (二进制) | JSON (文本) |
| 速度 | 极快 | 较慢 |
| 人类可读 | 需要工具 | 直接可读 |
| 浏览器支持 | 需要 gRPC-web | 原生支持 |
| 流式 | 原生支持 | SSE/WebSocket 额外实现 |
| 代码生成 | 自动生成 | 需手动或用 OpenAPI |
| 调试 | 较复杂 | 简单（curl/浏览器） |

## 适用场景

- **微服务内部通信**：低延迟，高性能
- **移动端 → 服务端**：二进制小体积，省流量
- **实时流式数据**：聊天、游戏、数据管道
- **多语言系统**：一份 proto 定义，多语言代码生成

## 关系

- [[rest-api]]
- [[rest-vs-graphql]]
