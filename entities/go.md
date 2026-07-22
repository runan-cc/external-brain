---
title: Go
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [go, language, programming, backend]
sources: []
confidence: high
---

# Go (Golang)

## 概览

Go 是 Google 于 2009 年发布的**编译型、并发优先的编程语言**，由 Rob Pike、Ken Thompson 和 Robert Griesemer 设计。以简洁、高效、goroutine 并发模型著称，是云原生基础设施的主力语言。

## 核心特性

- **Goroutine**：轻量级协程（~2KB 栈），一个程序可运行百万级 goroutine
- **Channel**：goroutine 间通信的原语——"不要通过共享内存来通信，而通过通信来共享内存"
- **接口（Interface）**：隐式实现，无需声明
- **垃圾回收**：低延迟、并发 GC
- **编译为单一二进制**：无运行时依赖，部署极简

## Go vs Rust

| 维度 | Go | [[rust]] |
|------|-----|----------|
| 设计哲学 | 简洁、工程效率 | 安全、零成本抽象 |
| 并发模型 | goroutine + channel | async/await + Send/Sync |
| 学习曲线 | 低 | 高 |
| GC | 有 | 无 |
| 适合场景 | 网络服务、CLI、DevOps | 系统编程、嵌入式、WASM |

## 生态

- **标准库**：HTTP 服务器、加密、JSON、模板——极其丰富
- **Docker / Kubernetes**：Go 编写
- **Terraform, Prometheus, Etcd**：云原生基础设施
- **CLI 工具**：hugo, lazydocker, fzf

## 关系

- [[rust]] — 系统编程竞品
- [[docker]]
- [[kubernetes]]
