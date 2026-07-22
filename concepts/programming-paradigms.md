---
title: 编程范式
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [programming, architecture, comparison, language]
sources: []
confidence: high
---

# 编程范式

## 定义

编程范式是编程的**思维模型和风格**。同一语言常支持多种范式，但通常以一种为主导。

## 主要范式

### 命令式 (Imperative)
"告诉计算机**怎么做**"——一条条指令改变程序状态。

- **过程式 (Procedural)**：`C`, Pascal — 通过函数组织代码
- **面向对象 (OOP)**：`Java`, `C++`, `Python` — 数据+方法封装为对象

### 声明式 (Declarative)
"告诉计算机**要什么**"——描述结果而非过程。

- **函数式 (Functional)**：`Haskell`, `Clojure`, `Elm` — 不可变数据、纯函数、高阶函数
- **逻辑式 (Logic)**：`Prolog` — 基于规则和关系的推理
- **SQL / 查询式**：`SQL` — 声明查询而非如何获取数据

### 响应式 (Reactive)
数据流和变化传播——`RxJS`, `ReactiveSwift`, React Hooks

## 面向对象 (OOP) 核心

| 概念 | 说明 |
|------|------|
| 封装 (Encapsulation) | 数据和操作打包在一起 |
| 继承 (Inheritance) | is-a 关系 |
| 多态 (Polymorphism) | 同一接口、不同实现 |
| 抽象 (Abstraction) | 隐藏实现细节 |

OOP 的现代反思：**组合优于继承 (Composition over Inheritance)**

## 函数式编程 (FP) 核心

| 概念 | 说明 |
|------|------|
| 纯函数 | 相同输入 → 相同输出，无副作用 |
| 不可变性 | 不修改已有数据，创建新数据 |
| 高阶函数 | 函数接受/返回函数 (`map`, `filter`, `reduce`) |
| 柯里化 (Currying) | 多参数函数 → 单参数函数链 |
| Monad | 抽象的计算上下文 (Maybe, Either, IO) |

## 范式对比

| 维度 | OOP | FP |
|------|-----|-----|
| 核心抽象 | 对象（数据+行为） | 函数（输入→输出） |
| 状态管理 | 可变、分散在对象中 | 不可变、集中管理 |
| 代码复用 | 继承/组合 | 高阶函数/Monad |
| 并发友好 | 需要锁/同步 | 天然线程安全 |
| 学习曲线 | 中 | 高 |

## 现代趋势：多范式融合

- **Rust**：过程式 + FP（Trait, Iterator）+ OOP（无继承）
- **Python**：OOP + 过程式 + 部分 FP
- **TypeScript**：OOP + FP（React 函数式）
- **Go**：极简 OOP（无继承）+ 过程式
- **Scala/Kotlin**：OOP + FP 深度融合

## 关系

- [[object-oriented-programming]]
- [[functional-programming]]
