---
title: GraphQL
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [api, protocol, query, graphql]
sources: []
confidence: high
---

# GraphQL

## 概览

GraphQL 是 Facebook (Meta) 于 2015 年开源的**API 查询语言和运行时**。客户端可以精确指定需要的数据结构和字段，服务器返回恰好所需——不多不少。

## 核心概念

### Schema（架构定义）
```graphql
type User {
  id: ID!
  name: String!
  email: String
  posts: [Post!]!
}

type Post {
  id: ID!
  title: String!
  author: User!
}

type Query {
  user(id: ID!): User
  posts(limit: Int): [Post!]!
}
```

### Query（查询）
```graphql
query {
  user(id: "1") {
    name
    posts(limit: 5) {
      title
    }
  }
}
```

### Mutation（写入）
```graphql
mutation {
  createPost(title: "Hello", authorId: "1") {
    id
    title
  }
}
```

### Subscription（实时推送）
通过 WebSocket 订阅数据变更通知。

## 对比 REST

| 维度 | GraphQL | [[rest-api]] |
|------|---------|-------------|
| 数据获取 | 客户端定义（精确字段） | 服务器定义（固定结构） |
| 端点数 | 1 个 | 多个 |
| over/under fetching | 无 | 常见 |
| 缓存 | 需要额外工具 | HTTP 原生支持 |
| 版本管理 | Schema 演进 | URL 版本 |

参见 [[rest-vs-graphql]] 和 [[api-paradigms]]

## 生态

| 工具 | 说明 |
|------|------|
| Apollo Server/Client | 最流行的 GraphQL 实现 |
| Relay | Facebook 官方 React + GraphQL 框架 |
| GraphQL Codegen | 根据 Schema 生成类型代码 |
| Hasura | 数据库自动生成 GraphQL API |
| Graphene (Python) | Python GraphQL 框架 |

## 陷阱

- **N+1 问题**：需要 DataLoader 批量加载关联数据
- **复杂查询性能**：深度嵌套查询可能导致数据库压力
- **文件上传**：GraphQL 不是为此设计的，需要额外处理
- **学习曲线**：Schema 设计需要经验

## 关系

- [[rest-api]]
- [[rest-vs-graphql]]
- [[api-paradigms]]
