---
title: 模型量化
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [quantization, inference, optimization, llm]
sources: []
confidence: high
---

# 模型量化 (Quantization)

## 定义

模型量化是将模型权重和激活值从**高精度（FP32/FP16）转换为低精度（INT8/INT4）**的技术——大幅降低内存和计算需求，同时尽量保持精度。是 LLM 本地部署的必备技术。

## 为什么量化

| 精度 | 每个参数 | 70B 模型内存 | 相对 |
|------|----------|-------------|------|
| FP32 | 4 bytes | 280 GB | 基线 |
| FP16/BF16 | 2 bytes | 140 GB | 2x |
| INT8 | 1 byte | 70 GB | 4x |
| INT4 | 0.5 byte | 35 GB | 8x |
| INT2 | 0.25 byte | 17.5 GB | 16x |

INT4 可以把 70B 模型塞进一张 RTX 3090 (24GB) + 部分 CPU offload。

## 量化方法

### 训练后量化 (PTQ)

不需要重新训练，直接用校准数据确定量化参数。

| 方法 | 精度 | 速度 | 内存 | 特点 |
|------|------|------|------|------|
| **GPTQ** | INT4/INT8 | 快 | 低 | 层逐层量化，GPU 加速，需校准数据 |
| **AWQ** | INT4 | 快 | 低 | 按权重重要性加权量化 |
| **GGUF (llama.cpp)** | INT2-INT8 | 中 | 极低 | CPU 推理优先，mmap 加载 |
| BitsAndBytes (BNB) | INT4/INT8 | 快 | 低 | QLoRA 的基础 |
| SmoothQuant | INT8 | 快 | 中 | 平滑激活值离群点 |

### 量化感知训练 (QAT)

在训练过程中模拟量化噪声，模型学会补偿精度损失。效果好于 PTQ 但需要重新训练。

## QLoRA

[[lora]] + 量化 = 在 4-bit 模型上微调适配器：

```
基模型: 4-bit 量化（NF4 + 双重量化）
LoRA 适配器: FP16/BF16
训练: 反向传播只更新 LoRA 权重
```

→ 48GB GPU 上微调 65B 模型（原来需要 780GB）

## GGUF 格式

llama.cpp 的模型格式：

| 量化级别 | 类型 | 质量 |
|----------|------|------|
| Q8_0 | 8-bit | 几乎无损 |
| Q6_K | 6-bit | 极好 |
| Q5_K_M | 5-bit | 好 |
| Q4_K_M | 4-bit | 推荐默认（质量/大小平衡） |
| Q3_K_M | 3-bit | 有损失、可接受 |
| Q2_K | 2-bit | 很糊 |

## 关键权衡

| 指标 | 高精度 | 低精度 |
|------|--------|--------|
| 质量 | ✅ | 有损 |
| 内存 | 大 | ✅ 小 |
| 速度 | 慢 | ✅ 快 |
| 硬件支持 | 任何 GPU | 需要 INT4/INT8 支持 |

> 大模型 + 低精度 > 小模型 + 高精度（经验法则）

## 关系

- [[large-language-model]]
- [[lora]]
- [[gpu]] — GPU 的 TFLOPS 规格影响量化推理性能
