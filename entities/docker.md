---
title: Docker
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [docker, devops, container]
sources: []
confidence: high
---

# Docker

## 概览

Docker 是**容器化平台**，通过操作系统级虚拟化将应用及其依赖打包为轻量级容器，实现"一次构建，到处运行"。2013 年开源，改变了软件部署方式。

## 核心概念

| 概念 | 说明 |
|------|------|
| Image（镜像） | 只读模板，包含运行环境和代码 |
| Container（容器） | Image 的运行实例 |
| Dockerfile | 构建镜像的声明式脚本 |
| Docker Compose | 多容器应用编排 |
| Registry | 镜像仓库（Docker Hub, ECR 等） |
| Volume | 持久化存储 |
| Network | 容器间网络通信 |

## Docker vs VM

| 维度 | Docker | 虚拟机 |
|------|--------|--------|
| 启动速度 | 秒级 | 分钟级 |
| 资源占用 | MB 级 | GB 级 |
| 隔离级别 | 进程级（共享内核） | 硬件级 |
| 镜像大小 | 通常 <100MB | 数 GB |

## 常用命令

```bash
docker build -t name .        # 构建镜像
docker run -d -p 80:80 name  # 运行容器
docker ps                      # 查看运行中的容器
docker compose up -d           # 启动 docker-compose
docker exec -it container sh  # 进入容器
docker logs container         # 查看日志
```

## 相关概念

- [[kubernetes]] — 容器编排
- [[ci-cd]] — 构建 + 部署
