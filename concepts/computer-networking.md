---
title: Computer Networking Notes
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [networking, internet, protocol]
sources: []
confidence: high
---

# 计算机网络基础

## 定义

计算机网络是**互联计算设备的集合**，通过通信协议实现资源共享和信息交换。互联网是最大的计算机网络实例。

## 网络拓扑

| 拓扑 | 特点 |
|------|------|
| Bus（总线） | 共享介质，已淘汰 |
| Star（星型） | 中心交换机，现代局域网主流 |
| Ring（环型） | 令牌环，SAN 中仍用 |
| Mesh（网状） | 全连接，无线 mesh |

## 网络设备

| 设备 | OSI 层 | 功能 |
|------|--------|------|
| Hub (集线器) | L1 | 广播所有端口 |
| Switch (交换机) | L2 | MAC 地址转发 |
| Router (路由器) | L3 | IP 地址路由 |
| Firewall (防火墙) | L3-L7 | 流量过滤 |
| Load Balancer | L4/L7 | 流量分发 |
| NAT Gateway | L3 | 内外 IP 映射 |

## 关键概念

### IP 地址
- **IPv4**：`192.168.1.1`，32 位
- **IPv6**：`2001:db8::1`，128 位，淘汰 IPv4 是必然趋势
- **私有地址**：`10.x.x.x`, `172.16-31.x.x`, `192.168.x.x`
- **CIDR**：`192.168.1.0/24`（子网掩码表示法）

### 路由协议
| 协议 | 类型 | 用途 |
|------|------|------|
| BGP | 外部网关 | 互联网骨干路由 |
| OSPF | 内部网关 | 企业内网路由 |

### NAT (Network Address Translation)
私有 IP ↔ 公网 IP 转换，缓解 IPv4 地址枯竭。缺点：破坏端到端原则。

## 关系

- [[tcpip]] — 核心协议栈
- [[http]] — Web 应用协议
- [[dns]] — 域名解析
- [[tls-ssl]] — 安全传输
- [[ip-address]] — 网络寻址
