---
title: React
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [javascript, framework, web, react]
sources: []
confidence: high
---

# React

## 概览

React 是 Meta (Facebook) 于 2013 年开源的**声明式 UI 库**。以组件化、虚拟 DOM 和单向数据流著称，是目前最主流的前端 UI 框架。

## 核心概念

### 组件
```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```

### State & Hooks
| Hook | 用途 |
|------|------|
| `useState` | 组件状态 |
| `useEffect` | 副作用（数据获取、订阅） |
| `useContext` | 跨组件共享数据 |
| `useRef` | 持久化引用 |
| `useMemo` / `useCallback` | 性能优化 |

### Virtual DOM
React 维护内存中的虚拟 DOM 树，diff 后只更新实际变化的 DOM 节点。

### 单向数据流
`Parent → Props → Child`，数据向下流动，事件向上冒泡。

## 生态

| 工具 | 说明 |
|------|------|
| Next.js | 全栈框架 (SSR/SSG/API routes) |
| React Router | 客户端路由 |
| Redux / Zustand | 状态管理 |
| React Query (TanStack) | 服务端状态管理 |
| React Native | 移动端开发 |
| Tailwind CSS | 实用优先的样式方案 |

## React vs Vue vs Angular

| 维度 | React | Vue | Angular |
|------|-------|-----|---------|
| 库 vs 框架 | 库 | 渐进式框架 | 完整框架 |
| 学习曲线 | 中 | 低 | 高 |
| 类型支持 | TS | TS | TS 内置 |
| 数据绑定 | 单向 | 双向 |

## 关系

- [[javascript]]
- [[typescript]]
- [[nextjs]]
- [[vue]]
