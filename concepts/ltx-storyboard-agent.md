---
title: LTX 2.3 导演台
created: 2026-07-22
updated: 2026-07-23
type: concept
tags: [storyboard, ltx, prompt-engineering, workflow, agent, directing]
sources: ["local skill: ltx23-script-to-video"]
confidence: high
---

# LTX 2.3 导演台

## 定义

LTX 2.3 导演台是一个**从剧本到 AI 视频成品的完整导演系统**。V2 版本的根本性升级：不再是"剧本翻译成提示词"的格式工程师，而是**做出视觉决策的导演**。

## V1 → V2 的变化

| 维度 | V1（格式翻译器） | V2（导演台） |
|------|-----------------|-------------|
| 分镜 | 按场景拆 Clip | 先做节拍分析 + 权力关系图，再拆 |
| 景别 | 规则：不用远景 | 决策：这个镜头的视觉意图是什么，景别服务于它 |
| 节奏 | 每段 6-12 秒 | 60 秒情绪弧线模板，留白设计 |
| 视觉 | 描述动作 | 每个 Clip 标注 visual intent |
| 输出 | 只有 prompt | 入口/转折/出口镜头设计 + prompt |

## 为什么需要导演台

AI 视频讲不好故事的原因不是 prompt 格式不对，而是：
- **文字和视觉是两套编码系统** — 同一句台词可以拍成十种不同的镜头
- **AI 没有审美判断** — 需要人来决定「这个 moment 用什么拍」
- **LTX 有物理限制** — 6-12 秒单 Clip，没有剪辑自由，必须提前设计节奏

## 8 阶段流程（V2）

```
阶段一：剧本锁定 + 情绪分析   → 角色表、Scene 表、情绪弧线、节拍分析
      ↓
阶段二：分镜设计（导演决策）   → 入口/转折/出口镜头、权力关系、Clip 拆分 + visual intent
      ↓
阶段三：角色图提示词          → RunningHub prompt（定妆照而非三视图）
      ↓
阶段四：场景图提示词          → 空场景 prompt
      ↓
门 A：等待图片               → 用户生成并上传
      ↓
阶段五：图片检查              → 观察实际外观，建立连续性台账
      ↓
阶段六：全局参考提示词        → 基于观察，每个 Scene 一份
      ↓
阶段七：LTX Clip 提示词       → 含 visual intent 标注
      ↓
阶段八：QC 检查              → 时长、对白、视线、节奏、音频
```

## 导演思维核心

### 节拍分析
每个 Scene 只有一个核心任务：建立/推进/转折/悬念/解决。

### 景别情绪
| 景别 | 感受 | 使用频率 |
|------|------|----------|
| Medium two-shot | 关系感 | 主镜头 |
| Medium close-up | 紧张/亲密 | 情绪上升 |
| Close-up | 脆弱/震惊 | 每 Scene 最多一次 |
| Over-the-shoulder | 主观/权力 | 揭示权力关系 |
| Reaction close-up | 隐藏真相 | 比说话更重要 |

### 权力与位置
- 屏幕左侧 = 主动方 / 支配方
- 屏幕右侧 = 被动方 / 防守方
- 权力反转 → 交换位置

### 节奏模板
```
60s 短片：
0-10s   → 建立（谁在哪，什么气氛）
10-25s  → 推进（冲突展开）
25-40s  → 升级（紧张加剧，景别收紧）
40-50s  → 转折（关键信息，唯一 close-up）
50-60s  → 解决（释放，后退/离开）
```

### 对白视觉替代
不说"我很生气" → 下颌收紧、手指掐桌沿、停顿两秒再开口
每句对白前后留 1-2 秒沉默反应空间

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

1. **定妆照代替三视图**：RunningHub 无法准确生成三视图排版，用高质量正面胸像定妆照（1:1，中性表情，黑灰背景）
2. **角色 ≤ 2 人**：LTX MSR 只支持双角色。三人场景要拆分为成对的 Clip
3. **少拆 Clip，每段有自己的生命**：1 个 10 秒 Clip > 3 个 3 秒 Clip
4. **Close-up 是稀有资源**：每 Scene 最多一次，用在本场戏最关键的情绪时刻
5. **先想视觉，后写 prompt**：不要急着格式化。先问自己"这个镜头要传达什么"

## 关系

- [[ltx]]
- [[ai-video-workflow]]
- [[comfyui]]
- [[runninghub]]
- [[prompt-engineering]]
