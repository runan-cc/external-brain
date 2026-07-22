---
title: DNS
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [networking, protocol, internet]
sources: []
confidence: high
---

# DNS (Domain Name System)

## 定义

DNS 是互联网的**电话簿**——将人类可读的域名（`google.com`）转换为机器可路由的 IP 地址（`142.250.80.46`）。1983 年由 Paul Mockapetris 设计。

## 域名解析过程

```
用户输入 example.com
    ↓
1. 浏览器缓存
    ↓ (miss)
2. OS 缓存 (hosts 文件)
    ↓ (miss)
3. 递归解析器 (ISP/8.8.8.8)
    ↓
4. Root DNS Server → ".com" NS
    ↓
5. TLD Server (.com) → "example.com" NS
    ↓
6. Authoritative Server → 142.250.80.46
    ↓
7. 返回 IP 地址给浏览器
```

## 记录类型

| 类型 | 用途 |
|------|------|
| A | 域名 → IPv4 地址 |
| AAAA | 域名 → IPv6 地址 |
| CNAME | 域名 → 别名（指向其他域名） |
| MX | 邮件服务器 |
| TXT | 文本记录（SPF/DKIM/验证） |
| NS | 权威 DNS 服务器 |
| SOA | 区域管理信息 |
| SRV | 服务发现 |

## 关键概念

- **TTL (Time To Live)**：缓存时间，决定了变更传播延迟
- **Anycast**：同一 IP 路由到最近节点（8.8.8.8 等公共 DNS）
- **DNSSEC**：DNS 安全扩展，防止 DNS 欺骗
- **DNS-over-HTTPS (DoH) / DNS-over-TLS (DoT)**：加密 DNS 查询，防 ISP 窥探

## 公共 DNS

| 服务 | IP | 特点 |
|------|-----|------|
| Google | 8.8.8.8 / 8.8.4.4 | 快，全球覆盖 |
| Cloudflare | 1.1.1.1 / 1.0.0.1 | 隐私优先 |
| Quad9 | 9.9.9.9 | 安全过滤（拦截恶意域名） |

## 关系

- [[http]] — Web 访问的第一步
- [[ip-address]] — DNS 解析的目标
- [[tls-ssl]] — HTTPS 依赖 DNS 解析后建立 TLS
