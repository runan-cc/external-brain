---
title: 操作系统
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [os, architecture, linux, systems]
sources: []
confidence: high
---

# 操作系统 (Operating System)

## 定义

操作系统是管理计算机硬件资源和提供公共服务的基础软件。它是硬件之上的第一层抽象——所有应用程序都运行在 OS 之上。

## 核心职责

| 职责 | 说明 |
|------|------|
| 进程管理 | 创建、调度、（进程间通信） |
| 内存管理 | 虚拟内存、分页、保护 |
| 文件系统 | 持久化存储的组织和访问 |
| 设备管理 | I/O 中断、DMA、驱动 |
| 安全与权限 | 用户/组，ACL，沙箱 |
| 系统调用 | `open()`, `read()`, `write()`, `fork()`, `exec()` |

## 进程 vs 线程

| 维度 | 进程 | 线程 |
|------|------|------|
| 定义 | 程序的一次执行实例 | 进程内的执行流 |
| 地址空间 | 独立 | 共享 |
| 创建开销 | 大 | 小 |
| 通信 | IPC (管道/共享内存/socket) | 直接读写共享变量 |
| 崩溃影响 | 不影响其他进程 | 整个进程崩溃 |

## 调度算法

| 算法 | 特点 |
|------|------|
| FCFS | 先来先服务，简单但可能饥饿 |
| SJF | 最短作业优先，需要预知运行时间 |
| Round Robin | 时间片轮转，公平 |
| CFS (Linux) | 完全公平调度器，红黑树维护 |
| EEVDF (Linux 6.6+) | 最早期限优先 |

## 内存管理

### 虚拟内存
每个进程看到独立的、连续的地址空间，实际物理内存由 MMU (Memory Management Unit) 通过**页表**映射。

### 分页 vs 分段
| 维度 | 分页 | 分段 |
|------|------|------|
| 单位 | 固定大小 (4KB/Huge Pages 2MB/1GB) | 可变大小 |
| 碎片 | 内部碎片 | 外部碎片 |
| 现代使用 | 主流 | 历史遗留 |

### 页面置换算法
- **LRU** (Least Recently Used)：换出最久未使用的页
- **Clock / Second Chance**：LRU 的近似实现
- **Linux**：Active/Inactive LRU 双链表

## 主流 OS

| OS | 内核 | 特点 |
|-----|------|------|
| [[linux]] | Linux (Monolithic) | 服务器/嵌入式/Android |
| Windows | NT (Hybrid) | 桌面/游戏/企业 |
| macOS | XNU (Hybrid: Mach + BSD) | 创意/开发 |
| FreeBSD | BSD (Monolithic) | 网络/存储 |
| Android | Linux | 移动端 |

## 关系

- [[linux]] — 最广泛使用的 OS 内核
- [[docker]] — 基于 OS 级虚拟化（namespace + cgroups）
- [[computer-architecture]] — OS 管理的硬件对象
