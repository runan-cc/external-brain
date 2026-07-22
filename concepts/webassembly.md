---
title: WebAssembly (WASM)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [web, architecture, performance, browser]
sources: []
confidence: high
---

# WebAssembly (WASM)

## 定义

WebAssembly 是浏览器中的**底层字节码格式**，允许 C/C++/Rust/Go 等语言编译后在浏览器中以接近原生的速度运行。2019 年成为 W3C 标准，是继 HTML/CSS/JS 后的 Web 第四语言。

## 为什么 WASM

| 问题 | WASM 答案 |
|------|-----------|
| [[javascript]] 性能不够 | WASM 接近原生速度 |
| 计算密集型任务 | 编译后的 C/Rust 代码 |
| 复用已有代码 | C++ 游戏引擎 → 浏览器 |
| 安全沙箱 | WASM 运行在隔离环境中 |

## 架构

```
┌──────────────────────────────┐
│  C / C++ / Rust / Go / Zig   │  高级语言
├──────────────────────────────┤
│     编译器 (Emscripten,       │
│     wasm-pack, TinyGo)       │  编译
├──────────────────────────────┤
│      WebAssembly (.wasm)     │  可移植字节码
├──────────────────────────────┤
│      WASM Runtime            │  V8 / SpiderMonkey
└──────────────────────────────┘
```

## WASI（WebAssembly System Interface）

WASM 在浏览器外的系统接口标准，使 WASM 可以在服务器、边缘、IoT 中运行。WASM + WASI 被视为替代 [[docker]] 容器的潜力方案（更安全、更快启动、真正跨平台）。

## 应用场景

| 场景 | 示例 |
|------|------|
| 浏览器高性能计算 | Figma (C++ → WASM), Photoshop Web |
| 游戏引擎 | Unity/Unreal → Web |
| 边缘计算 | Cloudflare Workers (WASM), Fastly |
| 插件系统 | Envoy Proxy WASM filters |
| 区块链 | 智能合约 (Polkadot, NEAR) |

## 局限性

- 不能直接操作 DOM（需通过 JS 桥接）
- 启动时间仍有优化空间
- 调试工具不如 JS 成熟
- GC 语言（Java/Go）编译体积大

## 相关概念

- [[rust]] — WASM 最佳语言之一
- [[javascript]] — 与 JS 互补
- [[docker]] — 潜在的替代方案
