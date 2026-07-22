---
title: SIMD & NUMA
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [hardware, performance, architecture, optimization]
sources: []
confidence: high
---

# SIMD & NUMA

## SIMD (Single Instruction, Multiple Data)

### 定义

SIMD 是**一条指令同时处理多个数据**的并行计算模式。现代 CPU 的向量寄存器 (128-bit 到 512-bit) 可以一次处理 4-64 个 8-bit 值。

```
标量 (SISD):     [a] + [b] = [c]
SIMD:      [a1,a2,a3,a4] + [b1,b2,b3,b4] = [c1,c2,c3,c4]
                ↑               ↑               ↑
               一次指令，四个结果
```

### ISA 向量扩展

| 扩展 | 宽度 | ISA | 特点 |
|------|------|-----|------|
| SSE | 128-bit | x86 | 4×FP32 |
| AVX | 256-bit | x86 | 8×FP32 |
| **AVX-512** | 512-bit | x86 (服务器/部分消费级) | 16×FP32，ML 加速 |
| NEON | 128-bit | ARM | 4×FP32 |
| SVE/SVE2 | 128-2048 bit | ARM (服务器) | 可变宽度，更灵活 |
| V Extension | 可配置 | RISC-V | 向量化标准 |

### 在 AI/ML 中

```python
# PyTorch 底层用 SIMD 加速
# 矩阵乘法 → BLAS → AVX/AVX-512
# 卷积 → im2col + GEMM → NEON/Metal
```

- Intel AMX：x86 的矩阵加速器，专为大模型推理设计
- Apple AMX：M 系列的矩阵协处理器，Core ML 调用
- Neon → Apple M 系列的 GEMM 加速

### 编译器自动向量化

```c
// 编译器识别这个循环为 SIMD 友好的
for (int i = 0; i < 1024; i++)
    c[i] = a[i] + b[i];
// → 展开为 AVX: 一次处理 8 个 float
```

`-O3 -march=native` 通常能自动向量化。查询：`gcc -fopt-info-vec`

## NUMA (Non-Uniform Memory Access)

### 定义

多路服务器中，CPU 访问"本地"内存快、访问"远程"内存慢——这就是 NUMA。

```
┌───────────────┐     ┌───────────────┐
│  CPU Socket 0 │←──→│  CPU Socket 1 │
│  ┌──┐  ┌──┐  │ QPI │  ┌──┐  ┌──┐  │
│  │核│  │DDR│ │     │  │核│  │DDR│ │
│  └──┘  └──┘  │     │  └──┘  └──┘  │
│  快速 (本地)   │     │  慢 ~1.5×     │
└───────────────┘     └───────────────┘
```

| UMA (老) | NUMA (新) |
|----------|-----------|
| 所有 CPU 访问同一内存 | 每个 CPU 有本地内存 |
| 总线竞争瓶颈 | 扩展性好 |
| 双路以上基本不用 | 双路以上标配 |

### NUMA 对性能的影响

- 跨 NUMA 节点内存访问慢 1.3-2x
- 线程在 Socket A 上跑，数据在 Socket B 的 DDR → 性能下降
- 数据库、ML 训练等内存密集型应用**必须注意 NUMA**

### NUMA 优化

| 策略 | 说明 |
|------|------|
| `numactl --cpunodebind=0 --membind=0` | 程序和内存绑定同一 socket |
| 进程绑定 | `taskset` + NUMA 策略 |
| First-touch 策略 | 谁先写谁分配本地内存 |
| Linux 自动 | `numa_balancing` 尝试迁移页面 |

### NUMA 与 ML 训练

- 多 GPU 服务器通常有 2 个 CPU socket + 8 GPU
- GPU 和 CPU socket 之间有固定连接关系
- **GPU 和配对的 CPU socket + DDR 绑定 → IO 最快**
- NCCL 和 PyTorch DDP 需要考虑 NUMA 拓扑

## 关系

- [[instruction-set-architecture]]
- [[cpu-microarchitecture]]
- [[gpu]] — GPU 本质上是 SIMT
