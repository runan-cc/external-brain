---
title: Turing Machine
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [theory, computation, mathematics]
sources: []
confidence: high
---

# Turing Machine（图灵机）

## 定义

图灵机是 Alan Turing 于 1936 年提出的**抽象计算模型**，定义了"什么是可计算的"。它是整个计算机科学理论的基础——任何可计算的问题都可以用图灵机解决。

## 结构

```
┌──────────────────────────┐
│  有限状态控制 (Finite       │
│  State Control)            │
│       ↓                    │
│  ┌─────────┐              │
│  │ 读写头    │               │
│  └────┬────┘               │
│       ↓                    │
│ ... │ B │ a │ n │ a │ n │ ...
│              纸带 (Tape)   │
│           (无限长度)        │
└──────────────────────────┘
```

- **纸带**：无限长度的存储（相当于内存）
- **读写头**：读取/写入当前格，左右移动
- **状态机**：根据当前状态和读到的符号决定下一步
- **转移函数 δ**：`δ(state, symbol) → (new_state, write_symbol, move_direction)`

## 关键特性

- **无限纸带**：理论上无限内存
- **确定性**：给定状态和输入，转移唯一确定
- **通用性**：存在**通用图灵机 (UTM)** 可以模拟任何图灵机
- **图灵完备**：能模拟图灵机的系统就是图灵完备的（几乎所有编程语言）

## 图灵完备性

一个系统是图灵完备的，如果它能模拟任意图灵机。

| 图灵完备 | 非图灵完备 |
|----------|-----------|
| Python, C, JS, Rust, Java, Go | 正则表达式 |
| HTML + CSS + JS | SQL（不含递归 CTE） |
| Minecraft 红石 | CSS (仅布局) |
| Magic: The Gathering | HTML (仅标记) |

## 停机问题 (Halting Problem)

> 不存在一个通用算法，能判断任意程序是否会在有限时间内停止。

**证明（反证法）：**
```
假设 halt(program, input) 存在。
构造 paradoxical(p)：
    if halt(p, p):
        loop_forever()    # 本来会停，偏不停
    else:
        return             # 本来不停，偏停
运行 paradoxical(paradoxical)：
    如果会停 → 进入循环（不停）→ 矛盾
    如果不停 → 返回（停）→ 矛盾
∴ halt() 不存在
```

停机问题说明了**存在不可计算的问题**——计算机能力有根本性上限。

## 变体

| 变体 | 特点 |
|------|------|
| 非确定性图灵机 (NTM) | 一个状态多条转移，NDTM 时间 = DTM 指数时间 |
| 多带图灵机 | 多纸带并行读写（等价于单带，但更快） |
| 量子图灵机 | 量子叠加态转移 |
| Oracle 图灵机 | 可查询一个"黑盒"oracle |

## Church-Turing 论题

> 所有"有效可计算"的函数都能被图灵机计算。

这不是定理（无法证明），但所有已知的计算模型都与其等价：
- λ 演算 ≈ 图灵机（可互相模拟）
- 递归函数 ≈ 图灵机
- 所有现代编程语言 ≈ 图灵机

## 关系

- [[computational-complexity]] — 图灵机定义了复杂度类
- [[compiler]] — 编译器的理论基础
- [[data-structures-and-algorithms]]
