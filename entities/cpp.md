---
title: C++
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [cpp, language, programming, systems]
sources: []
confidence: high
---

# C++

## 概览

C++ 是 Bjarne Stroustrup 于 1985 年创建的**多范式编程语言**，在 [[c-language]] 基础上增加了面向对象、泛型编程和函数式特性。以"零成本抽象"著称——高级特性不引入运行时开销。

## 核心特性

- **多范式**：过程式、面向对象、泛型、函数式
- **零成本抽象**：你不对不使用的特性付费
- **RAII** (Resource Acquisition Is Initialization)：资源由对象生命周期管理，无需手动 try-finally
- **模板元编程**：编译时计算和代码生成
- **Move 语义**（C++11）：避免不必要的拷贝

## 现代 C++ 演进

| 标准 | 年份 | 关键特性 |
|------|------|----------|
| C++11 | 2011 | auto, lambda, move, smart pointers |
| C++14 | 2014 | 泛型 lambda, `make_unique` |
| C++17 | 2017 | `if constexpr`, structured bindings, `std::optional` |
| C++20 | 2020 | Concepts, Ranges, Coroutines, Modules |
| C++23 | 2023 | `std::expected`, `std::mdspan` |
| C++26 | 2026(WIP) | Reflection, Contracts |

## 应用场景

| 领域 | 说明 |
|------|------|
| 游戏引擎 | Unreal Engine, Unity (底层) |
| 数据库 | MySQL, MongoDB, ClickHouse |
| 浏览器 | Chrome (Blink+V8), Firefox (Gecko+SpiderMonkey) |
| 量化交易 | 纳秒级延迟 |
| 计算机视觉 | OpenCV |
| LLM 推理 | llama.cpp, GGML |

## 关系

- [[c-language]] — 子集和基础
- [[rust]] — 现代安全替代
- [[go]] — 不同哲学（简洁 vs 强大）
