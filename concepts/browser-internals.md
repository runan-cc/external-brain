---
title: 浏览器工作原理
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [browser, web, performance, architecture]
sources: []
confidence: high
---

# 浏览器工作原理

## 定义

浏览器是最复杂的桌面应用之一——它是现代 Web 应用的运行时环境，集成了 HTML 解析、CSS 布局、JS 引擎、网络栈、GPU 渲染等。

## 浏览器架构

```
┌─────────────────────────────────────┐
│   Browser Process (主进程)            │
│   UI, 地址栏, 书签, 网络, 存储        │
├─────────────────────────────────────┤
│   Renderer Process (渲染进程) × N     │
│   ↓                                  │
│   GPU Process (合成、绘制)            │
├─────────────────────────────────────┤
│   Network, Storage, Plugin...        │
└─────────────────────────────────────┘
```

Chrome 采用**多进程架构**：每个 tab 一个渲染进程，崩溃不影响其他 tab。

## 关键渲染路径 (Critical Rendering Path)

```
HTML
 ↓ Parse
DOM Tree ──┐
            ├──→ Render Tree ──→ Layout ──→ Paint ──→ Composite
CSS        │    (合并后)        (几何位置)  (像素绘制)  (图层合成)
 ↓ Parse   │
CSSOM     ─┘
```

### 阻塞点

| 资源 | 阻塞 |
|------|------|
| CSS | **渲染阻塞**（必须等 CSSOM 完成） |
| JS (同步) | **解析阻塞**（`<script>` 暂停 HTML 解析） |
| JS (async) | 下载时不阻塞，执行时阻塞 |
| JS (defer) | HTML 解析完后再执行 |
| 图片/字体 | 不阻塞 |

> **优化**: CSS 放 `<head>`, JS 放 `<body>` 底部或用 async/defer

## JavaScript 引擎 (V8)

```
JS 源码
  ↓ Parser
AST (抽象语法树)
  ↓ Ignition (解释器)
Bytecode
  ↓ TurboFan (热点编译优化)
优化后的机器码
```

- **JIT (Just-In-Time)**：热点代码编译为机器码
- **Hidden Class**：V8 对结构相同的对象做优化（动态添删属性会破坏优化）
- **Garbage Collection**：分代 GC (Orinoco)，并行+增量减少停顿

## 事件循环 (Event Loop)

```javascript
// 浏览器的主线程循环
while (true) {
    执行宏任务 (MacroTask)  // script, setTimeout, I/O
    清空微任务队列 (MicroTask)  // Promise.then, MutationObserver
    if (需要渲染) {
        渲染 (requestAnimationFrame → Style → Layout → Paint)
    }
}
```

## 渲染优化

| 指标 | 含义 | 目标 |
|------|------|------|
| FCP (First Contentful Paint) | 首个有内容渲染 | <1.8s |
| LCP (Largest Contentful Paint) | 最大内容渲染 | <2.5s |
| TBT (Total Blocking Time) | 主线程阻塞时间 | <200ms |
| CLS (Cumulative Layout Shift) | 布局偏移 | <0.1 |
| INP (Interaction to Next Paint) | 交互延迟 | <200ms |

**Core Web Vitals** = LCP + INP + CLS

## 关系

- [[html-css]] — 解析为 DOM/CSSOM
- [[javascript]] — 主线程执行 JS
- [[http]] — 网络层加载资源
- [[tls-ssl]] — HTTPS 安全连接
