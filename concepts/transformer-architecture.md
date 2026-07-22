---
title: Transformer Architecture
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [architecture, model, attention, training]
sources: []
confidence: high
---

# Transformer Architecture

## 定义

Transformer 是 2017 年由 Vaswani et al. 在论文 "Attention Is All You Need" 中提出的神经网络架构。它完全基于 **自注意力机制（Self-Attention）**，摒弃了 RNN 的循环结构，实现了高度并行化的训练。

## 核心组件

### Self-Attention（自注意力）

$$
\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

每个 token 会"关注"序列中的所有 token，计算加权表示。这是 Transformer 能捕捉长距离依赖的关键。

### Multi-Head Attention（多头注意力）

将注意力拆分为多个"头"，每个头在不同的表示子空间中学习不同的关注模式。

### Positional Encoding（位置编码）

由于没有循环结构，Transformer 通过位置编码注入序列顺序信息。
- 原始：正弦/余弦函数
- 现代变体：RoPE (Rotary Position Embedding)、ALiBi

### Feed-Forward Network (FFN)

每个 attention 层后接全连接网络：
$$
\text{FFN}(x) = \text{GeLU}(xW_1 + b_1)W_2 + b_2
$$

现代变体：SwiGLU、Gated FFN

## 架构变体

| 类型 | 代表模型 | 特点 |
|------|----------|------|
| Decoder-only | GPT-4, Claude, DeepSeek, Llama | 自回归生成 |
| Encoder-decoder | T5, BART | 翻译/摘要任务 |
| Encoder-only | BERT, RoBERTa | 理解任务 |

## 关键优化

| 优化 | 说明 |
|------|------|
| FlashAttention | IO-aware 注意力计算，大幅降低显存和延迟 |
| KV Cache | 推理时缓存 Key/Value，避免重复计算 |
| GQA / MQA | Grouped Query Attention, Multi Query Attention — 减少 KV head 数量 |
| Mixture of Experts (MoE) | 稀疏激活，增大参数量的同时控制计算量 |

## 相关概念

- [[large-language-model]] — 基于 Transformer 的大语言模型
- [[chain-of-thought]] — 利用 Transformer 的推理能力
- [[fine-tuning]] — 在预训练 Transformer 上微调
