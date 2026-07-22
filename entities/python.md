---
title: Python
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [python, language, programming]
sources: []
confidence: high
---

# Python

## 概览

Python 是 Guido van Rossum 于 1991 年创建的高级编程语言，以**简洁可读**著称。目前是 AI/ML 和数据科学领域的绝对主流语言。

## 核心特性

- **动态类型**：变量无需声明类型
- **缩进定界**：用缩进而非花括号定义代码块
- **解释执行**：通过 CPython 解释器运行
- **丰富的标准库**：batteries included
- **包管理**：pip, uv, poetry, conda

## 关键版本

| 版本 | 发布时间 | 重大特性 |
|------|----------|----------|
| Python 3.0 | 2008 | 不兼容 Python 2 |
| Python 3.8 | 2019 | `:=` 海象运算符 |
| Python 3.10 | 2021 | Structural Pattern Matching |
| Python 3.11 | 2022 | 大幅性能提升（10-60%） |
| Python 3.12 | 2023 | 新的 type 语法, GIL 改进 |
| Python 3.13 | 2024 | 可选自由线程（no-GIL 实验） |

## AI/ML 生态

| 库 | 用途 |
|------|------|
| PyTorch | 深度学习框架 |
| Transformers (Hugging Face) | 预训练模型 |
| LangChain | LLM 应用框架 |
| NumPy / Pandas | 数据处理 |
| FastAPI | Web API 框架 |

## 局限

- **GIL (Global Interpreter Lock)**：限制多线程 CPU 密集型任务
- **运行速度**：比 C++/Rust 慢 10-100 倍
- **类型系统**：静态类型检查依赖外部工具（mypy）
- **移动端/前端**：不是主要选择

## 关系

- [[git]] — 版本控制
- [[docker]] — 容器化部署
