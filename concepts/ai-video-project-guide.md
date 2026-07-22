---
title: AI Video Project Guide
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [guide, project, workflow, creative, how-to]
sources: []
confidence: high
---

# AI 视频项目指南

## 这个项目怎么帮你做 AI 视频

`external-brain` 知识库里的以下页面构成了完整的 AI 视频制作知识体系。按这个顺序看：

### 🎯 理解底层原理（先看这些）
1. [[diffusion-models]] — 扩散模型是所有图像/视频生成的数学基础
2. [[transformer-architecture]] — DiT (Sora 架构) 的基础
3. [[attention-mechanisms]] — 时空 Attention 保证视频帧间一致性
4. [[video-encoding]] — 理解视频格式，成品才能分发

### 🎨 掌握图像生成（再看这些）
5. [[stable-diffusion-practice]] — SD 实际使用方法、Prompt 技巧、ControlNet
6. [[comfyui]] — 节点化工作流工具，AI 视频的"操作台"
7. [[lora]] — 训练专属角色/风格的微调技术
8. [[gan]] / [[vae]] — 生成模型基础

### 🎬 学习视频生成（核心）
9. [[ai-video-generation]] — 主流视频生成模型总览 (Sora/Kling/Runway)
10. [[ai-video-workflow]] — 完整制作流程：从创意到成品

### 🔊 掌握配音
11. [[tts-ai-voice]] — TTS 工具、AI 配音、配乐

### 📐 补充基础
12. [[multimodal-models]] — 多模态理解（CLIP 等）
13. [[quantization]] — 大模型本地部署必备
14. [[gradient-descent]] — 训练优化基础
15. [[linear-algebra]] — 理解扩散过程的数学

## 快速启动：做一个 AI 视频

### 如果你有高性能 GPU (RTX 4090/3090)

```
1. 安装 ComfyUI
   git clone https://github.com/comfyanonymous/ComfyUI
   
2. 下载模型
   - SDXL 或 FLUX checkpoint
   - AnimateDiff 模块
   - IP-Adapter + FaceID
   - ControlNet
   
3. 学习工作流
   → CivitAI 搜 "ComfyUI workflow" 下载现成的
   → 在 ComfyUI 里加载 → 改参数 → 出视频
   
4. 完整流水线
   SD 出图 → AnimateDiff 动起来 → Topaz 超分 → 配音 → 剪辑
```

### 如果你没有高性能 GPU

```
1. 图像生成
   - Midjourney (付费)
   - Kling/可灵 (中国，文生图 + 图生视频一站式)
   - Stable Diffusion 在线 (Replicate, RunDiffusion)

2. 视频生成
   - Runway Gen-3 ($15/月起)
   - Kling/可灵 (免费试用额度)
   - Pika (免费起步)

3. 配音
   - ElevenLabs (免费额度)
   - GPT-SoVITS (本地免费，约 6GB VRAM)

4. 剪辑
   - DaVinci Resolve (免费，功能全)
   - CapCut 剪映 (简单，有 AI 功能)

5. 配乐
   - Suno / Udio
```

## 推荐工具组合

| 预算 | 图像 | 视频 | 配音 | 剪辑 |
|------|------|------|------|------|
| 零成本 | ComfyUI本地 + SD | AnimateDiff (本地) | GPT-SoVITS (本地) | DaVinci |
| 低成本 | Kling/可灵 | Kling/可灵 | Fish Audio | CapCut |
| 中等 | Midjourney + ComfyUI | Runway + Kling | ElevenLabs | DaVinci |
| 专业 | FLUX + SD3 + 角色 LoRA | Runway + Sora | ElevenLabs + Suno | DaVinci |

## 学习资源

- **ComfyUI 入门**：YouTube "ComfyUI 从入门到精通"系列
- **AI 视频实战**：B站 "AI 影视飓风"、"AI 视频研究所"
- **工作流分享**：CivitAI、OpenArt 搜 ComfyUI workflow
- **Prompt 参考**：Lexica、PromptHero
- **角色一致**：IP-Adapter + FaceID 教程

## 关系

- [[ai-video-generation]]
- [[ai-video-workflow]]
- [[stable-diffusion-practice]]
- [[comfyui]]
- [[tts-ai-voice]]
