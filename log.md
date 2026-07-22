# Wiki Log

> 所有 wiki 操作的时间线记录。只追加不删除。
> 格式: `## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete
> 超过 500 条时轮转: 重命名为 log-YYYY.md, 新建 log.md。

## [2026-07-22] create | 第二轮知识库扩充
- 新增概念页: moe-mixture-of-experts, vector-database, scaling-laws, lora, mcp-model-context-protocol, grpc, rlhf, reinforcement-learning, diffusion-models
- 新增实体页: linux, kubernetes, typescript, github, nodejs
- 新增比较页: api-paradigms, sql-vs-nosql
- 更新 index.md: 总页面数 32，重组分类结构
- 本轮 +14 页

## [2026-07-22] create | 基础知识库批量创建
- 目录结构初始化: entities/, concepts/, comparisons/, queries/, raw/articles/, _archive/
- 创建 16 个页面（8 entities + 10 concepts + 1 comparison + log 更新）
- Vault 配置: Obsidian Git 插件 v2.38.6, SSH 同步至 github.com/runan-cc/external-brain

### 实体页面 (8)
- deepseek, openai, anthropic — AI/ML 公司
- git, docker — DevOps 工具
- python — 编程语言
- obsidian, vscode — 工具/编辑器

### 概念页面 (10)
- large-language-model, transformer-architecture, chain-of-thought, fine-tuning — AI 核心技术
- ai-agent, prompt-engineering, rag-retrieval-augmented-generation, embedding — LLM 应用技术
- rest-api, ci-cd — 软件工程概念

### 比较页面 (1)
- rest-vs-graphql — API 范式对比

## [2026-07-22] create | 第三轮知识库扩充 — 计算机全领域覆盖
- 硬件/体系结构: computer-architecture, gpu
- 操作系统: operating-system
- 网络/协议: computer-networking, tcpip, dns, http, tls-ssl (5页)
- 编程语言: javascript, rust, go, c-language, cpp, java (6页)
- 数据库: sql, acid-transactions, postgresql, graphql (4页)
- 编程理论: programming-paradigms, object-oriented-programming, functional-programming, data-structures-and-algorithms, compiler, regular-expressions, webassembly (7页)
- 前端/工具: react
- 安全: cryptography
- 本轮 +28 页，总计 65 页

### 当前目录结构
```
external-brain/
├── entities/        22 页
├── concepts/        37 页
├── comparisons/      3 页
├── index.md, log.md, SCHEMA.md
```

## [2026-07-22] create | 第二轮知识库扩充
- 新增概念页: moe-mixture-of-experts, vector-database, scaling-laws, lora, mcp-model-context-protocol, grpc, rlhf, reinforcement-learning, diffusion-models
- 新增实体页: linux, kubernetes, typescript, github, nodejs
- 新增比较页: api-paradigms, sql-vs-nosql
- 更新 index.md: 总页面数 32，重组分类结构
- 本轮 +14 页

## [2026-07-22] create | 基础知识库批量创建
- 目录结构初始化: entities/, concepts/, comparisons/, queries/, raw/articles/, _archive/
- 创建 16 个页面（8 entities + 10 concepts + 1 comparison + log 更新）
- Vault 配置: Obsidian Git 插件 v2.38.6, SSH 同步至 github.com/runan-cc/external-brain

### 实体页面 (8)
- deepseek, openai, anthropic — AI/ML 公司
- git, docker — DevOps 工具
- python — 编程语言
- obsidian, vscode — 工具/编辑器

### 概念页面 (10)
- large-language-model, transformer-architecture, chain-of-thought, fine-tuning — AI 核心技术
- ai-agent, prompt-engineering, rag-retrieval-augmented-generation, embedding — LLM 应用技术
- rest-api, ci-cd — 软件工程概念

### 比较页面 (1)
- rest-vs-graphql — API 范式对比

## [2026-06-14] create | 知识库初始化
- 领域: 通用知识库 (AI/ML, 开发, DevOps, 工具链, 系统设计等)
- 结构创建: SCHEMA.md, index.md, log.md
- 目录: raw/, entities/, concepts/, comparisons/, queries/, _archive/
