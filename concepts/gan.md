---
title: GAN (Generative Adversarial Network)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [generative-model, gan, image-generation, deep-learning]
sources: []
confidence: high
---

# GAN (生成对抗网络)

## 定义

GAN 是 Ian Goodfellow 于 2014 年提出的**生成模型架构**——两个神经网络互相对抗训练：**生成器 (Generator)** 创造假样本，**判别器 (Discriminator)** 区分真假。二者在博弈中共同进步。

## 工作原理

```
真实图片 → ┐
           ├──→ Discriminator → Real (1)
           │                        ↕ 对抗训练
噪声 z ──→ Generator → 假图片 ──→ Discriminator → Fake (0)
```

| 角色 | 目标 |
|------|------|
| Generator | 生成骗过判别器的假图片 |
| Discriminator | 区分真实图片和生成图片 |

### 训练公式

$$\min_G \max_D V(D, G) = \mathbb{E}_{x \sim p_{data}}[\log D(x)] + \mathbb{E}_{z \sim p_z}[\log(1 - D(G(z)))]$$

- D 想最大化（区分真伪）
- G 想最小化（骗过 D）

## 重要变体

| 变体 | 改进 | 典型应用 |
|------|------|----------|
| DCGAN | CNN 架构稳定训练 | 奠基现代 GAN 架构 |
| StyleGAN (NVIDIA) | 逐层控制风格 → 高分辨率人脸 | This Person Does Not Exist |
| CycleGAN | 不成对图像的域转换 | 马 ↔ 斑马、照片 ↔ 梵高风格 |
| Pix2Pix | 成对图像的域转换 | 草图 → 照片 |
| BigGAN | 大规模训练 + 条件生成 | 高质量 ImageNet 生成 |
| SRGAN | 超分辨率重建 | 低清 → 高清 |
| GPT-4o images | 自回归代替对抗训练（已大于 GAN 趋势） | 文生图 |

## GAN vs [[diffusion-models]]

| 维度 | GAN | Diffusion |
|------|-----|-----------|
| 训练 | 对抗训练（不稳定） | 去噪（稳定） |
| 采样 | 单次 forward（快） | 多步去噪（慢） |
| 质量 | StyleGAN 极佳 | SOTA (Stable Diffusion 3, FLUX) |
| 多样性 | 模式坍塌 (Mode Collapse) | 多样性更好 |
| 趋势 | 研究中、不如扩散模型主流 | ✅ 2023- 年主流 |

## 模式坍塌 (Mode Collapse)

GAN 训练的经典风险：Generator 发现几个"安全"的输出能骗过 D，就不再探索多样性——生成的都是相似样本。

缓解：Minibatch Discrimination、Wasserstein GAN (WGAN)、Gradient Penalty。

## 应用

| 领域 | 用例 |
|------|------|
| 图像生成 | StyleGAN 生成真人照 |
| 图像编辑 | Inpainting、风格迁移 |
| 超分辨率 | SRGAN、ESRGAN |
| 数据增强 | 给小数据集生成训练样本 |
| 药物发现 | 分子结构生成 |

## 关系

- [[diffusion-models]]
- [[machine-learning]]
- [[gradient-descent]]
