---
title: Prompt Engineering
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [technique, inference, optimization]
sources: []
confidence: high
---

# Prompt Engineering（提示工程）

## 定义

Prompt Engineering 是设计和优化输入提示（prompt），以引导 [[large-language-model]] 产生预期输出的技术。它是目前最广泛使用的 LLM 控制方法，不需要修改模型参数。

## 核心技巧

### 角色设定

```
你是一位资深 Python 开发者。请审查以下代码...
```

通过角色定义约束模型的行为空间。

### Few-shot Prompting

在 prompt 中提供 2-5 个示例，让模型通过 in-context learning 理解任务格式和要求。

### Chain-of-Thought (CoT)

参见 [[chain-of-thought]]。在 prompt 中添加"让我们一步一步思考"引导模型推理。

### 结构化输出

要求模型按 JSON、YAML、Markdown 表格等固定格式输出，便于程序解析。

## 高级技术

| 技术 | 说明 |
|------|------|
| Self-Consistency | 多次采样选最优答案 |
| Tree of Thoughts | 多分支探索 + 回溯搜索 |
| ReAct | 推理+行动循环（见 [[ai-agent]]） |
| Automatic Prompt Engineering | 用 LLM 自动优化 prompt（DSPy, APO） |

## 最佳实践

- **具体 > 抽象**：明确输出格式、长度、风格
- **正面指令 > 负面约束**：告诉模型"该做什么"而非"不要做什么"
- **上下文窗口利用**：把最重要的指令放在开头和结尾
- **System prompt vs User prompt**：系统级指令优先级最高

## 相关概念

- [[large-language-model]] — 被提示的对象
- [[chain-of-thought]] — 核心推理方法
- [[ai-agent]] — Agent 的系统 prompt 设计
- [[fine-tuning]] — 不写 prompt 时的替代方案
