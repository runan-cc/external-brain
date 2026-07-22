# Wiki Index

> 内容目录。每个 wiki 页面在对应分类下列出 + 一句话摘要.
> 先看这里找到相关页面.
> 最后更新: 2026-07-22 | 总页面数: 85

## 硬件与体系结构

- [[computer-architecture]] — 计算机体系结构：Von Neumann、CPU、内存层次、RISC vs CISC
- [[gpu]] — GPU 概览：CUDA、Tensor Core、深度学习硬件、H100/B200/Ascend

## 操作系统

- [[operating-system]] — 操作系统：进程调度、虚拟内存、分页、文件系统
- [[linux]] — Linux 操作系统内核，服务器/嵌入式/云计算的基础

## 网络与协议

- [[computer-networking]] — 计算机网络基础：拓扑、设备、路由、IP/子网
- [[tcpip]] — TCP/IP 协议栈：四层模型、TCP/UDP、QUIC、OSI 对比
- [[dns]] — 域名解析系统：A/CNAME/MX 记录、DoH/DoT
- [[http]] — HTTP 协议：版本演进、状态码、HTTPS、CORS、缓存
- [[tls-ssl]] — TLS/SSL 加密：握手、TLS 1.3、证书、前向安全
- [[rest-api]] — REST API 设计规范
- [[grpc]] — 高性能 RPC 框架，基于 Protobuf + HTTP/2
- [[mcp-model-context-protocol]] — MCP：AI 模型与工具的标准化通信协议

## 编程语言

- [[c-language]] — C 语言：系统编程的基石，操作系统/嵌入式的实现语言
- [[cpp]] — C++：多范式系统编程，零成本抽象，游戏/数据库/浏览器引擎
- [[rust]] — Rust：内存安全的系统编程语言，所有权模型
- [[go]] — Go：简洁、并发优先的编译型语言，云原生基础设施主力
- [[python]] — Python：AI/ML 和数据科学的绝对主流语言
- [[javascript]] — JavaScript：Web 的核心脚本语言，事件驱动 + 异步
- [[typescript]] — TypeScript：JS 的超集，静态类型系统
- [[java]] — Java：企业级应用和 Android 开发的核心语言
- [[nodejs]] — Node.js：基于 V8 的 JavaScript 服务端运行时

## 编程理论与实践

- [[programming-paradigms]] — 编程范式总览：命令式、声明式、OOP、FP、响应式
- [[object-oriented-programming]] — OOP：面向对象编程，SOLID 原则、设计模式
- [[functional-programming]] — 函数式编程：纯函数、不可变性、高阶函数、Monad
- [[data-structures-and-algorithms]] — 数据结构与算法：数组/链表/树/图 + 排序/搜索/DP
- [[compiler]] — 编译原理：Lexer→Parser→AST→IR→优化→代码生成
- [[regular-expressions]] — 正则表达式：模式匹配和文本处理的强大工具
- [[webassembly]] — WebAssembly：浏览器中的底层字节码，接近原生速度

## 数据库

- [[sql]] — SQL：关系型数据库查询语言，DDL/DML/DCL
- [[acid-transactions]] — ACID 事务：原子性、一致性、隔离性、持久性、MVCC
- [[postgresql]] — PostgreSQL：最先进的开源关系型数据库
- [[vector-database]] — 向量数据库：Pinecone、Milvus、Qdrant、Chroma

## 开发工具与 DevOps

- [[git]] — 分布式版本控制系统，现代软件开发的基础设施
- [[github]] — 全球最大的代码托管和协作平台
- [[docker]] — 容器化平台，一次构建到处运行
- [[kubernetes]] — 容器编排平台，云原生的事实标准
- [[ci-cd]] — 持续集成/持续部署：自动化构建测试部署
- [[obsidian]] — 基于本地 Markdown 的知识管理应用
- [[vscode]] — Microsoft 开源代码编辑器，最流行的开发工具
- [[react]] — React：Meta 的声明式 UI 库，最主流的前端框架
- [[graphql]] — GraphQL：API 查询语言和运行时

## 安全

- [[cryptography]] — 密码学基础：对称/非对称加密、哈希、数字签名、TLS/SSH

## AI/ML

### AI/ML 核心
- [[large-language-model]] — 大语言模型：基于 Transformer 的大规模文本生成模型
- [[transformer-architecture]] — Transformer 架构：自注意力驱动的神经网络基础架构
- [[moe-mixture-of-experts]] — MoE：混合专家架构，参数增长而计算可控
- [[scaling-laws]] — 缩放定律：模型性能与规模的可预测关系
- [[diffusion-models]] — 扩散模型：DALL-E / Stable Diffusion / Sora 的底层架构

### LLM 技术
- [[ai-agent]] — AI 智能体：能感知、规划、执行任务的自主 AI 系统
- [[prompt-engineering]] — 提示工程：设计和优化 LLM 输入以控制输出的技术
- [[chain-of-thought]] — 思维链：引导 LLM 逐步推理的技术
- [[fine-tuning]] — 微调：在预训练模型上用特定数据继续训练
- [[lora]] — 参数高效微调：只训练低秩矩阵，<1% 参数
- [[rlhf]] — RLHF / DPO：通过人类偏好对齐 AI 行为
- [[reinforcement-learning]] — 强化学习：通过试错和奖励学习最优策略
- [[rag-retrieval-augmented-generation]] — RAG：检索增强生成，用外部知识减少幻觉
- [[embedding]] — 向量嵌入：将非结构化数据映射到高维向量空间

### AI 公司
- [[deepseek]] — 深度求索，以高性能开源 LLM (DeepSeek-V3/R1) 著称
- [[openai]] — GPT/ChatGPT/o1/Sora 的创造者
- [[anthropic]] — Claude 系列模型的开发者，MCP 协议的创建者

## Comparisons (比较/对比)

- [[rest-vs-graphql]] — REST vs GraphQL：两种 API 范式对比
- [[api-paradigms]] — REST vs GraphQL vs gRPC：三种 API 范式三国杀
- [[sql-vs-nosql]] — SQL vs NoSQL：关系型与非关系型数据库对比

### ML 基础
- [[machine-learning]] — 机器学习基础：监督/无监督、分类/回归、偏差-方差
- [[gradient-descent]] — 梯度下降：SGD、Adam、学习率调度、鞍点
- [[information-theory]] — 信息论：熵、交叉熵、KL 散度、信道容量

## 前端

- [[html-css]] — HTML & CSS：Web 结构和样式的基石
- [[browser-internals]] — 浏览器工作原理：渲染路径、V8、事件循环、Core Web Vitals

## 中间件

- [[kafka]] — Kafka：分布式提交日志，流处理平台
- [[redis]] — Redis：内存数据结构存储，缓存/消息/排行榜
- [[message-queue]] — 消息队列：异步通信、Kafka vs RabbitMQ

## Comparisons (比较/对比)

- [[rest-vs-graphql]] — REST vs GraphQL：两种 API 范式对比
- [[api-paradigms]] — REST vs GraphQL vs gRPC：三种 API 范式三国杀
- [[sql-vs-nosql]] — SQL vs NoSQL：关系型与非关系型数据库对比
- [[rdbms-vs-document-db]] — RDBMS vs Document DB：关系型与文档型数据库对比

## Queries (查询归档)

<!-- 查询记录按时间倒序 -->
