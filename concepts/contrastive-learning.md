---
title: 对比学习 (Contrastive Learning)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [representation-learning, contrastive-learning, self-supervised]
sources: []
confidence: high
---

# 对比学习 (Contrastive Learning)

## 定义

对比学习是**自监督表示学习**的核心范式——通过拉近相似样本、推远不相似样本来学习有意义的特征表示。CLIP、SimCLR、MoCo 都基于这个思想。

## 核心思想

```
正样本对: 同一图片的两种增强 → 拉近 (Pull)
负样本对: 不同图片 → 推远 (Push)

编码后，猫的两种增强距离近
          猫的增强和狗的增强距离远
```

不需要人工标注——"同一张图的两个视角 = 同一个语义"就是免费的监督信号。

## 主要算法

### SimCLR (Google, 2020)

```
图片 x
  ↓ 两个随机增强
x₁ (裁剪+颜色)  → Encoder → z₁ ─┐
x₂ (旋转+模糊)  → Encoder → z₂ ←┤ 对比损失 (InfoNCE)
                                  │
其他图片的增强 → Encoder → z₃...zk (负样本)
```

| 关键 | 说明 |
|------|------|
| 数据增强 | 关键！裁剪+颜色变换最有效 |
| Batch Size | 越大越好（更多负样本，Google 用 4096） |
| MLP 投影头 | 简单的非线性层，训练后用其输出 |

### MoCo (何恺明, 2020)

解决大 batch 的需求——用**队列**存储大量负样本。

```
Query Encoder (当前 batch) → q
Key Encoder (动量更新)      → k₊ (正样本) + k₁...k_K (来自队列)
                                   ↓
                              对比损失
                                   ↓
                              k₊ 入队，旧负样本出队
```

动量更新：`θ_k ← m·θ_k + (1-m)·θ_q`（m≈0.999），Key Encoder 缓慢跟随 Query Encoder。

### CLIP

见[[multimodal-models]]——图文对比学习：匹配的图文对 = 正样本，不匹配的 = 负样本。4 亿图文对训练。

### BYOL (DeepMind, 2020)

**不需要负样本！**——通过动量网络 + MLP 预测器，防止模型崩塌。但理论上为什么有效还在讨论。

## InfoNCE Loss

$$\mathcal{L} = -\log \frac{\exp(sim(z_i, z_j) / \tau)}{\sum_{k=1}^{N} \exp(sim(z_i, z_k) / \tau)}$$

- 分子：正样本对的相似度
- 分母：所有样本对的相似度之和
- τ (温度)：越小越"硬"（对正样本要求更高）

## 应用

| 场景 | 方法 |
|------|------|
| 图像预训练 | SimCLR, MoCo → 下游分类/检测 |
| 图文对齐 | CLIP → DALL-E, Stable Diffusion |
| 推荐系统 | 用户-物品 对比 |
| NLP 句子表示 | SimCSE |
| 图表示学习 | GraphCL |

## 关系

- [[machine-learning]]
- [[multimodal-models]]
- [[embedding]]
