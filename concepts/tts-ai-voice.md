---
title: TTS & AI 语音
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [tts, voice, ai, audio, multimedia]
sources: []
confidence: high
---

# TTS & AI 语音

## 定义

TTS (Text-to-Speech) 是将**文本转换为自然语音**的技术。从 1980 年代的机器人声到现在的 AI 语音，已经实现了人类自然度的突破。AI 视频中，语音/配音和画面同等重要。

## TTS 技术演进

| 阶段 | 技术 | 质量 |
|------|------|------|
| 1980s | Formant Synthesis | 机器人声 |
| 1990s | Concatenative (拼接) | 机械但可用 |
| 2016 | WaveNet (DeepMind) | 接近真人 |
| 2018 | Tacotron 2 + WaveNet | 真人级 🎯 |
| 2022 | VITS / FastSpeech 2 | 快速、高质量 |
| 2023-24 | GPT-SoVITS, Bark, ElevenLabs | 带情感、可控制、语音克隆 |
| 2024+ | GPT-4o 语音, Moshi | 实时对话、情感丰富 |

## 主流工具

### ElevenLabs (商业，质量王者)

| 特性 | 说明 |
|------|------|
| 自然度 | 最高，几乎无法分辨 |
| 语音克隆 | 30 秒音频 → 完美克隆 |
| 多语言 | 29 种语言，保留原始音色 |
| 情感控制 | 开心、悲伤、愤怒… |
| API | 可集成到工作流 |
| 费用 | 免费额度 + $5-22/月 |

### GPT-SoVITS (开源，社区最强)

```
参考音频 (1 分钟) + 参考文本
    ↓
语音特征提取 + 文本编码
    ↓
GPT 模型 → 声学特征
    ↓
SoVITS → 语音合成
```

| 优势 | 说明 |
|------|------|
| 中文最佳 | 比 ElevenLabs 中文自然度更高 |
| 仅需 1 分钟参考音频 | 几秒也行但质量低 |
| 完全本地 | 不依赖网络 |
| 免费开源 | 随意使用 |
| 生态 | WebUI、API、ComfyUI 节点 |

### Coqui-AI / XTTS v2

| 特性 | 说明 |
|------|------|
| 语音克隆 | 6 秒音频即可 |
| 跨语言 | 用英语音频说中文 |
| 开源 | Apache 2.0 |
| 情感 | 支持 |
| 速度 | 实时 |

### Fish Audio / Fish Speech

中国开源 TTS，中文表现好，带 WebUI，轻量级。

## 视频配音集成

```python
# Python 配音脚本示例
from elevenlabs import generate, save

with open("script.txt", "r") as f:
    lines = f.readlines()

for i, line in enumerate(lines):
    audio = generate(
        text=line,
        voice="Rachel",  # 或 cloned voice
        model="eleven_multilingual_v2"
    )
    save(audio, f"narration_{i:03d}.mp3")
```

然后在 DaVinci Resolve / Premiere Pro 中导入。

## TTS 质量对比

| 工具 | 中文 | 情感 | 克隆 | 速度 | 费用 |
|------|------|------|------|------|------|
| ElevenLabs | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | 快 | $ |
| GPT-SoVITS | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ | 中 | 免费 |
| Fish Audio | ⭐⭐ | ⭐ | ⭐⭐ | 快 | 免费 |
| XTTS v2 | ⭐⭐ | ⭐⭐ | ⭐⭐⭐ | 实时 | 免费 |
| Azure Speech | ⭐⭐⭐ | ⭐ | ❌ | 快 | $ |
| CosyVoice (阿里) | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ | 快 | 免费 |

## 语音到语音 (S2S)

不只是 TTS → 保留原始说话的节奏、情感、语气、停顿：

```
原始语音 → 语音识别 (ASR) → 翻译/改写 → TTS (保留情感)
```

| 工具 | 说明 |
|------|------|
| GPT-4o 实时语音 | 原生多模态，直接语音→语音 |
| RVC (Retrieval-based Voice Conversion) | 歌声/语音换声 |
| CosyVoice 2 | 阿里最新，支持 S2S |

## AI 配乐

| 工具 | 类型 | 特点 |
|------|------|------|
| Suno | 歌曲 + 音乐 | 文→歌曲，最流行 |
| Udio | 音乐 | 质量略高于 Suno |
| Mubert | 背景音乐 | 按场景/情绪生成 |
| AIVA | 古典/电影配乐 | 专业级 |

## 视频配音 Gold Stack

```
脚本 → ElevenLabs/GPT-SoVITS 配音
     → Suno/Udio 配乐
     → DaVinci Resolve 剪辑合成
     → 输出
```

## 关系

- [[ai-video-generation]]
- [[ai-video-workflow]]
- [[large-language-model]] — LLM 写脚本
