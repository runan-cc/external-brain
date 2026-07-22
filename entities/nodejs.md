---
title: Node.js
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [javascript, runtime, backend, programming]
sources: []
confidence: high
---

# Node.js

## 概览

Node.js 是 Ryan Dahl 于 2009 年创建的 **JavaScript 运行时**，基于 Chrome V8 引擎，使 JavaScript 可以脱离浏览器在服务器端运行。它以事件驱动、非阻塞 I/O 著称。

## 核心特性

- **事件循环（Event Loop）**：单线程 + 异步非阻塞 I/O
- **npm**：全球最大的包管理器，百万级包生态
- **CommonJS / ES Modules**：模块系统
- **Streams**：大数据处理的高效抽象

## 运行时生态

| 运行时 | 引擎 | 特点 |
|--------|------|------|
| Node.js | V8 | 最成熟，生态最大 |
| Deno | V8 | TS 原生，安全优先，由 Node 创始人创建 |
| Bun | JavaScriptCore | 极快（Zig 编写），原生打包/测试/bundler |
| WinterJS | SpiderMonkey | WASM-based |

## 常用框架

| 框架 | 特点 |
|------|------|
| Express | 老牌，最小化 |
| Fastify | 高性能，Schema-based |
| NestJS | 企业级，装饰器 + DI（类 Spring） |
| Next.js | React 全栈框架（服务端渲染） |
| Hono | 超轻量，边缘计算 |

## 关系

- [[typescript]] — 类型安全层
- [[docker]] — 容器化部署
