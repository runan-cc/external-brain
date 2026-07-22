---
title: AI 视频制作工作流
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [video-production, workflow, creative, tutorial]
sources: []
confidence: high
---

# AI 视频制作工作流

## 定义

AI 视频制作工作流是将多个 AI 工具（图像生成、视频生成、配音、剪辑）串联起来，**从创意到成品**的完整生产流水线。不需要摄像机、演员、场景——只需要文字和方向。

## 完整流水线

```
1. 创意 → 2. 脚本 → 3. 分镜 → 4. 图像生成 → 5. 视频生成 → 6. 剪辑 → 7. 声音 → 8. 输出
```

### 每个阶段需要的工具

| 阶段 | 做什么 | 工具 |
|------|--------|------|
| 1. 创意/选题 | 确定主题和方向 | [[chatgpt]], [[claude]] 头脑风暴 |
| 2. 脚本写作 | 写台词、画外音 | [[claude]], [[deepseek]] |
| 3. 分镜设计 | 把脚本拆成镜头 | [[midjourney]], [[stable-diffusion-practice]] |
| 4. 风格设定 | 确定视觉风格和角色 | [[stable-diffusion-practice]] + IP-Adapter |
| 5. 关键帧生成 | 每个镜头的关键帧 | [[comfyui]] + ControlNet |
| 6. 图生视频 | 关键帧→动态视频 | Runway Gen-3, [[kling]], AnimateDiff |
| 7. 帧插值 | 提高帧率/流畅度 | RIFE, FILM, Topaz |
| 8. 超分辨率 | 提升分辨率 | Topaz Video AI, Real-ESRGAN |
| 9. 剪辑合成 | 拼接镜头、转场 | Premiere Pro, DaVinci Resolve, CapCut |
| 10. 配音 | 画外音、对话 | ElevenLabs, GPT-SoVITS |
| 11. 配乐 | 背景音乐 | Suno, Udio |
| 12. 最终输出 | 导出、编码 | FFmpeg, DaVinci |

## AI 视频制作的三种模式

### 模式一：纯文生视频

最简单——输入文字，输出视频。

```
Prompt → Kling / Sora / Runway → 视频
```

✅ 快速出片 ❌ 不可控、一致性差

适合：抽象创意、背景、氛围视频

### 模式二：图生视频（推荐）

**先用 AI 生图确保画面质量 → 再让视频模型动起来。**

```
Prompt → SD 生成关键帧 → ControlNet 控制构图
    ↓
关键帧 → Runway / Kling / AnimateDiff → 动态视频
    ↓
帧插值 → 超分 → 剪辑 → 配音 → 输出
```

✅ 可控、质量高 ✅ 可以一帧一帧打磨

适合：故事型、宣传片、MV

### 模式三：视频到视频

已有视频 → AI 改变风格/替换元素。

```
实拍/已有视频 → ControlNet 提取结构 → SD + Prompt → 新风格视频
```

适合：风格化处理、老视频修复

## 实战工作流详解

### Step 1: 脚本创作

```
你是一个短视频编导，请为主题"一只机器人猫在赛博朋克城市找家"写一个60秒的视频脚本，
包含分镜说明和画外音。
```

输出：7-8 个镜头，每个包含画面描述 + 画外音。

### Step 2: 分镜设计 (ComfyUI)

镜头 1："雨中的赛博朋克城市街景，霓虹灯" → SD 生成。同时用 IP-Adapter 绑定机器猫的外观。

### Step 3: 视频生成

| 方案 | 工具 | 适合 |
|------|------|------|
| 本地免费 | AnimateDiff + ComfyUI | 有显卡 |
| 在线高质量 | Runway Gen-3, Kling | 追求质量 |
| 手机端 | 可灵/Kling App, 即梦 | 快速尝试 |

### Step 4: 后期

```
DaVinci Resolve (免费专业剪辑)
├── 拼接镜头
├── 添加转场
├── 调色
├── 导入配音（ElevenLabs）
├── 导入配乐（Suno）
└── 导出 MP4 (H.265, 4K)
```

## 角色一致性方案

这是 AI 视频最大的痛点——同一个角色在不同镜头中长得不一样。

| 方案 | 说明 |
|------|------|
| **IP-Adapter FaceID** | 提取面部特征 → 每张图都用 |
| **固定种子 + 固定 Prompt** | 同一个种子和 prompt 出图风格一致 |
| **DreamBooth / LoRA 训练** | 用 10-20 张同人照片训练专属模型 |
| **InstantID** | 1 张参考图 → 高质量面部迁移 |
| **Midjourney --cref** | 角色参考功能（付费） |

## 成本估算

| 模式 | 工具 | 1 分钟视频成本 |
|------|------|---------------|
| 全本地 | ComfyUI + AnimateDiff | 电费 (~$1-5) |
| 在线服务 | Runway ($15/月) + ElevenLabs ($5/月) | ~$20/月 |
| 全在线 | Kling (中国平台) | ~¥50-200/月 |

## 推荐学习路径

```
Week 1: 学会用 SD 文生图 + 理解 Prompt
Week 2: 学会 ControlNet + IP-Adapter
Week 3: 学会 ComfyUI 工作流
Week 4: 学会图生视频 (AnimateDiff/Kling)
Week 5: 串联完整流水线，做一个 60 秒视频
```

## 关系

- [[stable-diffusion-practice]]
- [[ai-video-generation]]
- [[comfyui]]
- [[diffusion-models]]
- [[video-encoding]]
