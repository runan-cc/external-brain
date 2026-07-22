---
title: Chain-of-Thought (CoT)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [inference, technique, reasoning]
sources: []
confidence: high
---

# Chain-of-Thought (CoT)

## 定义

Chain-of-Thought（思维链）是一种引导 [[large-language-model]] 进行**逐步推理**的技术。通过在 prompt 中要求模型展示推理过程（而非直接给出答案），显著提升了复杂推理任务的准确率。

## 核心形式

### Few-shot CoT

在 prompt 中提供带完整推理步骤的示例，模型模仿推理模式。

### Zero-shot CoT

无需示例，仅添加触发短语：
```
Let's think step by step.
让我们一步一步思考。
```

### Auto-CoT

自动为不同问题类型选择和生成最合适的 few-shot 示例。

## 为什么有效

- **分解复杂问题**：把困难任务拆成小步，降低每步难度
- **暴露推理过程**：使模型"检查"自己的推理，减少跳步错误
- **计算扩展**：更多 tokens = 更多前向传播步骤 = 更深推理

## o1/o3 类推理模型

OpenAI o1/o3、DeepSeek-R1 等推理模型将 CoT **内化到训练和推理中**：
- 模型自动生成隐藏的思维链（internal CoT）
- 通过 RL 和 CoT 数据训练增强推理能力
- test-time compute scaling：推理时消耗更多计算以提升质量

## 局限性

- 不一定保证正确推理（可能产生"看似合理但错误"的逻辑链）
- 增加输出长度和延迟
- 对极其简单的问题无增益

## 相关概念

- [[large-language-model]]
- [[prompt-engineering]]
- [[reasoning-models]] — o1/o3/DeepSeek-R1 类推理模型
