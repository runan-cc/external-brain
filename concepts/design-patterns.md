---
title: 设计模式
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [pattern, programming, architecture, design]
sources: []
confidence: high
---

# 设计模式 (Design Patterns)

## 定义

设计模式是软件设计中**反复出现的问题的通用解决方案**。由 GoF (Gang of Four) 于 1994 年在《Design Patterns》一书中系统化，被称为"面向对象设计的圣经"。

## GoF 23 种模式

### 创建型 (Creational)

| 模式 | 意图 |
|------|------|
| Singleton | 确保一个类只有唯一实例 |
| Factory Method | 子类决定实例化哪个类 |
| Abstract Factory | 创建相关对象族 |
| Builder | 分步构造复杂对象 |
| Prototype | 克隆已有对象 |

### 结构型 (Structural)

| 模式 | 意图 |
|------|------|
| Adapter | 不兼容接口之间的桥梁 |
| Decorator | 动态添加职责 |
| Facade | 统一简化接口 |
| Proxy | 控制对象的访问 |
| Bridge | 抽象与实现分离 |
| Composite | 树形结构的一致处理 |
| Flyweight | 共享细粒度对象 |

### 行为型 (Behavioral)

| 模式 | 意图 |
|------|------|
| Observer | 一对多的依赖，状态变化通知 |
| Strategy | 算法族可互换 |
| Command | 请求封装为对象 |
| State | 对象行为随状态改变 |
| Template Method | 算法骨架，子类定制 |
| Iterator | 统一遍历方式 |
| Chain of Responsibility | 请求沿链传递 |
| Mediator | 协调对象交互 |
| Memento | 保存和恢复状态 |
| Visitor | 操作与数据结构分离 |

## 反模式 & 现代反思

| 反模式 | 说明 |
|--------|------|
| Singleton 滥用 | 全局状态 = 测试困难 + 隐藏依赖 = 很多场景应避免 |
| God Object | 一个类做所有事 |
| 过度工程 | 为"未来"加 5 层抽象 |
| Service Locator | 隐藏依赖（应用依赖注入替代） |

## 设计原则（超越 GoF）

| 原则 | 说明 |
|------|------|
| SOLID | 见 [[object-oriented-programming]] |
| DRY (Don't Repeat Yourself) | 消除重复 |
| KISS (Keep It Simple, Stupid) | 简单优先 |
| YAGNI (You Ain't Gonna Need It) | 不要为不存在的需求写代码 |
| Composition over Inheritance | 组合优于继承 |
| Law of Demeter | 只与直接朋友交谈 |
| Separation of Concerns | 关注点分离 |

## 模式在非 OOP 语言中

- **[[rust]]**：Trait = 策略模式，Enum + match = 状态模式
- **[[go]]**：interface + struct 组合 = 策略/装饰器
- **函数式**：高阶函数 = 策略/模板方法，Monad = 责任链
- **许多模式的本质是弥补语言表达力的不足**

## 关系

- [[object-oriented-programming]]
- [[functional-programming]]
- [[programming-paradigms]]
