---
title: 存储系统与文件系统
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [storage, filesystem, hardware, database]
sources: []
confidence: high
---

# 存储系统与文件系统

## 定义

存储系统负责数据的**持久化保存**——从硬件介质到文件系统再到数据库引擎，构成了完整的数据存储栈。

## 存储硬件

### HDD vs SSD

| 维度 | HDD | SSD |
|------|-----|-----|
| 原理 | 磁头旋转读取 | NAND Flash 电子读写 |
| 随机读写 IOPS | ~100-200 | 10K-1M+ |
| 顺序读 | ~200 MB/s | 500-7000 MB/s |
| 延迟 | ~5-10 ms | ~0.1 ms |
| 成本/GB | 低 | 中 (NVMe) / 高 |
| 寿命 | 机械磨损 | 写入次数有限 (TBW) |
| 适合 | 冷数据、大容量存储 | OS、数据库、热数据 |

### NVMe vs SATA

| 维度 | NVMe (PCIe) | SATA |
|------|-------------|------|
| 带宽 | PCIe 4.0: 8 GB/s | 600 MB/s |
| 协议 | 原生 PCIe | AHCI → NVMe 翻译 |
| 队列深度 | 64K 队列 | 32 队列 |
| 适用 | 高性能计算 | 普通消费 |

### RAID

| RAID | 模式 | 容量 | 容错 |
|------|------|------|------|
| RAID 0 | 条带化 | 100% | 0 块 |
| RAID 1 | 镜像 | 50% | 1 块 |
| RAID 5 | 奇偶校验 | N-1 块 | 1 块 |
| RAID 6 | 双奇偶校验 | N-2 块 | 2 块 |
| RAID 10 | 镜像+条带 | 50% | 每对 1 块 |

## 文件系统

| 文件系统 | 特点 |
|----------|------|
| ext4 | Linux 默认，稳定成熟 |
| XFS | 大文件 + 高并发 |
| Btrfs | Copy-on-Write、快照、压缩 |
| ZFS | 最强大：数据完整性校验、快照、去重、RAID-Z、128 位寻址 |
| NTFS | Windows 标准 |
| APFS | macOS 现代文件系统，CoW |

### ZFS 关键特性

- **Copy-on-Write**：写不覆盖原数据，天然支持快照
- **Checksum**：每个 block 有 SHA-256，自动检测和修复
- **Snapshot**：几乎零成本的快照和克隆
- **RAID-Z**：解决 RAID5 的 write hole 问题

## 数据库存储引擎

### B-Tree

最广泛使用的索引结构：
- 自平衡树，每个节点可以有很多子节点
- 适合范围查询和顺序扫描
- [[postgresql]]、MySQL InnoDB 默认使用

### LSM Tree (Log-Structured Merge Tree)

- 写入先进入内存（MemTable）→ 满了刷到磁盘（SSTable）
- 多层 SSTable 定时合并（Compaction）
- **写放大** vs **读放大**的权衡

| 引擎 | B-Tree | LSM Tree |
|------|--------|----------|
| 读性能 | ✅ 快 | 需查多层 |
| 写性能 | 随机写 | ✅ 顺序写 |
| 空间放大 | 较大（碎片） | 需 compaction |
| 代表 | PG, MySQL | RocksDB, LevelDB, Cassandra |

### WAL (Write-Ahead Log)

数据库的共同模式：**先写日志再写数据**——崩溃恢复时 replay WAL 恢复已提交事务。

## 关系

- [[computer-architecture]] — 内存层次结构
- [[operating-system]] — 文件系统是 OS 核心组件
- [[postgresql]] — PG 的数据存储
- [[acid-transactions]] — WAL 保证持久性
