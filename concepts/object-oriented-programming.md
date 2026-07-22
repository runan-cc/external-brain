---
title: Object-Oriented Programming
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [programming, architecture, pattern]
sources: []
confidence: high
---

# Object-Oriented Programming (OOP)

## 定义

OOP 是将程序组织为**对象**的编程范式——对象封装数据（属性）和行为（方法）。由 Alan Kay 在 Smalltalk 中倡导，通过 [[java]], [[cpp]], [[python]] 成为主导范式。

## 四大支柱

| 支柱 | 含义 | 示例 |
|------|------|------|
| 封装 | 隐藏内部实现，暴露接口 | private/public, getter/setter |
| 继承 | 子类复用父类代码 | `class Dog extends Animal` |
| 多态 | 同一接口不同行为 | `Animal.speak()` → 不同的声音 |
| 抽象 | 提取公共特性，忽略细节 | Abstract class / Interface |

## SOLID 原则

| 原则 | 说明 |
|------|------|
| **S**ingle Responsibility | 一个类只有一个职责 |
| **O**pen/Closed | 对扩展开放、对修改关闭 |
| **L**iskov Substitution | 子类必须能替换父类 |
| **I**nterface Segregation | 不应强迫使用不需要的接口 |
| **D**ependency Inversion | 依赖抽象而非具体实现 |

## 设计模式（GoF 经典）

| 类别 | 模式 |
|------|------|
| 创建型 | Singleton, Factory, Builder, Prototype |
| 结构型 | Adapter, Decorator, Facade, Proxy, Composite |
| 行为型 | Observer, Strategy, Command, State, Iterator |

## OOP 的困境

- **继承地狱**：深层继承链难以理解和维护
- **上帝对象**：一个类做太多事情
- **贫血模型**：对象只有 getter/setter，逻辑全在 Service
- **过度工程**：为"未来扩展"而过度抽象

> 现代共识：**组合优于继承(Composition over Inheritance)。** 用接口 + 依赖注入替代深层继承。

## 关系

- [[programming-paradigms]]
- [[functional-programming]]
- [[java]], [[cpp]], [[python]]
