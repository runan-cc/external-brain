---
title: Nginx
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [server, proxy, performance, devops]
sources: []
confidence: high
---

# Nginx

## 概览

Nginx (Engine X) 是 Igor Sysoev 于 2004 年创建的高性能 HTTP 服务器和反向代理。以**事件驱动、异步非阻塞**架构著称——一个 worker 进程处理数万并发连接。是目前全球最流行的 Web 服务器。

## 核心特性

| 特性 | 说明 |
|------|------|
| Web 服务器 | 静态文件服务、目录索引 |
| 反向代理 | 转发请求到后端应用 |
| 负载均衡 | Round Robin / Least Connections / IP Hash / Weighted |
| SSL/TLS 终止 | 在代理层加解密 |
| HTTP/2 & HTTP/3 | 支持现代协议 |
| 缓存 | 代理缓存，减少后端负载 |
| 限流 | 限制请求频率 |
| 流媒体 | HLS/RTMP |
| gRPC 代理 | 原生支持 gRPC（v1.13.10+） |

## 架构

```
Master Process（root）
    ├── Worker Process 1（非特权用户）
    ├── Worker Process 2
    ├── Worker Process 3
    └── Worker Process N  # N = CPU 核数

每个 Worker 是单线程异步事件驱动（epoll/kqueue）
→ 不需要为每个连接创建线程
→ 极低的内存占用
```

## 配置示例

```nginx
# 反向代理
server {
    listen 80;
    server_name example.com;
    return 301 https://$host$request_uri;  # HTTP → HTTPS
}

server {
    listen 443 ssl;
    server_name example.com;

    location / {
        proxy_pass http://localhost:3000;   # 转发到 Node 应用
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location /static/ {
        root /var/www;                      # 静态文件直接返回
        expires 30d;
    }
}
```

## Nginx vs Apache

| 维度 | Nginx | Apache |
|------|-------|--------|
| 架构 | 事件驱动 (async) | 进程/线程 (每个连接) |
| 并发 | 数万连接 | 数百连接 |
| 内存 | 低且稳定 | 随连接增长 |
| 动态内容 | 通过代理 | 支持嵌入模块 |
| .htaccess | 不支持 | 支持 |
| 配置 | 更简洁 | 更灵活 |

## 常用场景

| 场景 | 配置 |
|------|------|
| 静态文件 | `root + expires` |
| 反向代理 | `proxy_pass` |
| 负载均衡 | `upstream + proxy_pass` |
| 限流 | `limit_req_zone + limit_req` |
| HTTPS | `ssl_certificate + ssl_certificate_key` |
| WebSocket | `proxy_set_header Upgrade` |
| 压缩 | `gzip on` |

## 关系

- [[http]]
- [[tls-ssl]]
- [[cdn]]
- [[docker]] — 常用作容器中的反向代理
