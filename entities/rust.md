---
title: Rust
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [rust, language, programming, systems]
sources: []
confidence: high
---

# Rust

## 概览

Rust 是 Mozilla Research 主导开发（现由 Rust Foundation 维护）的**系统编程语言**，2015 年 1.0 发布。它在不牺牲性能的前提下保证内存安全和线程安全——不需要垃圾回收器（GC）。

## 核心特性

- **所有权 (Ownership)**：每个值有唯一所有者，离开作用域自动释放
- **借用 (Borrowing)**：`&T`（不可变借用）和 `&mut T`（可变借用）
- **生命周期 (Lifetimes)**：编译器静态验证引用不会悬空
- **Trait 系统**：类似 interface + typeclass，无继承
- **模式匹配**：`match` 和 `if let` 表达力极强

## Rust vs C++

| 维度 | Rust | C++ |
|------|------|-----|
| 内存安全 | 编译时保证 | 开发者自己保证 |
| 包管理 | Cargo（内置） | 多种（CMake/vcpkg/Conan） |
| 学习曲线 | 陡峭（所有权概念） | 中等 |
| 编译速度 | 较慢 | 也慢 |
| 并发安全 | 类型系统保证 | 需要小心 |

## 生态系统

- **Cargo**：内置包管理器和构建系统
- **crates.io**：官方包注册表
- **rust-analyzer**：IDE 支持（VS Code 等）
- **WASM**：Rust → WebAssembly 编译

## 应用场景

- **系统编程**：操作系统、驱动、嵌入式
- **CLI 工具**：ripgrep, fd, bat, delta
- **WebAssembly**：前端计算密集型
- **网络服务**：高性能代理、数据库（TiKV, Sled）
- **Infrastructure**：npm registry, Deno, SWC

## 关系

- [[go]] — 竞合关系（系统编程 vs 服务端开发）
- [[c-language]]
- [[cpp]]
- [[webassembly]]
