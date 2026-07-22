---
title: Anthropic
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [company, model, safety]
sources: []
confidence: high
---

# Anthropic

## 概览

Anthropic 是一家以 **AI 安全** 为核心使命的 AI 公司，由前 OpenAI 员工 Dario Amodei 和 Daniela Amodei 于 2021 年创立。其旗舰模型 Claude 以安全性和长上下文著称。

## 关键模型

| 模型 | 发布时间 | 特点 |
|------|----------|------|
| Claude 1 | 2023-03 | 首发，安全对齐 |
| Claude 2 | 2023-07 | 100K 上下文窗口 |
| Claude 3 (Opus/Sonnet/Haiku) | 2024-03 | 多模态，分级产品线 |
| Claude 3.5 Sonnet | 2024-06 | 编程/推理大幅提升 |
| Claude 4 (Opus/Sonnet) | 2025-06 | 前沿性能，Agent 能力 |

## 核心技术

- **Constitutional AI**：通过规则（宪法）而非人类反馈进行对齐，减少 RLHF 的标注成本
- **长上下文**：最早大规模支持 100K-200K token 上下文
- **MCP (Model Context Protocol)**：Agent-Tool 通信的标准协议
- **Computer Use**：Claude 可以直接操控桌面 GUI
- **Artifacts**：Claude 可以生成可交互的前端产物

## 特色

- **写作风格**：表达偏冷静、谨慎，较少过于自信的错误
- **编程能力**：3.5 Sonnet 在 SWE-bench 上表现领先
- **透明度**：发布 System prompt 和 Model Card

## 关系

- [[large-language-model]]
- [[openai]] — 主要竞争对手
- [[ai-agent]] — MCP 和 Computer Use 是 Agent 的重要基础
