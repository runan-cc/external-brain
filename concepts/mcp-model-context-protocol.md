---
title: MCP (Model Context Protocol)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [protocol, agent, tool, api]
sources: []
confidence: high
---

# MCP (Model Context Protocol)

## 定义

MCP（Model Context Protocol）是 [[anthropic]] 于 2024 年 11 月发布的开放标准协议，用于 **AI 模型与外部工具/数据源之间的标准化通信**。它定义了 Agent 如何发现、调用和接收工具的响应，类似于 AI 领域的"USB-C 接口"。

## 架构

```
AI Host (Claude/Cursor/etc.)
    ↕ MCP Protocol
MCP Server (工具实现)
    ↕
外部系统 (数据库/API/文件系统/浏览器)
```

## 核心概念

| 概念 | 说明 |
|------|------|
| MCP Server | 工具/数据源的标准化包装器 |
| Resource | 可供 AI 读取的数据（文件、数据库记录） |
| Tool | 可供 AI 调用的操作（搜索、执行命令） |
| Prompt | 预定义的任务模板 |
| Transport | stdio（本地） 或 HTTP/SSE（远程） |

## 为什么重要

- **标准化**：替代每个 AI 平台各自定义 function calling 格式，减少碎片化
- **可复用**：一个 MCP Server 可被 Claude、Cursor、Zed 等多个 AI 客户端使用
- **安全性**：通过标准化的权限控制模型
- **开源生态**：社区已贡献大量 MCP Server（数据库、搜索引擎、文件系统）

## 竞品/替代

- **OpenAI Function Calling / Tools API**：OpenAI 自有方案，绑定 OpenAI API
- **LangChain Tools**：Python 生态，灵活性高但缺乏跨平台标准化
- **Google A2A**：Google 的 Agent-to-Agent 协议

## 关系

- [[anthropic]] — MCP 的创建者
- [[ai-agent]] — MCP 为 Agent 提供工具接口
- [[rest-api]] — MCP 是更高层的 AI 交互协议
