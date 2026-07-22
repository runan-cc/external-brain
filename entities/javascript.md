---
title: JavaScript
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [javascript, language, programming, web]
sources: []
confidence: high
---

# JavaScript

## 概览

JavaScript 是 Brendan Eich 于 1995 年在 Netscape 中创建的**动态脚本语言**，是 Web 的三大核心技术之一（HTML + CSS + JS）。最初用于浏览器交互，目前通过 [[nodejs]] 等运行时成为全栈语言。

## 核心特性

- **事件驱动 / 异步编程**：回调 → Promise → async/await
- **原型继承**：而非传统的类继承（ES6 class 是语法糖）
- **动态类型**：变量类型运行时决定
- **一等公民函数**：函数可作为参数传递（高阶函数）

## ES6+ 关键特性

| 特性 | 说明 |
|------|------|
| let / const | 块作用域变量声明 |
| Arrow Functions | `=>` 简洁函数语法 |
| Destructuring | 解构赋值 |
| Spread / Rest | `...` 展开和收集 |
| Modules | `import` / `export` |
| async/await | 异步代码同步写法 |

## 运行环境

| 环境 | 说明 |
|------|------|
| 浏览器 | 原始运行环境，通过 V8/SpiderMonkey 引擎执行 |
| [[nodejs]] | 服务端运行时 |
| Deno | TS 原生，安全优先 |
| Bun | 高性能（Zig 编写） |

## 关系

- [[typescript]] — JS 的类型超集
- [[nodejs]] — 服务端运行时
- [[react]] — 最流行的 UI 框架
- [[html]] — 标记结构
- [[css]] — 样式
