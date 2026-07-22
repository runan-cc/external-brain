---
title: Large Language Model (LLM)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [model, architecture, training, inference, scaling]
sources: []
confidence: high
---

# Large Language Model (LLM)

## 定义

大语言模型（LLM）是一类基于 [[transformer-architecture]] 的大规模神经网络模型，通过自监督学习在海量文本语料上训练，能够理解和生成自然语言。LLM 的核心特征是 **scaling law**——模型性能随参数量、数据量和计算量的增加而可预测地提升。

## 核心架构

- **Decoder-only**（GPT 系）：自回归生成，每个 token 只关注前面的 token。代表：GPT-4, Claude, Gemini, DeepSeek
- **Encoder-decoder**（T5 系）：编码器理解输入，解码器生成输出。代表：T5, BART
- **Encoder-only**（BERT 系）：主要用于理解任务，不适合生成。代表：BERT, RoBERTa

## 关键能力

| 能力 | 说明 | 示例 |
|------|------|------|
| In-context learning | 通过 prompt 示例学习，不需要 fine-tuning | few-shot prompting |
| Chain-of-thought | 逐步推理，输出中间步骤 | [[chain-of-thought]] |
| Tool use | 调用外部工具/API | function calling, MCP |
| Multimodal | 处理图像、音频等多模态输入 | GPT-4V, Gemini |

## 当前知识状态

- **Scaling law 仍在继续**，但边际收益递减
- **开源追赶闭源**：DeepSeek、Llama 等开源模型性能逼近 GPT-4 级别
- **推理模型崛起**：o1/o3 类模型通过 test-time compute 实现更强的推理能力
- **Agent 化趋势**：LLM 从对话走向自主行动（[[ai-agent]]）

## 待解决问题

- **幻觉（Hallucination）**：模型生成看似合理但事实错误的内容
- **推理成本**：强推理模型（如 o3）单次推理可能消耗数百万 tokens
- **对齐（Alignment）**：如何确保模型行为符合人类意图
- **上下文窗口与注意力的权衡**：长上下文 ≠ 有效注意力

## 相关概念

- [[transformer-architecture]] — 底层架构
- [[chain-of-thought]] — 推理增强技术
- [[ai-agent]] — LLM 驱动的自主智能体
- [[fine-tuning]] — 微调技术
- [[prompt-engineering]] — 提示工程
