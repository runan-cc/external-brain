---
title: CPU 微架构
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [cpu, hardware, architecture, performance]
sources: []
confidence: high
---

# CPU 微架构

## 定义

CPU 微架构是**指令集架构 (ISA) 的具体硬件实现**。同一 ISA（如 x86-64）可以有完全不同的微架构（如 Intel Golden Cove 和 AMD Zen 4）。微架构决定了实际的性能、能效和功能。

## 指令执行流水线

经典五级流水线：

```
IF → ID → EX → MEM → WB
↑    ↑    ↑    ↑     ↑
取指 译码  执行  访存  写回
```

### 流水线冒险 (Hazards)

| 类型 | 说明 | 解决 |
|------|------|------|
| 结构冒险 | 硬件资源冲突 | 增加硬件（Harvard Architecture：独立 I-Cache/D-Cache） |
| 数据冒险 | 指令依赖前面指令的结果 | Forwarding / Bypassing + 停顿 |
| 控制冒险 | 分支导致不需要流水 | 分支预测 + 推测执行 |

## 现代 CPU 关键技术

### 超标量 (Superscalar)
每个时钟周期发射多条指令到多个执行单元。IPC > 1。

### 乱序执行 (Out-of-Order / OoO)
指令按**数据就绪**而非程序顺序执行。

```
程序顺序:  A = load X     (cache miss, 200 cycles)
            B = A + 1     (等待 A)
            C = 2 * 3     (独立，可以先执行！)

OoO 调度器:
  → 发现 C 不依赖 A → 先执行 C
  → 等 A 从内存回来后执行 B
```

需要：寄存器重命名 (Register Renaming)、Reservation Station、Reorder Buffer (ROB)。

### 分支预测 (Branch Prediction)

| 技术 | 说明 |
|------|------|
| 静态预测 | 总是预测跳转/不跳转（回溯边跳转） |
| 动态预测 | 基于历史（Bimodal、Two-level、GShare） |
| TAGE | 多长度历史混合预测，现代标准 |
| Perceptron | 神经网络预测，AMD Zen 使用 |

分支预测错误 = 清空流水线 + 回滚（~15-20 cycles 损失，Meltdown/Spectre 的根源）。

### 推测执行 (Speculative Execution)
在分支结果未知时**先执行预测方向**的指令。预测对：白赚；预测错：回滚 + 代价。

→ **Spectre / Meltdown (2018)**：推测执行留下的微架构侧信道可被利用读取内核内存。

### 缓存层次

```
L1 I-Cache (32KB, 4-5 cycles)
L1 D-Cache (32-48KB, 4-5 cycles)
L2 Cache (256KB-1MB, ~12 cycles)
L3 Cache (8-32MB shared, ~40 cycles)
DRAM (~100 ns, ~200+ cycles)
```

- **L1**：每个核心独立，极快极贵
- **L2**：核心独立或每核集群共享
- **L3/LLC**：所有核心共享，越大越好（AMD 3D V-Cache）

### 缓存一致性 (Cache Coherence)

多核共享内存时的协议：

| 协议 | 使用 |
|------|------|
| MESI | Intel x86 |
| MOESI | AMD |
| MESIF | Intel (QuickPath) |

**MESI 状态**：
| 状态 | 含义 |
|------|------|
| Modified | 只有我有，已修改，需写回 |
| Exclusive | 只有我有，未修改 |
| Shared | 多核共有，未修改 |
| Invalid | 无效（其他核已修改） |

## SMT (Simultaneous Multi-Threading) / Hyper-Threading

同一核心同时运行两个线程，共享执行单元。吞吐 +30%，但不等于两倍核心。

## Intel vs AMD 微架构

| 维度 | Intel | AMD |
|------|-------|-----|
| 当前架构 | Lion Cove (Arrow Lake) / Redwood Cove | Zen 5 |
| 设计哲学 | 高频率 + 大核心 | Chiplet + 高核心数 |
| AVX-512 | 混合支持 | 全支持 |
| 3D V-Cache | 无 | ✅ (游戏性能王者) |

## 关系

- [[computer-architecture]] — ISA 层面
- [[digital-logic]] — 门级实现
- [[gpu]] — GPU 是完全不同的微架构思路
