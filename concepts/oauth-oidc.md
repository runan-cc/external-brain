---
title: OAuth 2.0 & OIDC
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [authentication, authorization, protocol, security]
sources: []
confidence: high
---

# OAuth 2.0 & OpenID Connect

## OAuth 2.0

OAuth 2.0 (2012) 是**授权委托**协议，不是认证协议。本质：用户授权第三方应用访问其在某平台上受保护的资源，而**不暴露自己的密码**。

## 四大角色

| 角色 | 示例 |
|------|------|
| Resource Owner | 用户（你） |
| Client | 第三方 App |
| Authorization Server | Google/GitHub 的授权服务 |
| Resource Server | 存储用户资源的 API |

## 授权类型 (Grant Types)

| 类型 | 场景 |
|------|------|
| **Authorization Code + PKCE** | 原生 App、SPA（推荐，2025 年起非此莫属） |
| Client Credentials | 服务端到端（无用户） |
| Device Code | 电视/IoT 等无浏览器的设备 |
| Refresh Token | 续期 Access Token |

> ⚠️ **Implicit Grant 已弃用**（OAuth 2.1 草案移除）。密码 Grant 也应避免。

## Authorization Code + PKCE 流程

```
1. Client → Auth Server: /authorize?client_id=XX&code_challenge=<hash>&...
2. User 登录 + 授权
3. Auth Server → Client: ?code=AUTH_CODE_XYZ
4. Client → Auth Server: /token?code=AUTH_CODE_XYZ&code_verifier=<original>
5. Auth Server → Client: { access_token, refresh_token, id_token }
6. Client → Resource Server: Authorization: Bearer <access_token>
```

PKCE 防止授权码拦截攻击，已成为 OAuth 2.1 的强制要求。

## Access Token vs Refresh Token

| 维度 | Access Token | Refresh Token |
|------|-------------|---------------|
| 用途 | 访问资源 | 获取新 Access Token |
| 有效期 | 短（5-30 分钟） | 长（数天-数月） |
| 暴露频率 | 每个 API 请求 | 仅在 token endpoint |
| 格式 | 通常 JWT | 不透明字符串 |

## OpenID Connect (OIDC)

OAuth 2.0 只做授权，OIDC 在其上加**身份认证**层。增加 `id_token`（JWT 格式）。

| Token | 用途 | 受众 |
|-------|------|------|
| Access Token | 访问 API | Resource Server |
| id_token | 证明用户身份 | Client |
| Refresh Token | 续期 | Auth Server |

**id_token payload 示例**：
```json
{
  "iss": "https://accounts.google.com",
  "sub": "1234567890",
  "aud": "my-client-id",
  "exp": 1710000000,
  "email": "user@example.com",
  "name": "Alice"
}
```

## 常见安全陷阱

| 错误 | 后果 | 修复 |
|------|------|------|
| 在 SPA 中存储 Refresh Token | XSS 窃取 | BFF (Backend-for-Frontend) |
| redirect_uri 不验证 | 授权码拦截 | 精确匹配白名单 |
| state 参数省略 | CSRF | 每次请求带 random state |
| Implicit Grant 使用 | Token 泄露在 URL | 用 Auth Code + PKCE |

## 关系

- [[web-security]]
- [[cryptography]]
- [[http]]
