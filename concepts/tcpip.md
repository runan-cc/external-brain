---
title: TCP/IP Protocol Stack
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [networking, protocol, internet, architecture]
sources: []
confidence: high
---

# TCP/IP 协议栈

## 定义

TCP/IP 是互联网的核心协议族，定义了数据如何在网络中打包、寻址、传输和接收。由 Vint Cerf 和 Bob Kahn 于 1974 年设计，是互联网的"通用语言"。

## 四层模型

```
┌─────────────────────────────┐
│  Application Layer (应用层) │   HTTP, DNS, SMTP, SSH, FTP
├─────────────────────────────┤
│  Transport Layer (传输层)   │   TCP, UDP, QUIC
├─────────────────────────────┤
│  Internet Layer (网络层)    │   IP, ICMP, ARP, BGP
├─────────────────────────────┤
│  Link Layer (链路层)        │   Ethernet, Wi-Fi, MAC
└─────────────────────────────┘
```

## 各层详解

### 链路层（Link Layer）
数据在物理网络中的传输，MAC 地址标识设备。

### 网络层（Internet Layer）
**IP (Internet Protocol)**：负责寻址和路由
- IPv4：32 位地址，~43 亿地址（地址枯竭）
- IPv6：128 位地址，3.4×10³⁸ 地址

### 传输层（Transport Layer）

| 协议 | 特点 | 适用场景 |
|------|------|----------|
| **TCP** | 面向连接、可靠、有序、拥塞控制 | Web, Email, SSH, 文件传输 |
| **UDP** | 无连接、不可靠、低延迟 | 视频流, DNS, 游戏, VoIP |
| **QUIC** | 基于 UDP + TLS, 0-RTT, 多路复用 | HTTP/3, 未来趋势 |

**TCP 三向握手：**
```
Client  ─── SYN (seq=x) ─────→  Server
Client  ←─ SYN+ACK (seq=y, ack=x+1) ─  Server
Client  ─── ACK (ack=y+1) ───→  Server
```

**TCP 四次挥手：**
```
一方发送 FIN → 对方 ACK → 对方 FIN → 本方 ACK
```

### 应用层（Application Layer）
用户直接接触的协议：[[http]], [[dns]], SMTP (邮件), SSH (安全 shell), FTP (文件传输)

## OSI 七层模型（对比）

| OSI 层 | 对应 TCP/IP 层 |
|--------|---------------|
| 7. 应用层 | ┐ |
| 6. 表示层 | ├ 应用层 |
| 5. 会话层 | ┘ |
| 4. 传输层 | 传输层 |
| 3. 网络层 | 网络层 |
| 2. 数据链路层 | ┐ 链路层 |
| 1. 物理层 | ┘ |

## 关键概念

- **MTU (Maximum Transmission Unit)**：链路层最大数据包（以太网 1500 字节）
- **MSS (Maximum Segment Size)**：TCP 最大段大小 = MTU - IP 头 - TCP 头
- **Nagle 算法**：合并小数据包减少网络开销
- **拥塞控制**：TCP Cubic, BBR (Google)

## 关系

- [[http]] — 应用层协议
- [[dns]] — 应用层协议
- [[tls-ssl]] — 传输层之上的加密
- [[ip-address]] — 网络层寻址
