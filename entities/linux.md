---
title: Linux
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [linux, os, devops, security]
sources: []
confidence: high
---

# Linux

## 概览

Linux 是 Linus Torvalds 于 1991 年创建的**开源类 Unix 操作系统内核**。结合 GNU 工具链构成 GNU/Linux 操作系统，是全球服务器、嵌入式设备和云计算的基础。

## 核心概念

| 概念 | 说明 |
|------|------|
| Kernel | 内核：进程调度、内存管理、设备驱动、文件系统 |
| Shell | 命令行解释器（bash, zsh, fish） |
| Filesystem | 一切皆文件：ext4, xfs, btrfs, zfs |
| Process | 可执行程序的运行实例，有 PID |
| Package Manager | apt (Debian/Ubuntu), yum/dnf (RHEL), pacman (Arch) |

## 发行版家族

| 家族 | 代表 | 特点 |
|------|------|------|
| Debian | Ubuntu, Debian | 广泛，生态最丰富 |
| RHEL | CentOS, Rocky, Fedora | 企业级 |
| Arch | Arch, Manjaro | 滚动更新，前沿 |
| Alpine | Alpine | 超轻量（常用于 Docker） |

## 常用命令

```bash
ls -la         # 列出文件
cd /path       # 切换目录
grep -r "text" # 搜索文本
chmod 755 file # 修改权限
ps aux | grep  # 进程查看
systemctl      # 服务管理
journalctl     # 日志查看
```

## Linux 在 AI/ML 中的角色

- **GPU 训练服务器**：几乎所有 AI 训练都在 Linux 上进行
- **[[docker]] 容器基础**：绝大多数 Docker 镜像基于 Linux
- **HPC 集群**：Slurm/MPI 等调度系统运行在 Linux 上
- **推理部署**：生产环境的 AI 服务几乎都在 Linux 上

## 关系

- [[docker]]
- [[kubernetes]]
