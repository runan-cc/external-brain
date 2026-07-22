---
title: 密码学基础
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [security, cryptography, encryption]
sources: []
confidence: high
---

# 密码学基础

## 定义

密码学是研究**安全通信**的数学学科——在存在敌手的情况下保护信息的机密性、完整性和真实性。

## 核心目标

| 目标 | 含义 | 实现 |
|------|------|------|
| 机密性 (Confidentiality) | 只有授权方能看到内容 | 加密 |
| 完整性 (Integrity) | 内容未被篡改 | 哈希、MAC |
| 认证 (Authentication) | 确认通信方身份 | 数字签名、证书 |
| 不可否认性 (Non-repudiation) | 发送者不能否认已发送 | 数字签名 |

## 加密类型

### 对称加密
**同一密钥**加密和解密。

| 算法 | 密钥长度 | 特点 |
|------|----------|------|
| AES | 128/256-bit | 全球标准，硬件加速 |
| ChaCha20 | 256-bit | 移动端友好，软件高效 |
| DES | 56-bit | **不安全，已淘汰** |

### 非对称加密
**公钥加密、私钥解密**（或反向签名）。

| 算法 | 用途 |
|------|------|
| RSA | 加密 + 签名（逐渐被淘汰） |
| ECDSA (椭圆曲线) | 数字签名（SSH, TLS, 区块链） |
| Ed25519 | 现代签名标准，安全且快 |
| ECDH | 密钥交换 |

## 哈希函数

| 算法 | 输出长度 | 状态 |
|------|----------|------|
| SHA-256 | 256-bit | ✅ 安全（比特币、TLS） |
| SHA-3 | 可变 | ✅ 最新标准 |
| BLAKE3 | 可变 | ✅ 极快 |
| MD5 | 128-bit | ❌ 已破解 |
| SHA-1 | 160-bit | ❌ 已破解 |

## 实战场景

| 场景 | 使用的技术 |
|------|-----------|
| HTTPS | [[tls-ssl]] (ECDHE + AES-GCM + SHA-256) |
| SSH | Ed25519 / RSA + DH 密钥交换 |
| Git commit 签名 | GPG (RSA/ECC) |
| 密码存储 | bcrypt / Argon2id（不是哈希！） |
| 区块链 | ECDSA + SHA-256 |
| JWT | HMAC-SHA256 / RS256 |

## 关键原则

- **Kerckhoffs 原则**：系统安全性应完全依赖密钥而非算法保密
- **不要自己发明密码算法**：使用经过审计的库（libsodium, OpenSSL）
- **密码 ≠ 哈希**：密码存储用 bcrypt/Argon2id（故意慢）
- **量子威胁**：Shor 算法将破解 RSA/ECDSA，后量子密码学 (PQC) 正在标准化

## 关系

- [[tls-ssl]] — 密码学的集大成应用
- [[ssh]] — 基于非对称加密的安全 shell
