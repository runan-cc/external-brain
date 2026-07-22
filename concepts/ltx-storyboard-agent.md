---
title: LTX 2.3 分镜智能体
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [storyboard, ltx, prompt-engineering, workflow, agent]
sources: ["local skill: ltx23-script-to-video"]
confidence: high
---

# LTX 2.3 分镜智能体

## 定义

LTX 2.3 分镜智能体是一个**从剧本到 LTX 视频剪辑提示词的完整分镜设计系统**。它不是你人工写分镜——而是一个 AI 智能体按 7 个阶段自动拆解剧本、生成角色/场景图提示词、检查参考图一致性、最终输出可直接喂给 ComfyUI 的 LTX Prompt。

## 为什么需要

人工写分镜的痛点是：
- 分镜描述不够精确 → AI 理解偏差
- 角色/场景图不一致 → 视频角色漂移
- 镜头规则缺失 → 生成的视频构图混乱
- Prompt 格式不对 → ComfyUI 效果差

这个智能体解决了所有这些。

## 7 阶段流程

```
阶段一：锁定剧本       → 角色表、Scene 表、风格设定
      ↓
阶段二：角色图提示词    → 每人一张参考图 prompt（三视图+服装锁死）
      ↓
阶段三：场景图提示词    → 每场地一张空场景 prompt（无人物）
      ↓
门 A：等待图片         → 用户上传 RunningHub/ComfyUI 生成的图
      ↓
阶段四：图片检查        → 对照文字确认一致性，建立连续性记录
      ↓
阶段五：全局参考提示词  → 每个 Scene 一份（角色+背景描述）
      ↓
阶段六：LTX Clip 提示词 → 每 Scene 拆成少量 Clip（6-12 秒）
      ↓
阶段七：QC 检查        → 时长、对白、视线、连续性、音频
```

## 核心规则（不能违反）

### 角色一致性
- 每人**一张**参考图：左胸像 + 右三视图（正/侧/背全身）
- 中性深灰背景，无文字
- 同一人、同脸、同发型、同服装 —— 全部锁定

### 场景一致性
- 空场景（无人物）
- 固定灯光方向、色温、建筑空间锚点
- 足够两人中景对话的表演区域

### 镜头规则
- ❌ **禁止**远景/大全景人物镜头
- ✅ 优先：medium two-shot, medium close-up, close-up, over-the-shoulder
- 人物**看着对方**，用三分之四侧面，**不能对镜头说话**
- 用眼神、呼吸、下颌、手指、停顿表现情绪

### Prompt 规则
- 镜头/动作/光线用**英文**
- 对白保留**剧本原语言**（中文对白用中文）
- LTX 标点全部**ASCII**
- 每 ~2-3 秒一个可见节拍
- MSR 参考图顺序固定：1=角色1, 2=角色2, 3=背景
- 一个 MSR Clip 最多**两个**可见说话角色

### 每 Scene → 一个全局 prompt → 不重复在每个 Clip 里

## 与 ComfyUI 工作流的连接

```
智能体输出              ComfyUI 工作流 (MSR多参考图V2)
───────────            ─────────────────────────────
角色图 prompt    → RunningHub 生成角色图       → LoadImage 1,2
场景图 prompt    → RunningHub 生成场景图       → LoadImage 3
全局 prompt      → 输入到 global_prompt 文本框
Clip prompt      → 输入到 prompt (基础提示词) 文本框
时长/分辨率       → INTConstant / TTResolutionSelector
```

工作流：`LTX2.3-MSR多参考图V2`
- 模型：LTX 2.3 22B distilled
- LoRA：LTX-2.3-Licon-MSR-V2
- 文本编码器：Gemma 3 12B
- 输出：H.264 MP4, 24fps

## 最佳实践

1. **先做定妆照**：用 RunningHub 生成每个角色的三视图（1:1, 白底, neutral face），然后再用这个做参考图
2. **角色不要超过 2 人**：LTX MSR 只支持双角色，三人场景要拆分
3. **每 Scene 少拆 Clip**：宁可 1 个 12 秒 Clip 拍完一个戏剧节拍，不要拆成 3 个 4 秒
4. **AI 不要"导演创作"**：智能体只翻译你的剧本，不自作主张加戏

## 关系

- [[ltx]]
- [[ai-video-workflow]]
- [[comfyui]]
- [[runninghub]]
- [[prompt-engineering]]
