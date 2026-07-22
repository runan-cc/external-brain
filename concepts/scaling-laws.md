---
title: Scaling Laws
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [scaling, training, model, architecture]
sources: []
confidence: high
---

# Scaling Laws（缩放定律）

## 定义

Scaling laws 描述了 [[large-language-model]] 性能与**参数量 (N)、数据量 (D)、计算量 (C)** 之间的可预测幂律关系。由 OpenAI 在 2020 年发表于论文 "Scaling Laws for Neural Language Models"，Karpathy 称之为"AI 领域最重要的发现之一"。

## 核心关系

$$L(N, D) \propto N^{-\alpha} + D^{-\beta}$$

- 损失（Loss）随参数量和数据量的增加遵循幂律下降
- 没有明显的收益递减上限（至少在已有观测范围内）

## Chinchilla 最优

DeepMind (2022) 发现：此前所有模型都**训练不足**（参数太多，数据太少）。

Chinchilla 定律：最优的**训练 token 数 ≈ 20 × 参数量**
- 例如 70B 参数 → 需要 1.4T tokens 训练数据

这解释了为什么 Llama 系列用更多数据训练小模型能超越大模型。

## 三个扩展维度

| 维度 | 说明 |
|------|------|
| 模型规模 (N) | 更大的模型 → 更低 loss |
| 数据规模 (D) | 更多数据 → 更低 loss |
| 训练计算 (C) | N × D，同时增长效果最好 |

## 超越 Scaling Laws

- **Inference-time compute**：o1/o3 模型通过增加推理时的计算量来提升性能
- **Data quality > Data quantity**：高质量数据比更多低质量数据有效
- **Architecture improvements**：MoE 让参数增长更快而计算增长更慢（见 [[moe-mixture-of-experts]]）
- **Synthetic data**：用 LLM 生成训练数据扩展数据量

## 局限

- Scaling 不能解决所有问题（如推理、事实准确性）
- 高质量数据接近耗尽（data wall）
- 训练成本指数级增长

## 相关概念

- [[large-language-model]]
- [[moe-mixture-of-experts]]
- [[transformer-architecture]]
