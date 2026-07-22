---
title: Attention Mechanisms
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [attention, transformer, optimization, gpu]
sources: []
confidence: high
---

# Attention 机制深入

## 核心公式回顾

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

标准 [[transformer-architecture]] 的 Attention 复杂度：O(n²)，n = 序列长度。这是 L → L 模型的瓶颈。

## Attention 变体

| 变体 | 复杂度 | 核心思想 |
|------|--------|----------|
| Standard | O(n²) | 每个 token 关注所有 token |
| Multi-Head (MHA) | O(n²·h) | 多个注意力头并行 |
| Multi-Query (MQA) | O(n²) | 所有头共享 K、V，省 KV cache |
| Grouped-Query (GQA) | O(n²) | 分组共享 K、V（MHA 和 MQA 的折中） |
| **FlashAttention** | O(n²) | 用 GPU SRAM 做分块，**IO 感知** |
| FlashAttention-2 | O(n²) | 更好的并行度 |
| FlashAttention-3 | O(n²) | Hopper 架构优化 |
| Sparse Attention | O(n log n) | 只关注一部分 token |
| Sliding Window | O(n·w) | 固定窗口大小 w |

## FlashAttention 核心

不是数学上的改进，而是**工程优化**——用 GPU 内存层次减少 HBM 读写。

```
标准 Attention：
QK^T → 写 HBM → softmax → 写 HBM → ×V → 写 HBM
        ↑ 每次 O(n²) 矩阵落盘，带宽瓶颈

FlashAttention：
Q,K,V 分块 → 每次一个小块在 SRAM 中完成全部计算
              → 只写最终结果到 HBM
```

快了 2-4 倍，内存使用 O(n) 而不是 O(n²)。

## MHA vs MQA vs GQA

| 维度 | MHA | MQA | GQA |
|------|-----|-----|-----|
| Q 头数 | h | h | h |
| K,V 头数 | h | 1 | g (1<g<h) |
| KV Cache | 大 | 小 (1/h) | 中 |
| 精度损失 | 无 | 轻微 | 极小 |
| 使用 | GPT-3 | PaLM | **Llama 2/3**, Mistral |

GQA 是 2024 后 LLM 的主流选择——KV cache 小、质量几乎无损。

## KV Cache

推理时不重新计算过去的 K、V，而是**缓存**它们——自回归每生成一个 token 只需追加计算，不需重算历史。

```
生成 token 1: compute K₁,V₁ → 缓存
生成 token 2: compute K₂,V₂ → 缓存，Q₂ attn over [K₁,K₂]
生成 token 3: compute K₃,V₃ → 缓存，Q₃ attn over [K₁,K₂,K₃]
...
```

KV cache 是推理的**主要内存消耗**：
- Llama 2 70B × 4096 tokens × FP16 → ~1.1 GB KV cache
- 长上下文（128K）→ ~35 GB

## 推测解码 (Speculative Decoding)

用**小模型快速生成候选**，大模型**并行验证**——不牺牲质量，1.5-3x 加速。

```
小模型（Draft）: 生成 A, B, C, D (4 个候选 token，超快)
大模型（Verify）: 一次 forward 验证 A,B,C,D
  → A ✓, B ✓, C ✗, D ✗
  → 接受 A,B，拒绝 C,D
  → 大模型生成 C' → 循环
```

## 关系

- [[transformer-architecture]]
- [[large-language-model]]
- [[gpu]] — FlashAttention 依赖 GPU 内存架构
