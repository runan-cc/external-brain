---
title: DeepSeek
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [company, model, open-source, china]
sources: []
confidence: high
---

# DeepSeek

## 概览

DeepSeek（深度求索）是中国 AI 研究公司，由幻方量化孵化。以**高性能开源模型**著称，在推理能力和性价比上直接挑战 OpenAI。

## 关键模型

| 模型 | 发布时间 | 特点 |
|------|----------|------|
| DeepSeek-V2 | 2024-05 | MoE 架构，高性价比 |
| DeepSeek-V3 | 2024-12 | 671B MoE（37B 活跃），训练成本仅 $5.6M |
| DeepSeek-R1 | 2025-01 | 开源推理模型，对标 o1，支持思维链可视化 |

## 核心技术

- **Multi-head Latent Attention (MLA)**：大幅减少 KV cache 显存占用
- **DeepSeekMoE**：细粒度 MoE + 共享专家（shared experts）
- **Multi-Token Prediction (MTP)**：同时预测多个后续 token，提升训练效率
- **FP8 混合精度训练**：在 V3 中全面使用 FP8，大幅降低训练成本
- **纯 RL 推理训练**：R1-Zero 未使用 SFT 数据，仅通过 RL 习得推理能力

## 行业影响

- 证明了**高效训练**可以大幅压缩成本（V3 训练成本是同等规模模型的 1/10-1/20）
- 推动了**开源模型**与闭源模型的差距缩小
- R1 引发全球关注，展示了中国 AI 的研发实力

## 局限

- 中文能力突出，部分多语言场景弱于 GPT-4
- 内容审核机制较严格，某些话题可能拒答
- 生态系统（API、插件）不及 OpenAI 成熟

## 关系

- [[large-language-model]] — DeepSeek 是一类 LLM
- [[transformer-architecture]] — 底层架构
- [[reasoning-models]] — R1 是典型推理模型
- [[moe-mixture-of-experts]] — V2/V3 的核心架构
