---
title: Embedding
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [model, data, inference]
sources: []
confidence: high
---

# Embedding（向量嵌入）

## 定义

Embedding 是将文本、图像、音频等非结构化数据映射到**高维向量空间**的技术。语义相近的内容在向量空间中距离更近，语义不相关的距离更远。它是 [[rag-retrieval-augmented-generation]] 和语义搜索的基础。

## 工作原理

```
文本 → Tokenization → Embedding 模型 → 向量 [d₁, d₂, ..., dₙ]
```

典型维度：768 (BERT), 1536 (OpenAI ada), 1024 (bge-large), 4096 (Jina v3)

## 常用模型

| 模型 | 提供方 | 维度 | 特点 |
|------|--------|------|------|
| text-embedding-3-large | OpenAI | 3072/256/1024 | 可变维度，MTEB 领先 |
| bge-m3 | BAAI | 1024 | 多语言，支持 dense+sparse |
| Jina embeddings v3 | Jina AI | 1024 | 8192 token 上下文，多语言 |
| Cohere Embed v3 | Cohere | 1024 | 分类优化 |
| GTE-Qwen2 | 阿里 | 多种 | 开源强模型 |

## 评估指标

- **MTEB**（Massive Text Embedding Benchmark）：综合评估检索、分类、聚类、语义相似度等任务

## 应用场景

- **语义搜索**：用户查询 → embedding → 相似度排序
- **RAG 检索**：见 [[rag-retrieval-augmented-generation]]
- **聚类与分类**：文本相似度聚类
- **推荐系统**：用户/内容 embedding 匹配
- **异常检测**：偏离正常分布的向量

## 相关概念

- [[rag-retrieval-augmented-generation]]
- [[vector-database]]
- [[large-language-model]]
