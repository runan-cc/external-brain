---
title: VAE (Variational Autoencoder)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [generative-model, vae, deep-learning]
sources: []
confidence: high
---

# VAE (变分自编码器)

## 定义

VAE 是 Kingma & Welling 于 2013 年提出的**生成模型**——Autoencoder + 概率论。它不仅编码数据，还学习数据的**概率分布**，从而可以采样生成新样本。

## 架构

```
输入 x
  ↓
Encoder → μ(x), σ²(x)  (均值、方差)
  ↓
Sample z ~ N(μ, σ²)     (重参数化技巧)
  ↓
Decoder → 重建 x̂
```

**关键**：Encoder 不输出一个定值，而是**输出一个分布**——"这个图片可能在哪"。

## 损失函数

$$L = \underbrace{\mathbb{E}_{q(z|x)}[\log p(x|z)]}_{\text{重建损失}} - \underbrace{D_{KL}(q(z|x) \| p(z))}_{\text{KL 散度正则}}$$

| 项 | 含义 |
|-----|------|
| 重建损失 | x̂ 像不像原始 x |
| KL 散度 | 后遍分布有多接近标准正态分布 |

KL 项约束 latent space 连续且光滑——这是 VAE 能生成新样本的原因。

## 重参数化技巧 (Reparameterization Trick)

```python
# 坏：z 是随机的，梯度不能流过采样
z = normal(mu, sigma)

# 好：把随机性移到外部
eps = normal(0, 1)
z = mu + sigma * eps  # 梯度可以流过 mu 和 sigma
```

## VAE vs AE vs GAN vs Diffusion

| 模型 | 生成能力 | Latent Space | 输出质量 |
|------|----------|-------------|----------|
| AE | ❌ 只能重建 | 分散的 | — |
| VAE | ✅ 可采样 | 连续、光滑 | 模糊 |
| [[gan]] | ✅ 可采样 | 单一噪声 | 清晰 |
| [[diffusion-models]] | ✅ 可采样 | 多步去噪 | SOTA 清晰度 |

## 变体

| 变体 | 改进 |
|------|------|
| β-VAE | 加大 KL 权重 → 更好的解挤 (disentanglement) |
| VQ-VAE | 离散化 latent code（DALL-E 1, Stable Diffusion 的基础） |
| Conditional VAE | 条件生成（给定标签生成样本） |

## 应用

| 应用 | 场景 |
|------|------|
| 图像生成 | 人脸、字体 |
| 异常检测 | 重建误差大 = 异常 |
| 数据压缩 | 学到的 latent 表示 |
| 分子设计 | 化学空间采样 |

## 关系

- [[gan]]
- [[diffusion-models]]
- [[information-theory]] — KL 散度
- [[gradient-descent]]
