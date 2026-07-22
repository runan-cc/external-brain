---
title: Stable Diffusion 实战
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [stable-diffusion, image-generation, hands-on, workflow]
sources: []
confidence: high
---

# Stable Diffusion 实战

## 定义

Stable Diffusion 是目前最主流的**开源文生图模型**，由 Stability AI 开发。基于 [[diffusion-models|Latent Diffusion]]，将扩散过程从像素空间移至压缩的 latent space，大幅降低计算需求。是所有 AI 图像/视频生成工作流的基石。

## 核心组件

```
┌─ Checkpoint (大模型) ────────────────┐
│  SD 1.5 / SDXL / SD3 / FLUX         │
├─ VAE ────────────────────────────────┤
│  编解码 (pixel ↔ latent)             │
├─ CLIP / T5 ──────────────────────────┤
│  文本理解                            │
├─ LoRA ───────────────────────────────┤
│  微调适配器（角色/风格/姿势）          │
├─ ControlNet ─────────────────────────┤
│  精确控制（姿态/边缘/深度/面部）        │
├─ IP-Adapter ─────────────────────────┤
│  图像提示（用图片控制生成）             │
└─ Upscaler ───────────────────────────┘
│  超分辨率放大                          │
```

## 模型家族

| 模型 | 发布时间 | 分辨率 | 特点 |
|------|----------|--------|------|
| SD 1.5 | 2022.10 | 512×512 | 生态最丰富、LoRA 最多 |
| SDXL 1.0 | 2023.07 | 1024×1024 | 构圖更好、理解力更强 |
| SDXL Turbo | 2023.11 | 1024×1024 | 1-4 步出图（蒸馏） |
| SD3 (MMDiT) | 2024.06 | 多种 | Transformer 架构，文本理解质的飞跃 |
| FLUX.1 (Black Forest Labs) | 2024.08 | 多种 | 原 SD 团队新作，质量达 Midjourney 级 |
| FLUX.1 schnell | 2024.08 | 多种 | 蒸馏版，1-4 步出图 |

## Prompt 工程

### 结构
```
主体描述 + 环境/场景 + 艺术风格 + 质量词 + 技术参数
```

### 示例

**基础：**
```
a girl reading a book, sitting by the window, soft lighting
```

**优化后：**
```
1girl, solo, reading book, sitting, window seat, sunlight streaming through window, dappled light, book in hands, focused expression, 
(masterpiece, best quality:1.2), (8k, ultra high res:1.1), 
depth of field, bokeh, cinematic lighting, ray tracing,
soft focus, film grain, analog photo, kodak portra 400
```

**Negative Prompt:**
```
(worst quality, low quality:1.4), blurry, ugly, deformed, bad anatomy,
extra fingers, missing fingers, bad hands, watermark, signature,
text, jpeg artifacts, lowres
```

### XYZ Plot 测试法

在 ComfyUI/A1111 中同时测试多个参数：
- X 轴：采样器（Euler a, DPM++ 2M, DPM++ SDE...）
- Y 轴：步数 (20, 30, 40, 50)
- Z 轴：CFG Scale (5, 7, 9, 11)

→ 一张网格图展示所有组合，一眼找到最优。

## CFG (Classifier-Free Guidance)

`CFG Scale = 多少比例遵循你的 prompt` 

| CFG | 效果 |
|-----|------|
| 1-3 | 松散、创意自由 |
| 5-7 | 平衡（推荐） |
| 8-12 | 严格遵循 prompt |
| 15+ | 过度曝光/怪异 |

## 采样器选择

| 采样器 | 速度 | 收敛 | 特点 |
|--------|------|------|------|
| Euler a | 中 | 不收敛 | 最常用，细节丰富 |
| DPM++ 2M Karras | 快 | 收敛 | 质量好，步骤敏感 |
| DPM++ SDE Karras | 慢 | 收敛 | 最优质量，需多步 |
| UniPC | 极快 | 收敛 | 5-10 步就能有质量 |
| LCM | 1-8 步 | 收敛 | 实时生成（需 LCM LoRA） |

## ControlNet

### 常用 ControlNet

| ControlNet | 输入 | 控制什么 |
|-----------|------|----------|
| Canny | 边缘检测图 | 物体轮廓 |
| OpenPose | 骨骼姿态 | 人物动作 |
| Depth (Midas) | 深度图 | 空间关系 |
| SoftEdge | 柔化边缘 | 构图（比 Canny 更灵活） |
| Tile | 图块 | 超分 + 局部重绘 |
| Lineart | 线稿 | 线稿上色 |
| IP-Adapter | 参考图 | 风格/面部迁移 |
| Reference Only | 参考图 | 构图 + 风格 |

### 实战：角色一致性

```
1. 用 IP-AdapterFaceID 提取面部特征
2. 绑定到 Prompt → 所有生成的图片都是同一个人
3. → 这些图送入视频生成模型 → 角色一致的视频
```

## 从图像到视频的流水线

```
文生图 (Txt2Img)
  ↓
ControlNet 控制构图
  ↓
IP-Adapter 保证一致性
  ↓
图生视频 (Img2Video: SVD / AnimateDiff / Kling)
  ↓
帧插值 (RIFE / FILM)  → 提高帧率
  ↓
Topaz / Real-ESRGAN   → 超分辨率
  ↓
视频编码 (H.264/H.265) → 输出
```

## 推荐配置 (本地)

| 组件 | 最低 | 推荐 | 理想 |
|------|------|------|------|
| VRAM | 6 GB | 12 GB | 24 GB |
| RAM | 16 GB | 32 GB | 64 GB |
| 存储 (模型) | 50 GB | 200 GB | 1 TB |
| GPU | RTX 3060 | RTX 4070 Ti | RTX 4090 |

## 关系

- [[diffusion-models]]
- [[comfyui]] — 实际使用工具
- [[lora]] — 关键微调技术
- [[ai-video-generation]]
