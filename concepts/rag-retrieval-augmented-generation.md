---
title: RAG (Retrieval-Augmented Generation)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [data, inference, architecture, database]
sources: []
confidence: high
---

# RAG (Retrieval-Augmented Generation)

## 定义

RAG（检索增强生成）是一种将**信息检索**与 [[large-language-model]] 生成相结合的技术。模型在生成回答前，先从外部知识库检索相关文档，将其作为上下文注入 prompt，从而减少幻觉、获取最新信息。

## 工作流程

```
用户查询 → Embedding → 向量检索 → 相关文档 → Prompt 拼接 → LLM 生成 → 回答
```

1. **索引（Indexing）**：文档 → 文本分块 → embedding → 向量数据库
2. **检索（Retrieval）**：查询 embedding → 语义相似度搜索 → Top-K 文档
3. **增强（Augmentation）**：检索结果拼入系统 prompt
4. **生成（Generation）**：LLM 基于 prompt + 上下文生成回答

## 关键技术

| 环节 | 技术选择 |
|------|----------|
| Embedding 模型 | text-embedding-3, bge-m3, Jina embeddings |
| 向量数据库 | Pinecone, Milvus, Qdrant, Weaviate, Chroma |
| 分块策略 | Fixed-size, Semantic, Recursive, Agentic chunking |
| 检索策略 | Dense (向量), Sparse (BM25/关键词), Hybrid |
| 重排序 | Cohere Rerank, Cross-encoder re-ranking |

## 高级模式

- **Self-RAG**：模型自行判断是否需要检索，以及检索结果是否相关
- **Graph RAG**：结合知识图谱的结构化关系 + 向量语义搜索
- **HyDE**（Hypothetical Document Embeddings）：先让 LLM 假设一个答案，用假设答案做检索
- **Multi-hop RAG**：多跳推理，一次检索的结果触发下一次检索

## 常见问题

| 问题 | 解决方向 |
|------|----------|
| 检索不相关 | 更好的 embedding + reranker |
| 上下文窗口溢出 | 压缩/摘要检索结果 |
| 分块破坏语义 | 语义分块 + 上下文窗口 overlap |
| 多模态检索 | 图文混合 embedding |

## 相关概念

- [[large-language-model]] — 生成层
- [[vector-database]] — 向量存储
- [[ai-agent]] — RAG 是 Agent 的知识基础组件
- [[embedding]] — 向量表示
