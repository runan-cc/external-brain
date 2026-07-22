---
title: 数字逻辑基础
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [hardware, digital-logic, boolean-algebra]
sources: []
confidence: high
---

# 数字逻辑基础

## 定义

数字逻辑是计算机硬件的最底层理论基础——用布尔代数和逻辑门构建所有数字电路。从 AND 门到 CPU，都建立在这套体系之上。

## 布尔代数

| 运算 | 符号 | 真值表 |
|------|------|--------|
| AND | A·B | 1·1=1 否则 0 |
| OR | A+B | 0+0=0 否则 1 |
| NOT | Ā | 1→0, 0→1 |
| XOR | A⊕B | 不同=1 |
| NAND | (A·B)' | AND 再 NOT |
| NOR | (A+B)' | OR 再 NOT |

## 基本定律

| 定律 | 公式 |
|------|------|
| 交换律 | A+B = B+A, A·B = B·A |
| 结合律 | (A+B)+C = A+(B+C) |
| 分配律 | A·(B+C) = A·B + A·C |
| De Morgan | (A·B)' = A' + B', (A+B)' = A'·B' |
| 互补 | A + A' = 1, A·A' = 0 |

## 组合逻辑电路

输出**仅取决于当前输入**（无记忆）。

### 基本门电路

| 门 | 符号 | 晶体管数 (CMOS) |
|-----|------|-----------------|
| NOT | Y = Ā | 2 |
| NAND | Y = (AB)' | 4 |
| NOR | Y = (A+B)' | 4 |
| AND | Y = AB | 6 (NAND + NOT) |
| OR | Y = A+B | 6 (NOR + NOT) |
| XOR | Y = A⊕B | ~12 |

> NAND 和 NOR 是**万能门**——用它们可以构建任何逻辑电路。

### 组合电路示例

**半加器 (Half Adder)**：
- Sum = A ⊕ B
- Carry = A · B

**全加器 (Full Adder)**：
- Sum = A ⊕ B ⊕ Cin
- Carry = (A·B) + (Cin·(A⊕B))

### 多路复用器 (MUX)
根据选择信号从多个输入中选一个输出。
```
2:1 MUX: Y = (S'·I0) + (S·I1)
```

### 译码器 (Decoder)
n 位输入 → 2ⁿ 位输出（one-hot）。用于地址译码、指令译码。

## 时序逻辑电路

输出**取决于当前输入和之前的状态**——有记忆。

### 锁存器 (Latch)
| 类型 | 行为 |
|------|------|
| SR Latch | S=1: Set(Q=1), R=1: Reset(Q=0), S=R=1: 禁止 |
| D Latch | 使能 =1 → Q = D, =0 → Q 保持 |

### 触发器 (Flip-Flop)

| 类型 | 触发方式 | 特点 |
|------|----------|------|
| D Flip-Flop | 时钟边沿 | 最常用，Q = D（上一个时钟沿） |
| JK Flip-Flop | 时钟边沿 | J=K=1 时翻转，更灵活 |
| T Flip-Flop | 时钟边沿 | T=1 时翻转 |

D Flip-Flop 是寄存器的基础——N 个 D FF = N-bit 寄存器。

## FPGA vs ASIC

| 维度 | FPGA | ASIC |
|------|------|------|
| 原理 | 可编程逻辑块 | 一次性蚀刻硅片 |
| 性能 | 较低 | ✅ 最优 |
| 能耗 | 较高 | ✅ 最低 |
| 成本 | 单价高 | 大产时最低 |
| 开发周期 | ✅ 快 | 月-年 |
| 灵活性 | ✅ 可重配置 | 不可改 |
| 适用 | 原型、加速、小批量 | 手机芯片、比特币矿机 |

## 关系

- [[computer-architecture]] — 数字逻辑构建 CPU
- [[gpu]] — GPU 就是大规模并行数字电路
- [[turing-machine]] — 数字电路实现图灵机
