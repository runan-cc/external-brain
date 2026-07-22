---
title: 形式语言与自动机
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [theory, computation, compiler, formal-languages]
sources: []
confidence: high
---

# 形式语言与自动机

## 定义

形式语言理论研究**语言的形式化定义**以及**识别语言的机器（自动机）**。它是编译原理、正则表达式和计算理论的基础——回答了"什么样的语言能被机器识别"。

## Chomsky 层级

| 层级 | 语言 | 自动机 | 产生式规则 |
|------|------|--------|-----------|
| Type 3 | 正则语言 | **DFA / NFA** | A → aB, A → a |
| Type 2 | 上下文无关语言 | **PDA**（下推自动机） | A → γ |
| Type 1 | 上下文相关语言 | **LBA**（线性有界自动机） | αAβ → αγβ |
| Type 0 | 递归可枚举 | **Turing Machine** | 无限制 |

每层是上层的**真子集**：正则 ⊂ 上下文无关 ⊂ 上下文相关 ⊂ 递归可枚举

## 正则语言与有限自动机

### DFA (确定有限自动机)
- 有限状态、确定转移
- 等价于 [[regular-expressions]]
- 用于：词法分析（Lexer）、文本搜索

### NFA (非确定有限自动机)
- 同一输入可转移多个状态
- DFA 与 NFA 等价（可互相转换），但 NFA 更简洁

> 正则语言 ≠ 能计算的都能。例如 **aⁿbⁿ（n 个 a 后 n 个 b）不是正则的**——需要"计数"。

## 上下文无关语言与 PDA

### 下推自动机 (PDA)
有限自动机 + **栈**——有了记忆能力。

- 能识别 aⁿbⁿ（栈计数）
- 能识别括号匹配、HTML 标签嵌套
- **不能识别 aⁿbⁿcⁿ（需要两个栈 → 图灵机）**

### 上下文无关文法 (CFG)

```bnf
# 编程语言的文法
expr ::= expr + term | term
term ::= term * factor | factor
factor ::= ( expr ) | number
```

CFG 是**编译器前端**（Parser）的理论基础：
- **LL Parser**：自顶向下，左递归需消除
- **LR Parser**：自底向上，更强大（Yacc/Bison）

## 在编程中的应用

| 层次 | 应用 |
|------|------|
| 正则语言 | 词法分析 (Lexer), `grep`, 语法高亮 |
| 上下文无关 | 语法分析 (Parser), JSON/XML 解析 |
| 上下文相关 | 类型检查、声明使用匹配 |
| 图灵完备 | 整个程序语言 |

## 关系

- [[regular-expressions]] — 正则语言的实际使用
- [[compiler]] — 编译器实现
- [[turing-machine]] — Chomsky 最高层
- [[computational-complexity]]
