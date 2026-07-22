---
title: C Language
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [c, language, programming, systems]
sources: []
confidence: high
---

# C Language

## 概览

C 是 Dennis Ritchie 于 1972 年在贝尔实验室开发的**系统编程语言**。它是 UNIX 操作系统的实现语言，也是几乎所有现代编程语言的"祖先"或参考。至今仍是嵌入式、操作系统内核和高性能计算的基石。

## 核心特性

- **编译型**：直接编译为机器码，无运行时开销
- **指针与手动内存管理**：`malloc` / `free`，没有 GC
- **极简语法**：32 个关键字（C89），极低的语言复杂度
- **接近硬件**：直接操作内存地址和寄存器
- **无 OOP**：通过 struct + 函数指针模拟

## C 在现代的位置

| 领域 | 说明 |
|------|------|
| 操作系统内核 | Linux, Windows, macOS 内核 |
| 嵌入式/IoT | 资源受限设备 |
| 数据库引擎 | SQLite, PostgreSQL, Redis |
| 语言 runtime | Python (CPython), Ruby (CRuby), Lua 解释器 |
| 加密库 | OpenSSL, libsodium |

## C vs C++

| 维度 | C | [[cpp]] |
|------|---|---------|
| 范式 | 过程式 | 多范式 (过程式+OOP+泛型) |
| 复杂度 | 极简 | 非常复杂 |
| 标准库 | 小巧 | STL 非常丰富 |
| 适用场景 | 底层/嵌入式 | 大型应用/游戏 |

## 关系

- [[cpp]] — 继承自 C 的 OOP 扩展
- [[rust]] — 现代内存安全替代
- [[linux]] — 用 C 写的
