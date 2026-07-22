---
title: Vector Database
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [database, data, architecture, tool]
sources: []
confidence: high
---

# Vector Database（向量数据库）

## 定义

向量数据库是专门存储和检索高维 [[embedding]] 向量的数据库系统。它通过**近似最近邻搜索（ANN）** 实现高效的语义相似度查询，是 [[rag-retrieval-augmented-generation]] 的核心基础设施。

## 工作原理

```
文档 → Embedding 模型 → 向量 [d₁, ..., dₙ] → 向量数据库 → ANN 索引
                                                        ↓
查询 → Embedding → 查询向量 → 相似度搜索 → Top-K 结果
```

## 索引算法

| 算法 | 特点 |
|------|------|
| HNSW (Hierarchical NSW) | 分层图搜索，速度快，内存开销大 |
| IVF (Inverted File) | 聚类 + 倒排索引，内存节省 |
| PQ (Product Quantization) | 向量压缩，内存极省，精度略降 |
| DiskANN | 基于磁盘，超大规模支持 |

## 主流数据库

| 数据库 | 特点 | 适合场景 |
|--------|------|----------|
| Pinecone | 全托管，开箱即用 | 快速开始，不想运维 |
| Milvus | 开源，高性能，云原生架构 | 大规模生产 |
| Qdrant | Rust 实现，性能优异 | 中大规模 |
| Weaviate | GraphQL 原生，内置模块 | 多模态 |
| Chroma | 轻量，Python 原生 | 原型开发 / 小规模 |
| pgvector | PostgreSQL 扩展 | 已有 PG 基础设施 |
| Elasticsearch | 混合检索（dense + sparse） | 企业搜索 |

## 关键特性

- **相似度指标**：Cosine, Euclidean, Dot Product
- **Metadata 过滤**：向量搜索 + 结构化过滤（如 "2026 年的文章"）
- **多模态**：支持文本、图像、音频向量的统一存储和检索
- **分片与副本**：水平扩展和容错

## 相关概念

- [[embedding]]
- [[rag-retrieval-augmented-generation]]
- [[large-language-model]]
