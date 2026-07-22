---
title: TLS / SSL
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [security, networking, protocol, encryption]
sources: []
confidence: high
---

# TLS / SSL（传输层安全）

## 定义

TLS (Transport Layer Security) 及其前瞻 SSL (Secure Sockets Layer) 是加密通信协议，在 [[tcpip]] 传输层之上为应用层提供**机密性、完整性和身份验证**。HTTPS = HTTP + TLS。

## TLS 握手（1.2）

```
Client ── ClientHello (加密套件, 随机数, SNI) ───→  Server
Client ←── ServerHello + 证书 + ServerKeyExchange ←  Server
Client ── ClientKeyExchange + Finished ───→           Server
Client ←── Finished ←───────────────────────────      Server
```

## TLS 1.3 改进

- **1-RTT 握手**（vs 1.2 的 2-RTT），0-RTT 恢复
- 移除不安全算法：RSA 密钥交换、CBC 模式、RC4、SHA-1
- 前向安全 (Forward Secrecy)：强制使用 ECDHE 密钥交换
- 简化加密套件：只有 AEAD 算法 (AES-GCM, ChaCha20-Poly1305)

## 核心概念

| 概念 | 说明 |
|------|------|
| 证书 (Certificate) | 由 CA 签发，证明服务器身份 |
| CA (Certificate Authority) | 信任锚点（Let's Encrypt, DigiCert, Cloudflare） |
| SNI | Server Name Indication，一个 IP 多证书 |
| 前向安全 (PFS) | 私钥泄露不影响历史会话 |
| ALPN | 应用层协议协商 (HTTP/2, HTTP/1.1) |
| mTLS | 双向 TLS，客户端也提供证书 |

## 加密算法

### 对称加密（数据加密，快）
AES-GCM (128/256-bit), ChaCha20-Poly1305

### 非对称加密（密钥交换，慢）
ECDHE (椭圆曲线), RSA (逐渐淘汰)

### 哈希（完整性）
SHA-256, SHA-384

## 常见问题

| 问题 | 原因 |
|------|------|
| 证书过期 | 未续签 |
| 证书不匹配 | 域名与证书 SAN 不匹配 |
| 自签名证书 | 未受信任的 CA |
| TLS 降级攻击 | 中间人强制使用弱加密 |

## 关系

- [[http]] — HTTPS = HTTP + TLS
- [[tcpip]] — TLS 运行在传输层之上
- [[dns]] — DNS-over-TLS 加密 DNS 查询
