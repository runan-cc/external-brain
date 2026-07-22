---
title: AI Agent
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [agent, tool, automation, architecture]
sources: []
confidence: high
---

# AI Agent（AI 智能体）

## 定义

AI Agent 是以 [[large-language-model]] 为核心，具备**感知、规划、决策、执行**能力的自主系统。与传统的"一问一答" chatbot 不同，Agent 能主动调用工具、分解任务、迭代执行，并在失败时自我纠错。

## 核心架构模式

### ReAct（Reasoning + Acting）

交替进行推理和行动——模型先思考（Thought），再执行（Action），观察结果（Observation），循环直到完成任务。

### Plan-and-Execute

先制定完整计划，再逐步执行。适合复杂多步任务。

### Tool Use / Function Calling

Agent 通过结构化接口（JSON Schema）调用外部工具：搜索 API、代码执行器、数据库查询、文件操作等。

## 关键组件

| 组件 | 职责 |
|------|------|
| LLM 核心 | 推理、规划、生成 |
| 记忆系统 | 短期（对话历史）、长期（向量数据库、知识库） |
| 工具集 | API、代码沙箱、浏览器、文件系统 |
| 规划器 | 任务分解与调度 |
| 反思机制 | 自我评估、错误恢复 |

## 当前趋势

- **MCP (Model Context Protocol)**：Anthropic 提出的 Agent-Tool 通信标准协议
- **Multi-Agent 系统**：多个 Agent 协作，分工完成复杂任务，如 AutoGen、CrewAI
- **Desktop Agent**：直接操控 GUI 的 Agent（OpenClaw、Claude Computer Use）
- **Coding Agent**：Devin、Cursor、Claude Code 等自主编程 Agent

## 挑战

- **可靠性**：多步任务中错误累积
- **安全性**：Agent 拥有执行权限时的风险控制
- **成本**：长任务消耗大量 tokens
- **评估**：缺乏标准化的 Agent 能力基准

## 相关概念

- [[large-language-model]] — Agent 的核心引擎
- [[chain-of-thought]] — 推理方法
- [[prompt-engineering]] — Agent 指令设计
- [[rag-retrieval-augmented-generation]] — 知识增强
