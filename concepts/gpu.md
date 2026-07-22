---
title: GPU
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [hardware, gpu, model, training, inference]
sources: []
confidence: high
---

# GPU (Graphics Processing Unit)

## 定义

GPU 是专为**大规模并行计算**设计的处理器。最初用于图形渲染，2000 年代后期通过 CUDA 成为通用并行计算（GPGPU）的核心硬件。[[large-language-model]] 的训练和推理几乎全部依赖 GPU。

## GPU vs CPU

| 维度 | GPU | CPU |
|------|-----|-----|
| 核心数 | 数千个（小核心） | 4-32 个（大核心） |
| 设计目标 | 吞吐量优先 | 延迟优先 |
| 线程切换 | 几乎零成本 | 较高成本 |
| 缓存 | 较小 | 大而复杂 (L1/L2/L3) |
| 控制逻辑 | 极简 | 复杂（分支预测、乱序执行） |
| 适用场景 | 矩阵运算、并行任务 | 复杂逻辑、串行任务 |

## 关键概念

| 概念 | 说明 |
|------|------|
| CUDA Core | NVIDIA GPU 的计算单元 |
| Tensor Core | 专用矩阵乘法加速单元 (FP16/BF16/FP8/FP4) |
| SM (Streaming Multiprocessor) | 多个 CUDA Core 组成的调度单元 |
| VRAM / HBM | 显卡内存（HBM3e: 4.8 TB/s 带宽） |
| NVLink | GPU 间高速互联（900 GB/s） |

## 主流 GPU（用于 AI）

| GPU | VRAM | FP16 TFLOPS | 互联 | 定位 |
|-----|------|-------------|------|------|
| H100 | 80GB HBM3 | 989 | NVLink 900GB/s | 训练旗舰 |
| H200 | 141GB HBM3e | 989 | NVLink 900GB/s | 超大模型推理 |
| B200 | 192GB HBM3e | 2250 (FP8) | NVLink 1.8TB/s | 2024 新旗舰 |
| A100 | 40/80GB HBM2e | 312 | NVLink 600GB/s | 上一代旗舰 |
| RTX 4090 | 24GB GDDR6X | 330 | 无 NVLink | 消费旗舰 |
| HUAWEI Ascend 910B | 64GB HBM2e | 320 | HCCS | 国产替代 |
| AMD MI300X | 192GB HBM3 | 1307 (FP8) | Infinity Fabric | AMD 旗舰 |

## CUDA 编程模型

```cuda
// 核函数：在 GPU 上并行执行
__global__ void vector_add(float *a, float *b, float *c, int n) {
    int i = blockIdx.x * blockDim.x + threadIdx.x;
    if (i < n) c[i] = a[i] + b[i];
}
// block ⊂ grid, thread ⊂ block
```

## 瓶颈

- **显存墙**：H100 80GB 仍是很多大模型的瓶颈
- **互联带宽**：GPU 间通信比本地显存慢 10-100x
- **功耗**：单卡 700W，数据中心功耗惊人
- **供应**：NVIDIA 垄断，产能紧张

## 相关概念

- [[computer-architecture]]
- [[large-language-model]] — GPU 训练出来的
