---
title: WebSocket & QUIC
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [network, protocol, websocket, realtime]
sources: []
confidence: high
---

# WebSocket & QUIC

## WebSocket

### 定义

WebSocket (RFC 6455, 2011) 是在单个 TCP 连接上实现**全双工、持久化通信**的协议。HTTP 请求-响应模式之外，WebSocket 让服务器可以**主动推送**消息到客户端。

### HTTP vs WebSocket

| 维度 | HTTP | WebSocket |
|------|------|-----------|
| 通信模式 | 请求-响应 | 全双工 |
| 连接 | 短连接/Keep-Alive | 持久连接 |
| 服务器推送 | ❌ (需 SSE/轮询) | ✅ |
| 头部开销 | 每次几百字节 | 2-14 字节/frame |
| 适用场景 | API、文档、静态资源 | 聊天、游戏、实时数据 |

### 握手（Upgrade from HTTP）

```
Client → Server:
GET /chat HTTP/1.1
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
Sec-WebSocket-Version: 13

Server → Client:
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
```

### Socket.IO vs 原生 WebSocket

| 维度 | 原生 WebSocket | Socket.IO |
|------|---------------|-----------|
| 传输 | WebSocket only | WebSocket + HTTP long-polling fallback |
| 自动重连 | ❌ | ✅ |
| 房间/广播 | ❌ | ✅ |
| 确认机制 | ❌ | ✅ |

### SSE vs WebSocket

| 维度 | SSE (Server-Sent Events) | WebSocket |
|------|--------------------------|-----------|
| 方向 | 服务器→客户端（单向） | 双向 |
| 协议 | HTTP | 独立协议 (ws://) |
| 自动重连 | ✅ 内置 | ❌ 需动手 |
| 数据格式 | 文本 | 文本/二进制 |
| 适用 | 通知、feed | 聊天、游戏、协作 |

## QUIC

### 定义

QUIC (Quick UDP Internet Connections) 是 Google 设计、现已成为 IETF 标准 (RFC 9000) 的**基于 UDP 的传输协议**。[[http|HTTP/3]] 运行在 QUIC 之上。

### TCP 的问题

| 问题 | QUIC 怎么解决 |
|------|-------------|
| 三次握手 + TLS 握手 = 2-3 RTT | **0-RTT** 恢复连接，1-RTT 新建连接 |
| 队头阻塞 (HoL Blocking) | 每条流独立，丢包只影响那条流 |
| 握手时协议僵化 | 连接迁移（WiFi ↔ 5G 无缝） |
| 中间设备篡改 | 所有数据加密（连 TCP 头部也不明文） |

### QUIC 协议栈

```
HTTP/3
  ↓
QUIC (流复用、拥塞控制、加密、连接迁移)
  ↓
UDP
  ↓
IP
```

### QUIC vs TCP+TLS

| 维度 | TCP + TLS 1.3 | QUIC |
|------|--------------|------|
| 传输 | TCP | UDP |
| 握手 (首次) | 2 RTT | 1 RTT |
| 握手 (恢复) | 1 RTT | 0 RTT |
| HoL 阻塞 | ✅ 存在 | ✅ 消除 |
| 连接迁移 | ❌ | ✅ |
| 部署 | ✅ 成熟 | 增长中（~30% Web） |
| 内核实现 | 内核 | 用户态 |

## 关系

- [[http]] — HTTP/3 = QUIC
- [[tcpip]] — TCP vs UDP
- [[tls-ssl]] — QUIC 内建 TLS 1.3
