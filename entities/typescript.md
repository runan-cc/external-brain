---
title: TypeScript
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [typescript, javascript, language, programming]
sources: []
confidence: high
---

# TypeScript

## 概览

TypeScript 是 Microsoft 于 2012 年发布的 **JavaScript 超集**，添加了可选的静态类型系统。编译为纯 JavaScript 后在任何支持 JS 的环境中运行。目前是前端开发的主流语言，并日益渗透到后端（Node.js/Bun/Deno）。

## 核心特性

- **静态类型检查**：编译时发现类型错误，减少运行时 bug
- **类型推断**：自动推断变量类型，减少标注负担
- **接口和泛型**：实现复杂类型的组合和复用
- **最新 JS 特性**：提前使用尚在 Stage 3 的 JS 提案
- **工具链**：通过 tsc 编译器 + tsconfig.json 配置

## TypeScript vs JavaScript

| 维度 | TypeScript | JavaScript |
|------|-----------|------------|
| 类型安全 | 编译时类型检查 | 运行时才能发现 |
| IDE 支持 | 极佳的智能提示和重构 | 较弱 |
| 学习曲线 | 中（需学类型系统） | 低 |
| 开发效率 | 大型项目更高 | 小型脚本更快 |

## 生态

| 框架 | TypeScript 支持 |
|------|----------------|
| React | 优秀（自带类型定义） |
| Next.js | 原生支持 |
| Vue 3 | 原生 TS 支持 |
| Node.js | 通过 ts-node/tsx 运行 |
| Express/Fastify | 有类型定义 |

## 关系

- [[javascript]] — 超集和运行时
- [[nodejs]] — 服务端运行时
- [[react]] — 最常用的 UI 框架
