---
title: VS Code
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [tool, editor, development]
sources: []
confidence: high
---

# Visual Studio Code (VS Code)

## 概览

VS Code 是 Microsoft 于 2015 年发布的**开源代码编辑器**。基于 Electron（Chromium + Node.js），是目前最流行的代码编辑器（Stack Overflow 调查中 ~75% 开发者首选）。

## 核心特性

- **开源**：MIT 协议，GitHub 上开发
- **扩展生态**：数万扩展，覆盖所有语言和工具
- **Language Server Protocol (LSP)**：标准化语言支持
- **集成终端**：内置 shell
- **Git 集成**：内置 Git GUI
- **Remote Development**：SSH、Container、WSL 远程开发
- **Copilot / AI 集成**：GitHub Copilot Chat, Cursor 类 AI 功能

## 主要分支/竞品

| 编辑器 | 特点 |
|------|------|
| VS Code | 原版，Microsoft 维护 |
| Cursor | AI-first 编辑器，基于 VS Code |
| Windsurf | Codeium 的 AI IDE |
| VSCodium | 去除了 Microsoft telemetry 的干净版 |

## 常用扩展

| 扩展 | 用途 |
|------|------|
| Python / Pylance | Python 开发 |
| ESLint / Prettier | 代码检查与格式化 |
| GitLens | 增强 Git 功能 |
| Remote - SSH | 远程开发 |
| GitHub Copilot | AI 编程助手 |

## 局限

- **Electron 内存占用**：大型项目可能吃 1-2GB
- **启动速度**：不如 Sublime/Vim 快
- **非完整 IDE**：对 Java/C# 支持不如 IntelliJ/Visual Studio

## 关系

- [[git]] — 内置集成
- [[python]] — 最常用的 Python 编辑器
