---
title: RunningHub
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [tool, api, cloud, image-generation, text-to-image, image-to-image]
sources: ["https://www.runninghub.cn"]
confidence: high
---

# RunningHub

## 概览

RunningHub 是一个**云端 AI 图像生成 API 平台**（中国），提供文生图和图生图服务。通过 HTTP API 提交任务、轮询结果、下载图片，适合做 AI 视频制作流程中的「图像生成层」——把图像推理卸载到云端，本地 GPU 专注于视频生成。

## 核心理念

```
本地脚本 ──POST JSON──→ RunningHub API (云端推理)
    ↓                          ↓
  Python/RH.xxx()          GPU 集群处理
    ↓                          ↓
 轮询 taskId               返回图片 URL
    ↓                          ↓
 下载到本地 ←──────────────────┘
```

## API 端点

| 功能 | 方法 | 端点 |
|------|------|------|
| **文生图** | POST | `/openapi/v2/rhart-image-g-2/text-to-image` |
| **图生图** | POST | `/openapi/v2/rhart-image-g-2/image-to-image` |
| **查询任务** | POST | `/openapi/v2/query` |
| **上传图片** | POST | `/openapi/v2/media/upload/binary` |

Base URL: `https://www.runninghub.cn`

## Python 客户端

```python
from runninghub_client import RH

# 文生图
result = RH.text_to_image(
    "一只可爱的小猫", 
    aspect_ratio="1:1",
    resolution="2k"
)

# 图生图 (传参考图)
result = RH.image_to_image(
    "骑士骑马在森林中", 
    image_urls=["https://..."], 
    aspect_ratio="16:9"
)

# 上传本地图片 → 获取URL
url = RH.upload("E:/项目/定妆照.png")

# 下载结果
paths = RH.download(result, "E:/output")

# 快捷: 生成定妆照 (1:1 白底半身, 2k)
result, paths = RH.make_portrait("年轻女侠，长发飘逸")

# 快捷: 定妆照→图生图出分镜
result, paths = RH.make_storyboard(
    "夜晚的竹林里，女侠拔剑",
    portrait_url="https://...",
    aspect_ratio="9:16"
)
```

## 关键参数

### 文生图 / 图生图

| 参数 | 说明 |
|------|------|
| `prompt` | 提示词 1-20000 字符 |
| `aspectRatio` | 1:1 / 16:9 / 9:16 / 2:3 / 3:2 / 4:5 / 5:4 / 4:3 / 3:4 / 21:9 / 9:21 / 2:1 / 1:2 / 3:1 / 1:3 |
| `resolution` | 1k / 2k / 4k |
| `imageUrls` | 参考图 URL 列表（图生图，最多 10 张，每张 ≤30MB） |
| `webhookUrl` | 回调地址（可选，异步通知） |

### 任务状态

| 状态 | 说明 |
|------|------|
| `PENDING` | 排队中 |
| `RUNNING` | 生成中（2k 约 2-5 分钟） |
| `SUCCESS` | 完成 |
| `FAILED` | 失败 |

## 实战模式

### 模式一：生成定妆照（角色设计）

```
写角色描述 → RH.make_portrait() → 1:1 白底半身定妆照
```

输出用作后续图生图的参考图（角色一致性）。

### 模式二：定妆照 → 分镜图（推荐）

```
定妆照 URL
    ↓
RH.make_storyboard()  × N 个分镜描述
    ↓
N 张分镜关键帧 → 送入 ComfyUI 生成视频
```

### 模式三：批量场景生成

用脚本循环调用 `RH.text_to_image()`，一次生成多种场景、多种比例。

## 注意事项

1. **防止文字乱入**：prompt 末尾加 `"absolutely no text, no Chinese characters"`，避免中文/乱码出现在画面
2. **URL 有效期**：结果图片 URL 和上传 URL 有效期 **24 小时**，及时下载
3. **图生图白底问题**：如果参考图是白底定妆照，生成近景/特写时背景可能继承白底 → 修复：把场景描述放在 prompt **最前面**，角色描述放后面
4. **超时设置**：单次推理 2-5 分钟（2k），轮询超时设 ≥300 秒
5. **PowerShell 踩坑**：PS 5.1 发 JSON body 用 `WebClient.UploadString`，不要用 `Invoke-WebRequest`（可能报 errorCode=1007）

## 在 AI 视频流程中的位置

```
RunningHub (云端出图) → ComfyUI (本地出视频) → DaVinci (剪辑)
     ↑                         ↑
  定妆照+分镜             LTX2.3 / Wan 2.2
```

这样本地 RTX 5090 的 VRAM 全部留给视频生成，图像推理不占资源。

## 关系

- [[comfyui]]
- [[ai-video-workflow]]
- [[ai-video-generation]]
- [[rest-api]]
