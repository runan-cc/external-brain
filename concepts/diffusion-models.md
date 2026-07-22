---
title: Diffusion Models
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [model, architecture, image-generation]
sources: []
confidence: high
---

# Diffusion Models（扩散模型）

## 定义

扩散模型是一类**生成模型**，通过逐步添加噪声（前向过程），再学习逆向去噪（反向过程）来生成数据。是 Stable Diffusion、DALL-E、Midjourney 等图像生成模型的底层架构。

## 工作原理

```
Forward Process（前向扩散）:
真实图像 x₀ → 加噪 → x₁ 加噪 → ... → 纯噪声 xₓ

Reverse Process（逆向去噪）:
纯噪声 xₓ → UNet 去噪 → ... → x₁ → x₀（生成图像）
```

模型学习的是**预测每一步添加的噪声**，然后减去它。

## 关键组件

- **UNet**：核心去噪网络，带有跳跃连接的编码-解码架构
- **Noise Schedule**：控制噪声添加速率
- **Text Conditioning**：通过 CLIP 等文本编码器注入文字提示
- **DDPM / DDIM**：不同的采样方法（DDIM 快但可能质量略低）

## 主流模型

| 模型 | 开发者 | 特点 |
|------|--------|------|
| Stable Diffusion | Stability AI | 开源，社区生态丰富 |
| DALL-E 3 | [[openai]] | 文本理解强，与 ChatGPT 集成 |
| Midjourney | Midjourney | 美学质量领先 |
| FLUX | Black Forest Labs | 最新开源 SOTA |

## 关键进展

- **Latent Diffusion**：在压缩的 latent space 而不是像素空间扩散，大幅降低计算
- **ControlNet**：精确控制生成图像的结构（姿势、深度图、线稿）
- **IP-Adapter**：用参考图像控制生成风格
- **Video Diffusion**：Sora、Runway 等扩展到视频生成

## 局限

- 采样慢（多步去噪）
- 细节一致性难以保证（手指、文字）
- 版权和深度伪造伦理问题

## 相关概念

- [[stable-diffusion]]
- [[openai]] — DALL-E 和 Sora
- [[gan-generative-adversarial-network]] — 传统生成模型对比
