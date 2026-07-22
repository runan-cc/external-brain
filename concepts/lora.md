---
title: LoRA (Low-Rank Adaptation)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [fine-tuning, training, optimization, technique]
sources: []
confidence: high
---

# LoRA (Low-Rank Adaptation)

## 定义

LoRA 是 Microsoft 于 2021 年提出的**参数高效微调（PEFT）** 方法。它不修改原始模型权重，而是注入可训练的**低秩矩阵**，训练参数量通常不到原始模型的 1%。这是目前最流行的 [[fine-tuning]] 方法。

## 原理

对于原始权重矩阵 $W \in \mathbb{R}^{d \times k}$：

$$h = Wx + \frac{\alpha}{r} BAx$$

其中 $B \in \mathbb{R}^{d \times r}$, $A \in \mathbb{R}^{r \times k}$，$r \ll \min(d, k)$

- $r$（rank）通常选 4-64，越低越省显存
- $\alpha$ 缩放因子，控制 LoRA 更新幅度
- 只训练 $A$ 和 $B$，冻结 $W$

## 关键参数

| 参数 | 含义 | 典型值 |
|------|------|--------|
| r (rank) | 低秩矩阵的秩 | 8, 16, 32, 64 |
| alpha | 缩放因子 | r 的 1-2 倍 |
| target_modules | 哪些层注入 LoRA | q_proj, v_proj, all linear |
| dropout | LoRA dropout | 0.05-0.1 |

## 变体

- **QLoRA**：LoRA + 4-bit 量化，在单个 24GB GPU 上微调 65B 模型
- **DoRA**：Weight-Decomposed LoRA，将权重分解为幅度和方向
- **LoRA+**：为 A 和 B 使用不同学习率

## 优势

- 显存消耗仅全量微调的 ~20%
- 可保存多个 LoRA adapter，在推理时切换（多任务微调）
- 适配器文件仅几 MB（vs 全量权重数百 GB）
- 不影响原始模型，可随时回退

## 局限

- 效果不如全量微调（差距通常 <5%）
- 对某些任务 rank 选择较敏感
- 多 LoRA adapter 推理时需额外管理

## 相关概念

- [[fine-tuning]] — LoRA 的父范畴
- [[large-language-model]]
- [[qlora]]
