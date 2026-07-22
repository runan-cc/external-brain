---
title: Instruction Set Architecture (ISA)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [hardware, instruction-set, cpu, architecture]
sources: []
confidence: high
---

# Instruction Set Architecture (ISA)

## 定义

ISA 是**软硬件之间的界面**——定义了 CPU 能执行哪些指令、寄存器如何组织、内存如何寻址。软件编译目标不是具体 CPU，而是 ISA。

同一 ISA (如 x86-64) → 不同的微架构实现 (Intel Golden Cove vs AMD Zen 5)。

见 [[cpu-microarchitecture]]

## x86-64

| 属性 | 值 |
|------|-----|
| 开发者 | Intel/AMD |
| 诞生 | 1978 (8086), 2003 (x86-64) |
| 类型 | CISC |
| 寄存器 | 16 个通用寄存器 (64-bit) |
| 指令长度 | 1-15 字节（变长） |
| 指令数 | ~1000+ (不断增长) |
| 主要场景 | PC、服务器、数据中心 |

### 特点
- **向后兼容**：1980 年的 8086 程序理论上能在现代 CPU 上跑
- **变长指令**：解码复杂、功耗大，但代码密度高
- **AVX/AVX-512**：SIMD 向量指令，一次处理多个数据

## ARM

| 属性 | 值 |
|------|-----|
| 开发者 | Arm Ltd.（授权模式） |
| 诞生 | 1985 |
| 类型 | RISC |
| 寄存器 | 31 个通用寄存器 |
| 指令长度 | 固定 4 字节 (ARM) / 2 或 4 字节 (Thumb) |
| 指令数 | ~200 |

### 授权模式
Arm 不生产芯片，**授权 ISA/设计**给他人：
- Apple：A17 Pro / M3（定制 + 架构授权）
- Qualcomm：Snapdragon（定制核）
- 联发科/华为：公版 Cortex 核

### Apple Silicon 革命 (2020)
- M1 → M4：ARM 证明其性能和能效在 PC/服务器领域也能击败 x86
- 引发行业地震：x86 的统治结束了吗？

## RISC-V

| 属性 | 值 |
|------|-----|
| 开发者 | UC Berkeley (2010) |
| 类型 | RISC |
| 授权 | **开源、免版税** |
| 指令长度 | 32 位基础 + 16 位压缩扩展 |
| 模块化 | 基础 ISA + 标准扩展 (M/A/F/D/V) |

### 为什么 RISC-V 重要

| 原因 | 说明 |
|------|------|
| 免版税 | 不需像 ARM 付授权费 |
| 开源 | 任何人都可设计 RISC-V 处理器 |
| 中国大力推 | 地缘政治因素，x86/ARM 可能断供 |
| 模块化 | 按需添加扩展，从 IoT 到超算 |
| 竞争中 | 生态年轻但增长极快 |

## CISC vs RISC

| 维度 | CISC (x86) | RISC (ARM, RISC-V) |
|------|-----------|---------------------|
| 指令 | 复杂、变长 | 简单、定长 |
| 指令数 | 多 (~1000+) | 少 (~200) |
| 一条指令能做的事 | 多（内存+运算） | 少（load 然后 compute） |
| 解码 | 复杂、功耗大 | 简单、功耗低 |
| 代码密度 | ✅ 高 | 较低（有压缩模式补偿） |
| 现代实际 | 内部也拆成 µOP（RISC-like） | 差距已模糊 |

> 现代 CPU 中 x86 前端将 CISC 指令解码为 **µOP (微操作)**，实际执行的是 RISC 风格微操作。CISC 的外壳，RISC 的内核。

## SIMD 指令

| ISA | SIMD 扩展 |
|-----|----------|
| x86 | MMX → SSE → AVX → AVX-512 |
| ARM | NEON → SVE/SVE2 |
| RISC-V | V Extension (Vector) |

SIMD = **一次指令处理多个数据**——CPU 的"批量处理加速器"。

## 在 ML 中

- AVX-512 / NEON 加速矩阵乘法
- Intel AMX (Advanced Matrix Extensions) — AI 专用矩阵指令
- Apple AMX (Apple's Matrix coprocessor) — M 系列的 AI 引擎

## 关系

- [[cpu-microarchitecture]]
- [[computer-architecture]]
- [[gpu]]
