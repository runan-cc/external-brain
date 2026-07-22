---
title: 多模态模型
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [multimodal, vision-language, llm, clip]
sources: []
confidence: high
---

# 多模态模型 (Multimodal Models)

## 定义

多模态模型能**理解并关联多种数据类型**——文本、图像、音频、视频、代码等。人类是多模态的（看到红色圆球 → "这是一个红色的球"），AI 正变得如此。

## 从单模态到多模态

| 阶段 | 模型 | 能处理 |
|------|------|--------|
| 单模态 | GPT-3 | 文本 |
| 单模态 | ResNet | 图像 |
| 跨模态 | CLIP | 文本 + 图像对齐 |
| 多模态理解 | GPT-4V/4o, Gemini | 看 + 读 + 听 + 说 |
| 多模态生成 | DALL-E 3, Sora | 文→图，文→视频 |

## CLIP (Contrastive Language-Image Pre-training)

OpenAI 2021 — 多模态的转折点：

```
Text: "a dog playing in the park"
  ↓ Text Encoder
 Text Embedding
                ↕  对比学习：匹配的对靠近，不匹配的远离
 Image Embedding
  ↑ Image Encoder
Image: 🐕🌳
```

- 用 4 亿图文对训练，零样本分类超越监督 ResNet-50
- 下游：DALL-E 2/3、Stable Diffusion、GPT-4V 都用了类似的对比学习

## 现代多模态架构

### 视觉-语言模型 (VLM)

```
图像 → Vision Encoder → Visual Tokens
                           ↓
文本 → Tokenizer → Text + Visual Tokens → LLM → 输出
```

| 模型 | 架构 |
|------|------|
| GPT-4V/4o | 原生多模态（文本+图像+音频 统一处理） |
| Gemini | 原生多模态，从设计开始 |
| LLaVA | CLIP ViT + Vicuna LLM，开源 |
| Qwen-VL | 中文多模态 |
| Claude 3.5 | 视觉理解（图、图表、PDF） |
| Pixtral (Mistral) | 开源 VLM |

### 视频理解

图像每帧 → 视频 = 帧序列 + 时序信息。

| 模型 | 能力 |
|------|------|
| Gemini 1.5 Pro | 100 万 token 上下文 → 看整部电影 |
| Video-LLaMA | 视频 + 音频理解 |
| Sora (OpenAI) | 文→视频生成（世界模拟器） |

### 音频/语音

| 模型 | 能力 |
|------|------|
| Whisper (OpenAI) | 99 语言语音识别 |
| GPT-4o 语音模式 | 端到端语音对话 |
| ElevenLabs | 高质量 TTS |
| Suno, Udio | 文→音乐生成 |

## 关键技术

| 技术 | 说明 |
|------|------|
| Contrastive Learning | CLIP 式图文对齐 |
| Visual Tokenization | 图像切块 + 线性投影 → LLM 可读的 tokens |
| Cross-Attention | 文本和图像特征互相 attend |
| Q-Former (BLIP-2) | 小模型把图像特征投影到 LLM 空间 |
| Early Fusion | 在 token 层面混合（GPT-4o 风格）|

## 挑战

| 挑战 | 说明 |
|------|------|
| 数据对齐 | 图文对质量决定模型上限 |
| 计算成本 | 训练多模态模型极贵 |
| 跨模态幻觉 | 图像和文本描述不对应 |
| 时序理解 | 视频中理解因果关系 |

## 关系

- [[large-language-model]]
- [[transformer-architecture]]
- [[diffusion-models]]
