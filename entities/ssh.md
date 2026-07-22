---
title: SSH
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [ssh, security, remote, protocol, tool]
sources: []
confidence: high
---

# SSH (Secure Shell)

## 概览

SSH (Secure Shell) 是**加密的远程登录协议**，1995 年由 Tatu Ylönen 创建，现已成为远程服务器管理的标准。替代了不安全的 Telnet 和 rlogin。

## 工作原理

```
客户端                                    服务器
  ↓                                          ↓
1. TCP 连接建立
2. 密钥交换 (DH 或 ECDH) → 共享密钥
3. 服务器认证 (Host Key 验证)
4. 用户认证:
   - 密码
   - 公钥认证 (最常用)
   - 键盘交互
5. 加密通道建立 → 后续通信全加密
```

## 公钥认证

```bash
# 1. 生成密钥对
ssh-keygen -t ed25519 -C "user@host"

# 2. 复制公钥到服务器
ssh-copy-id user@server

# 3. 免密登录
ssh user@server
```

| 密钥类型 | 推荐度 | 说明 |
|----------|--------|------|
| **Ed25519** | ⭐⭐⭐ | 现代标准，安全 + 快 |
| ECDSA (P-256) | ⭐⭐ | 可接受 |
| RSA 4096 | ⭐ | 兼容性好，体积大 |
| RSA < 2048 | ❌ | 不安全 |
| DSA | ❌ | 已废弃 |

## 关键功能

| 功能 | 命令 |
|------|------|
| 远程登录 | `ssh user@host` |
| 端口转发 (Local) | `ssh -L 8080:localhost:80 user@host` |
| 端口转发 (Remote) | `ssh -R 9090:localhost:3000 user@host` |
| 动态转发 (SOCKS) | `ssh -D 1080 user@host` |
| SCP 复制文件 | `scp file.txt user@host:/path` |
| SFTP | `sftp user@host` |
| 执行远程命令 | `ssh user@host 'ls -la'` |
| 跳板 | `ssh -J bastion user@internal` |

## 配置文件 (~/.ssh/config)

```
Host myserver
    HostName 192.168.1.100
    User ubuntu
    IdentityFile ~/.ssh/id_ed25519
    Port 2222

Host prod-*
    User admin
    IdentityFile ~/.ssh/id_ed25519_prod
```

然后直接用 `ssh myserver`。

## 安全最佳实践

| 实践 | 说明 |
|------|------|
| 禁用密码登录 | `PasswordAuthentication no` |
| 禁用 root 登录 | `PermitRootLogin no` |
| 更换端口 | 非 22 端口减少扫描 |
| 使用 Fail2ban | 自动封禁暴力破解 IP |
| 定期更换密钥 | 每年轮换 |
| 密钥带密码 | `ssh-keygen -t ed25519 -C ...` 输密码 |

## SSH 隧道

```bash
# 本地端口转发：访问本地 5432 → 远程 DB
ssh -L 5432:rds.amazonaws.com:5432 bastion

# 远程端口转发：暴露本地 3000 到服务器 9000
ssh -R 9000:localhost:3000 server
```

## 关系

- [[cryptography]] — Ed25519、DH 密钥交换
- [[tls-ssl]] — 同为加密通信协议
- [[linux]] — SSH 是 Linux 服务器的标配
