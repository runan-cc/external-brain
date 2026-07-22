---
title: Fine-tuning
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [training, fine-tuning, optimization, data]
sources: []
confidence: high
---

# Fine-tuning（微调）

## 定义

Fine-tuning 是在预训练 [[large-language-model]] 的基础上，使用特定领域或任务的数据进行额外训练，使模型适应该领域或任务。与 prompt engineering 不同，fine-tuning **改变模型参数**。

## 微调方法

### Full Fine-tuning

更新模型所有参数。效果最好，但显存和计算成本极高（全量微调 GPT-4 级别模型需要数百 GB 显存）。

### Parameter-Efficient Fine-Tuning (PEFT)

| 方法 | 原理 | 可训参数量 |
|------|------|-----------|
| LoRA | 注入低秩矩阵，只训练矩阵参数 | <1% |
| QLoRA | LoRA + 4-bit 量化 | <1% |
| Adapter | 在层间插入小型适配网络 | 1-5% |
| Prefix Tuning | 在输入前添加可训练虚拟 token | <0.1% |
| IA3 | 只缩放激活值，仅 3 个向量 | ~0.01% |

### 指令微调 (Instruction Tuning)

使用 `(指令, 回答)` 对训练，让模型学会遵循指令。是 ChatGPT 等模型的基础。

### RLHF (Reinforcement Learning from Human Feedback)

1. 收集人类偏好数据（对多个回答排序）
2. 训练奖励模型（Reward Model）
3. 用 PPO/DPO 优化模型，使输出更符合人类偏好

DPO (Direct Preference Optimization) 是 RLHF 的简化版，直接优化偏好数据，不需要单独的奖励模型。

## 何时选择 Fine-tuning vs Prompt Engineering

| 场景 | 推荐 |
|------|------|
| 快速迭代、简单任务 | [[prompt-engineering]] |
| 特定领域术语/风格 | Fine-tuning |
| 减少 prompt 长度（降低成本） | Fine-tuning |
| 需要模型学会新能力 | Fine-tuning |
| 多任务通用场景 | [[prompt-engineering]] |

## 相关概念

- [[large-language-model]]
- [[prompt-engineering]]
- [[lora]] — LoRA 技术详解
