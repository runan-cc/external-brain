---
title: ComfyUI
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [tool, image-generation, video-generation, visual-workflow]
sources: []
confidence: high
---

# ComfyUI

## 概览

ComfyUI 是基于**节点图 (Node Graph)** 的 Stable Diffusion 工作流工具，2023 年发布后迅速成为 AI 图像/视频生成社区的标准工具。区别于 WebUI (A1111) 的固定表单，ComfyUI 让你**像搭电路图一样搭建生成流水线**。

## 核心理念

```
文本 Prompt → CLIP Encoder → Positive/Negative Embeddings
                                      ↓
     Latent Image (噪声) ──────────→ KSampler
                                      ↓
                               VAE Decoder → 最终图片
```

每个步骤是一个**节点**，拖线连接就是整个 pipeline。

## 为什么用 ComfyUI

| 优势 | 说明 |
|------|------|
| 可视化工作流 | 精确控制每一步，不像 WebUI 的黑盒 |
| 可复用 | 保存工作流 JSON，分享/复现零成本 |
| 内存优化 | 按需加载/卸载模型，低 VRAM 也能跑 |
| 差分重跑 | 改一个节点只重跑下游，不用重头开始 |
| 队列系统 | 支持批量和 API 调用 |
| 模块化 | 社区上千个自定义节点 |

## 核心节点类型

| 类别 | 节点 | 功能 |
|------|------|------|
| Load | Load Checkpoint, Load LoRA, Load VAE | 加载模型 |
| Encode | CLIP Text Encode, VAE Encode | 文本/图像 → embedding |
| Sample | KSampler, KSampler Advanced | 去噪采样（核心） |
| Decode | VAE Decode | latent → 图片 |
| Control | ControlNet, IP-Adapter | 控制生成（姿态/边缘/面部） |
| Upscale | Upscale Image, Ultimate SD Upscale | 超分辨率 |
| Video | AnimateDiff, SVD, Video Combine | 视频生成 |

## 典型工作流

### 基础文生图

```
Checkpoint → CLIP → Text Encode → KSampler → VAE Decode → Save
```

### ControlNet 精确控制

```
参考图 → ControlNet (Canny/OpenPose/Depth) → ┐
                                               ├→ KSampler → ...
文本 Prompt ──────────────────────────────────┘
```

### LoRA 角色生成

```
Checkpoint → Load LoRA → CLIP → KSampler → ...
```

### AnimateDiff 视频

```
Prompt → CLIP → AnimateDiff Loader → KSampler → AnimateDiff → Video Combine
```

## ComfyUI vs A1111 (Stable Diffusion WebUI)

| 维度 | ComfyUI | A1111 WebUI |
|------|---------|-------------|
| 上手难度 | 陡峭 | 平缓 |
| 高级控制 | ✅ 极强 | 有限 |
| 工作流复用 | ✅ JSON | ❌ 需重新配置 |
| 内存效率 | ✅ 更高 | 较低 |
| 生态 | 快速增长 | ✅ 成熟 |
| 适合 | 高级用户、批量生产 | 入门、快速出图 |

## 视频生成工作流

ComfyUI 是 AI 视频生成社区的主力工具：

| 流程 | 组件 |
|------|------|
| 文生视频 | SVD (Stable Video Diffusion), AnimateDiff |
| 图生视频 | IP-Adapter + AnimateDiff |
| 视频到视频 | ControlNet + Video Input |
| 帧插值 | FILM, RIFE 节点 |
| 人脸视频 | FaceSwap + AnimateDiff |

## 关键生态

| 工具 | 用途 |
|------|------|
| ComfyUI Manager | 节点管理、安装更新 |
| CivitAI | 社区模型和 ComfyUI 工作流分享 |
| ComfyUI-Custom-Scripts | 增强功能（批量、自动队列等） |
| WAS Node Suite | 万能节点集 |
| Impact Pack | 面部修复、检测等 |
| ComfyUI-InstantID | 面部一致性生成 |

## 工作流即代码

ComfyUI 工作流是 JSON 文件 → Git 管理、分享、复现：

```json
{
  "nodes": [
    {"id": 1, "type": "CLIPTextEncode", "inputs": {"text": "a cat"}},
    {"id": 2, "type": "KSampler", "inputs": {"positive": [1, 0]}}
  ]
}
```

## 关系

- [[diffusion-models]]
- [[ai-video-generation]]
- [[stable-diffusion]]
