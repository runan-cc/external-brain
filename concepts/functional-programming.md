---
title: Functional Programming
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [programming, architecture, pattern]
sources: []
confidence: high
---

# Functional Programming (FP)

## 定义

函数式编程是以**数学函数**为核心的编程范式。它强调不可变数据、纯函数和声明式表达，根植于 Lambda 演算。随着 [[react]]、[[rust]] 和 [[scala]]/Kotlin 的流行，FP 思想正广泛渗透到主流语言。

## 核心原则

### 纯函数
```
相同输入 → 相同输出，无副作用
```
可测试、可缓存、可并行——FP 的基石。

### 不可变性
不修改现有数据，而是创建新数据。React 的 `setState`、Redux、[[rust]] 的所有权系统都是其延伸。

### 高阶函数
函数是一等公民——可作为参数传递和返回：
```javascript
[1,2,3].map(x => x * 2)        // [2,4,6]
[1,2,3].filter(x => x > 1)     // [2,3]
[1,2,3].reduce((a,b) => a+b, 0) // 6
```

### 函数组合
```javascript
const upperCaseHead = compose(
  toUpperCase,
  head
)
upperCaseHead(['hello', 'world']) // 'HELLO'
```

## 关键概念

| 概念 | 说明 |
|------|------|
| Functor | 可映射的容器 (`Array.map`, `Optional.map`) |
| Applicative | 在上下文中应用函数 |
| Monad | 可链式计算的上下文 (`Promise`, `Optional`, `Either`) |
| Currying | `f(a,b,c)` → `f(a)(b)(c)` |
| Pattern Matching | 按模式解构和匹配数据 |

## FP vs OOP

| 维度 | FP | [[object-oriented-programming]] |
|------|-----|------|
| 数据 | 不可变 | 可变 |
| 逻辑组织 | 函数组合 | 对象方法 |
| 状态 | 无状态优先 | 有状态 |
| 并发 | 天然安全 | 需要同步机制 |
| 测试 | 极简单（纯函数） | 需要 mock 对象 |

## 现实中的 FP

- **React Hooks**：函数式 UI 范式
- **Rust Iterator**：惰性求值链式操作
- **Kotlin/Java Streams**：`filter/map/collect`
- **SQL**：声明式数据处理（本质是 FP）

## 关系

- [[programming-paradigms]]
- [[object-oriented-programming]]
