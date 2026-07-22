---
title: CDN (Content Delivery Network)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [network, web, performance, architecture]
sources: []
confidence: high
---

# CDN (Content Delivery Network)

## 定义

CDN 是**地理分布的代理服务器网络**，将内容缓存到离用户最近的边缘节点，显著降低延迟和源服务器压力。现代 Web 几乎没有不用 CDN 的。

## 工作原理

```
用户（北京）→ DNS 解析 → CDN 智能调度 → 北京边缘节点（有缓存？）
                                              ↓ 没有
                                         回源（Origin）→ 缓存 → 返回
```

## 核心能力

| 能力 | 说明 |
|------|------|
| 静态加速 | 图片/JS/CSS/视频 缓存到边缘 |
| 动态加速 | 智能路由、协议优化（TCP 优化、QUIC） |
| DDoS 防护 | 分布式节点吸收攻击流量 |
| WAF | 应用防火墙（SQL 注入、XSS 拦截） |
| Edge Computing | 在边缘节点运行代码（Cloudflare Workers） |

## 关键技术

### Anycast
多个节点共享同一 IP，BGP 自动路由到最近节点。

### Cache 策略

| 头 | 含义 |
|-----|------|
| Cache-Control: max-age=3600 | 缓存 1 小时 |
| Cache-Control: no-cache | 每次都验证 |
| Cache-Control: no-store | 不缓存 |
| ETag | 内容版本标识 |
| Last-Modified | 上次修改时间 |

### 缓存 Key
默认：`scheme + host + URI`。可自定义（去掉无用查询参数）。

### 回源策略
- 缓存未命中 → 回源 → 缓存 → 返回
- 预热：提前把热点内容推送到边缘
- 分层缓存：L1 (边缘) → L2 (区域) → Origin

## 主流 CDN

| 提供商 | 特点 |
|--------|------|
| Cloudflare | 全球最大，免费套餐，Workers 边缘计算 |
| Akamai | 企业级，最早商业化 CDN |
| AWS CloudFront | AWS 生态集成 |
| Fastly | 高性能，VCL 配置，即时 purge |
| KeyCDN / BunnyCDN | 性价比高 |

## CDN 不见于的坑

| 问题 | 说明 |
|------|------|
| 缓存穿透 | 大量请求同一未缓存资源 → 都回源 |
| 缓存雪崩 | 大量缓存同时过期 → 源站被打爆 |
| 缓存不一致 | 更新了源站但 CDN 还有旧版本 → Cache Purge |
| 地域限制 | 某些 CDN 在中国大陆没有节点 |
| SSL 证书 | 需要在 CDN 上配置证书 |

## 关系

- [[dns]] — CDN 基于 DNS 做智能解析
- [[http]] — 通过 HTTP Cache-Control 控制缓存
- [[tls-ssl]] — CDN 边缘节点做 SSL termination
