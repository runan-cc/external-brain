---
title: 编译原理
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [compiler, language, systems]
sources: []
confidence: high
---

# 编译原理

## 定义

编译原理研究**如何将高级语言源码转化为机器可执行的代码**。编译器是计算机科学中最成熟的领域之一，也是理解语言和系统的基础。

## 编译阶段

```
源代码
  ↓
1. 词法分析 (Lexer)    → Token 流
  ↓
2. 语法分析 (Parser)   → AST (抽象语法树)
  ↓
3. 语义分析            → 类型检查、符号表
  ↓
4. 中间代码生成 (IR)   → LLVM IR / 三地址码
  ↓
5. 优化 (Optimizer)    → 常量折叠、死代码消除、内联...
  ↓
6. 目标代码生成        → 汇编/机器码
  ↓
7. 链接 (Linker)       → 可执行文件
```

## 核心概念

| 概念 | 说明 |
|------|------|
| AST | Abstract Syntax Tree，源码的结构化树表示 |
| Symbol Table | 变量、函数等标识符的映射表 |
| IR (Intermediate Representation) | 中间表示，LLVM IR 是行业标准 |
| SSA (Static Single Assignment) | 每个变量只赋值一次，便于优化 |
| CFG (Control Flow Graph) | 程序控制流图 |

## 编译器 vs 解释器

| 维度 | 编译器 | 解释器 |
|------|--------|--------|
| 执行方式 | 先翻译、后执行 | 边读边执行 |
| 速度 | 快 | 慢 |
| 灵活性 | 需要编译步骤 | 即时修改 |
| 代表 | C/C++, Rust, Go | Python, JS, Ruby |

**现代主流：JIT（Just-In-Time）编译**
- 解释执行 + 热点编译 = 两者优势结合
- 代表：JVM (HotSpot), V8 (TurboFan), .NET CLR

## LLVM

| 组件 | 功能 |
|------|------|
| Clang | C/C++/ObjC 前端 |
| LLVM IR | 统一中间表示 |
| LLVM Optimizer | 目标无关优化 |
| LLVM Backend | 目标架构代码生成 |

被 Rust, Swift, Julia, Kotlin/Native 等新语言广泛采用。

## 关系

- [[c-language]] — 编译器最常编译的语言
- [[cpp]] — 最复杂的编译目标
- [[rust]] — 使用 LLVM，前沿编译器技术
