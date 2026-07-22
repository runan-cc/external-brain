---
title: AI 视频生成
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [video-generation, generative-ai, sora, diffusion]
sources: []
confidence: high
---

# AI 视频生成

## 定义

AI 视频生成是使用深度学习模型**从文本、图像或其他视频自动生成视频内容**的技术。这是继文生图之后 AI 生成领域最重要的发展方向，2024 年 OpenAI Sora 的发布标志着里程碑突破。

## 核心技术

### 扩散模型基础

所有主流视频生成模型都基于 [[diffusion-models]]，但视频增加了**时序维度**的挑战：

| 维度 | 图像 | 视频 |
|------|------|------|
| 形状 | [H, W, C] | [T, H, W, C] |
| 数据量 | 一张图 ~MB | 一个视频 ~GB |
| 一致性 | 不需要 | 帧间必须连贯 |
| 物理合理 | 不需要 | 对象不能消失/突变 |

### 视频扩散架构

```
文本 Prompt
    ↓ Text Encoder
文本 Embedding
    ↓
噪声 (T×H×W×C) → UNet/DiT → 逐帧去噪 → 视频输出
                   ↑
              时间注意力层
              (关键！保证帧间一致性)
```

### 关键技术

| 技术 | 说明 |
|------|------|
| **时空 Attention** | Attention 在空间和时间维度同时计算，保证帧间连贯性 |
| **3D UNet / DiT** | 2D 卷积 → 3D 卷积，处理时空信息 |
| **Causal / Masked Attention** | 只关注过去帧，保证因果性（生成类） |
| **帧插值** | 先生成关键帧，再插值中间帧 |
| **超分辨率级联** | 低分辨率生成 → 高分辨率渲染 |
| **Temporal Consistency Loss** | 训练时惩罚帧间不一致 |

## 主要模型

### OpenAI Sora (2024, 2024.12 公测)

**里程碑模型**——真正意义上的"世界模拟器"初现。

| 特性 | 说明 |
|------|------|
| 基础架构 | Diffusion Transformer (DiT)，是 Transformer 而非 UNet |
| 最大时长 | 1 分钟（远超市面上其他模型） |
| 分辨率 | 1080p |
| 核心突破 | 将视频编码为 spacetime patches（视频的"token"），类似 GPT 的文本 token |
| 理解力 | 能理解物理因果关系、遮挡关系、物体持久性 |

**Spacetime Patches 原理**：
```
视频 → 压缩到 latent space → 切成 3D patches (×时间+空间)
      → 这些 patches 就是 Transformer 的 tokens
      → 类似 GPT 预测下一个 token，预测下一帧的 patches
```

### Runway Gen-3 Alpha (2024)

| 特性 | 说明 |
|------|------|
| 模式 | 文生视频、图生视频 |
| 时长 | 10 秒 |
| 一致性 | 极佳的角色和场景保持 |
| 控制 | 摄像机运动控制、风格迁移 |
| 定位 | 专业视频创作者工具 |

### Kling (Kuaishou, 2024)

| 特性 | 说明 |
|------|------|
| 模式 | 文生视频、图生视频 |
| 时长 | 最长 2 分钟 |
| 分辨率 | 1080p |
| 特色 | 3D 时空联合注意力，物理模拟好 |
| 可用 | 中国用户可直接使用 |

### Pika 2.0 (2024)

| 特性 | 说明 |
|------|------|
| 模式 | 文生视频、图生视频、视频编辑 |
| 特色 | 场景成分控制（替换角色/物体） |
| 定位 | 易用、社交媒体场景 |

### 其他重要模型

| 模型 | 特点 |
|------|------|
| Stable Video Diffusion (Stability AI) | 开源、图生视频 |
| Emu Video (Meta) | 两步法：先生成图像再生成视频 |
| VideoPoet (Google) | 自回归 + 扩散混合 |
| Lumiere (Google) | Space-Time UNet，一次性生成全视频 |
| Vidu (Shengshu, 中国) | 对标 Sora，支持中国特色场景 |
| CogVideoX (Zhipu) | 开源中文视频生成 |

## 训练数据

| 来源 | 特点 |
|------|------|
| YouTube/视频网站 | 海量视频，有对应标题/描述 |
| 电影/电视剧 | 高质量但版权风险 |
| 合成数据 | 用游戏引擎生成（Unreal/Unity） |
| 3D 渲染 | 物理准确的训练数据 |

## 核心挑战

| 挑战 | 现状 |
|------|------|
| 时序一致性 | 改善中，长视频仍有物体突变 |
| 物理合理性 | 物体穿透、违反重力等问题仍存在 |
| 计算成本 | 训练需数千 GPU，推理也昂贵 |
| 可控性 | 精确控制运动轨迹/角色动作差距大 |
| 评估指标 | FVD (Fréchet Video Distance) 但不够全面 |

## AI 视频编辑

| 功能 | 说明 | 代表 |
|------|------|------|
| 局部重绘 (Inpainting) | 移除/替换视频中的物体 | Runway, Pika |
| 风格迁移 | 视频变成动漫/油画风格 | EbSynth, Runway |
| 帧插值 | 提高帧率 (24→60fps) | RIFE, DAIN |
| 超分辨率 | 480p→1080p→4K | Topaz Video AI |
| 唇形同步 | 让口型匹配新语音 | Wav2Lip, SadTalker |

## 应用场景

| 场景 | 说明 |
|------|------|
| 短视频制作 | 文生视频替代拍摄 |
| 广告创意 | 快速生成多版创意素材 |
| 游戏过场动画 | 比手工制作便宜 |
| 电影预览 (Pre-vis) | 低成本概念验证 |
| 教育动画 | 解释抽象概念的可视化 |
| 数据增强 | 为视频理解模型生成训练数据 |

## 关系

- [[diffusion-models]]
- [[transformer-architecture]]
- [[large-language-model]] — 视频生成的文本理解依赖 LLM
- [[multimodal-models]] — 视频在向多模态融合
