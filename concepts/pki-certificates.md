---
title: 数字证书与 PKI
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [security, cryptography, certificate, pki]
sources: []
confidence: high
---

# 数字证书与 PKI (公钥基础设施)

## 定义

数字证书是**将公钥与身份绑定的电子凭证**——由可信第三方 (CA) 签名，确认"这个公钥确实属于 www.example.com"。PKI 是签发、管理、撤销证书的全套基础设施。

## 证书结构 (X.509)

```
X.509 Certificate
├── Subject: CN=www.example.com
├── Issuer: CN=Let's Encrypt R3
├── Validity: 2026-01-01 to 2026-04-01
├── Public Key: (RSA 2048 / ECDSA P-256)
├── Signature: (CA 的签名)
├── Serial Number: 123456789
├── Extensions
│   ├── SAN (Subject Alternative Name): example.com, *.example.com
│   ├── Key Usage: Digital Signature, Key Encipherment
│   └── Basic Constraints: CA=FALSE
└── Fingerprint: SHA-256: AB:CD:...
```

## 证书链 (Chain of Trust)

```
Root CA (自签名，预置在 OS/浏览器)
  ├── Intermediate CA 1
  │     ├── Intermediate CA 2
  │     │     └── End-entity Certificate (你的网站)
  │     └── End-entity Certificate
  └── End-entity Certificate
```

验证路径：逐级验证签名直到信任的根证书。

## TLS 握手中的证书

见 [[tls-ssl]]：
1. 服务器发送证书链
2. 客户端验证：
   - 签名有效性
   - 证书是否在有效期内
   - 证书是否被吊销 (CRL / OCSP)
   - CN/SAN 是否匹配域名

## 证书类型

| 类型 | 验证级别 | 示例 |
|------|----------|------|
| DV (Domain Validation) | 证明你控制域名 | Let's Encrypt 免费证书 |
| OV (Organization Validation) | +验证组织信息 | 公司网站 |
| EV (Extended Validation) | +严格法律验证 | 银行、支付（浏览器地址栏显示公司名） |

> EV 在 Chrome 中已不再显示绿色标识——DV 证书成为主流。

## Let's Encrypt

2016 年上线的免费 CA，通过 ACME 协议自动化签发。

```bash
certbot certonly --nginx -d example.com
# 自动验证域名所有权 → 签发 → 安装 → 自动续期
```

证书有效期 90 天（短周期降低风险），自动续期是标配。

## 证书吊销

| 方法 | 说明 |
|------|------|
| CRL (Certificate Revocation List) | CA 定期发布吊销列表（文件大、延迟高） |
| OCSP (Online Certificate Status Protocol) | 实时查询单个证书状态（隐私问题） |
| **OCSP Stapling** | 服务器代查并缓存 OCSP 响应，随 TLS 握手发给客户端 ✅ |

## CT (Certificate Transparency)

Google 推动的公开审计系统——所有 CA 签发的证书必须提交到 CT Log。
- 任何人都能监控哪个 CA 给哪个域名签发了证书
- 防止 CA 被入侵后秘密签发假证书（曾发生过多次！）

## 关系

- [[cryptography]]
- [[tls-ssl]]
- [[web-security]]
