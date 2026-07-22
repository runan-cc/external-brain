---
title: HTTP
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [protocol, networking, web]
sources: []
confidence: high
---

# HTTP (Hypertext Transfer Protocol)

## 定义

HTTP 是万维网的基础通信协议，基于 TCP 的请求-响应模型。由 Tim Berners-Lee 于 1989 年提出。目前 Web 的所有 API 和页面传输都基于 HTTP。

## 版本演进

| 版本 | 年份 | 关键特性 |
|------|------|----------|
| HTTP/1.0 | 1996 | 每请求一个 TCP 连接 |
| HTTP/1.1 | 1997 | 持久连接、管道化、Host 头、分块传输 |
| HTTP/2 | 2015 | 多路复用、头部压缩 (HPACK)、Server Push |
| HTTP/3 | 2022 | 基于 QUIC (UDP)，0-RTT 连接建立 |

## 请求-响应模型

```
Client (浏览器/app)                    Server
    |                                    |
    |  GET /api/users HTTP/1.1          |
    |  Host: example.com                |
    |  Authorization: Bearer xxxx       |
    |  ──────────────────────────────→  |
    |                                    |
    |  HTTP/1.1 200 OK                  |
    |  Content-Type: application/json   |
    |  {"users": [...]}                 |
    |  ←──────────────────────────────  |
```

## HTTP 方法

| 方法 | 语义 | 幂等 | 安全 |
|------|------|------|------|
| GET | 获取资源 | ✅ | ✅ |
| POST | 创建资源 | ❌ | ❌ |
| PUT | 替换/创建资源 | ✅ | ❌ |
| PATCH | 部分更新 | ❌ | ❌ |
| DELETE | 删除资源 | ✅ | ❌ |
| HEAD | 只获取头部 | ✅ | ✅ |
| OPTIONS | 查询支持的方法 | ✅ | ✅ |

## 状态码

| 范围 | 含义 | 示例 |
|------|------|------|
| 1xx | 信息 | 101 Switching Protocols |
| 2xx | 成功 | 200 OK, 201 Created, 204 No Content |
| 3xx | 重定向 | 301 永久, 302 临时, 304 Not Modified |
| 4xx | 客户端错误 | 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 429 Too Many Requests |
| 5xx | 服务端错误 | 500 Internal Error, 502 Bad Gateway, 503 Service Unavailable |

## 安全

- **HTTPS**：HTTP + TLS 加密
- **CORS**：跨域资源共享，通过 `Access-Control-*` 头部控制
- **CSP**：Content Security Policy，防止 XSS
- **HSTS**：强制 HTTPS

## 关系

- [[rest-api]] — 基于 HTTP 的 API 设计
- [[tls-ssl]] — 加密层
- [[dns]] — 域名解析
- [[tcpip]] — 底层传输协议
