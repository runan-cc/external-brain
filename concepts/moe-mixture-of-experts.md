---
title: MoE (Mixture of Experts)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [model, architecture, training, scaling]
sources: []
confidence: high
---

# MoE (Mixture of Experts)

## 定义

MoE（混合专家）是一种神经网络架构，将模型的 FFN 层划分为多个"专家"子网络，每个 token 只激活其中 **一部分** 专家。这实现了**参数量的指数级增长而计算量几乎不变**——是 scaling law 的重要实现路径。

## 工作原理

```
Input → Router (Softmax) → Top-K 专家被激活 → 加权求和 → Output
                             其余专家闲置
```

- **Router/Gate**：一个小型网络，决定每个 token 应该发给哪些专家
- **Sparse activation**：只有 Top-K（通常 K=2）专家被激活
- **Load balancing loss**：额外损失项，防止某几个专家被过度使用

## 关键变体

| 变体 | 代表 | 特点 |
|------|------|------|
| Soft MoE | - | 软路由，所有专家都参与，加权更大 |
| DeepSeekMoE | [[deepseek]] V2/V3 | 细粒度专家 + 共享专家 (shared experts) |
| Mixtral | Mistral | 8×7B MoE（8 个专家，每次激活 2 个） |
| ST-MoE | Google | 引入稳定训练技巧（Z-loss, router variance） |

## 优势

- **参数效率**：假设 8 个专家 × 10B 参数 = 80B 总参数，实际计算量仅 ~20B（激活 2 个）
- **更低的推理延迟**：每个 token 只通过 2-4 个专家，速度快于同参数量的 dense 模型
- **训练成本**：DeepSeek-V3（671B MoE）训练成本仅 $5.6M

## 挑战

- **显存占用**：所有专家都要加载到显存（即使不计算），高内存需求
- **负载均衡**：某些专家可能"过载"或"饥饿"
- **微调困难**：稀疏激活使 fine-tuning 更容易过拟合
- **Router collapse**：Router 可能退化到只选少数专家

## 相关概念

- [[large-language-model]]
- [[transformer-architecture]]
- [[deepseek]] — MoE 最佳实践者
- [[scaling-laws]]
