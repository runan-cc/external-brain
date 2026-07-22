---
title: 计算机体系结构
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [hardware, architecture, cpu, memory]
sources: []
confidence: high
---

# 计算机体系结构

## 定义

计算机体系结构研究计算机系统的组成和行为——从 CPU 微架构到内存层次再到 I/O 子系统。经典的 Von Neumann 架构将计算机分为五大部件。

## Von Neumann 架构

```
  控制单元 ←─→ 算术逻辑单元 (ALU)
       ↕
    内存 (指令+数据统一存储)
       ↕
    输入设备 ←→ 输出设备
```

**关键特征**：存储程序、指令与数据同址、顺序执行。

## CPU 核心概念

| 概念 | 说明 |
|------|------|
| ALU | 算术逻辑单元，执行运算 |
| 寄存器 | CPU 内最快存储（RAX, RBX 等） |
| 程序计数器 (PC) | 指向下一条指令地址 |
| 指令周期 | Fetch → Decode → Execute → Write-back |
| 流水线 (Pipeline) | 多条指令并行在不同阶段 |
| 分支预测 | 猜测分支走向，减少流水线停顿 |
| 超标量 | 一个时钟周期执行多条指令 |
| 乱序执行 | 不按程序顺序执行（只要数据依赖满足） |

## 内存层次结构 (Memory Hierarchy)

```
容量小、快、贵                     容量大、慢、便宜
─────────────────────────────────────────────────
寄存器 → L1 Cache → L2 Cache → L3 Cache → RAM → SSD/HDD
  <1ns     ~1ns       ~3ns       ~10ns     ~100ns  ~100μs
```

| 层级 | 典型大小 | 延迟 |
|------|----------|------|
| L1 Cache | 32-64KB/core | ~1ns |
| L2 Cache | 256-512KB/core | ~3ns |
| L3 Cache | 8-32MB shared | ~10ns |
| RAM (DDR5) | 16-128GB | ~100ns |
| NVMe SSD | 1-4TB | ~100μs |

## 指令集架构 (ISA)

| ISA | 特点 | 代表 |
|-----|------|------|
| x86-64 | CISC，兼容性极强 | Intel Core, AMD Ryzen |
| ARM | RISC，能效高 | Apple M 系列，Qualcomm, 手机 |
| RISC-V | 开源 RISC | 新兴，中国大力推动 |

### RISC vs CISC

| 维度 | RISC | CISC |
|------|------|------|
| 指令长度 | 固定（通常 32-bit） | 变长 |
| 指令数量 | 少（~50-150） | 多（>1000） |
| 寻址模式 | 少（Load/Store） | 多 |
| 编译器负担 | 大 | 小 |
| 解码复杂度 | 低 | 高 |

> 现代实际情况：x86 内部将 CISC 解码为类 RISC 微指令执行，ARM 也有越来越复杂的扩展。边界已经模糊。

## 相关概念

- [[von-neumann-vs-harvard]]
- [[cpu-vs-gpu]]
- [[c-language]] — 与硬件最近的编程语言
