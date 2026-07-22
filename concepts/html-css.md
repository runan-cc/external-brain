---
title: HTML & CSS
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [web, html, css, frontend]
sources: []
confidence: high
---

# HTML & CSS

## 定义

HTML (HyperText Markup Language) 定义网页的**结构和语义**，CSS (Cascading Style Sheets) 定义网页的**外观和布局**。两者 + [[javascript]] 构成 Web 三大技术基石。

## HTML 核心

### 文档结构
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Page Title</title>
</head>
<body>
    <!-- 内容 -->
</body>
</html>
```

### 语义化标签
| 标签 | 用途 |
|------|------|
| `<header>` `<nav>` `<main>` `<footer>` | 页面分区 |
| `<article>` `<section>` `<aside>` | 内容分组 |
| `<h1>-<h6>` | 标题层次 |
| `<p>` `<ul>` `<ol>` `<li>` | 文本和列表 |
| `<a>` | 超链接 |
| `<img>` | 图片 |
| `<form>` `<input>` | 表单 |
| `<table>` | 表格 |
| `<canvas>` | 位图绘制 |

### SEO 和可访问性
- **`<title>`** 和 **`<meta description>`** 影响搜索引擎
- **`alt` 属性**：图片替代文本（无障碍）
- **ARIA 标签**：增强屏幕阅读器支持
- **语义化标签 > `<div>` 堆砌**

## CSS 核心

### 选择器
```css
/* 元素 */ p { }
/* 类 */   .class { }
/* ID */   #id { }
/* 属性 */ [type="text"] { }
/* 伪类 */ a:hover { }
/* 组合 */ .parent > .child { }
```

### 盒模型
```
┌── margin ───────────────┐
│  ┌── border ──────────┐ │
│  │  ┌── padding ────┐ │ │
│  │  │   content     │ │ │
│  │  └───────────────┘ │ │
│  └────────────────────┘ │
└─────────────────────────┘
```

`box-sizing: border-box` 让 width 包含 padding+border（推荐）。

### 布局技术

| 技术 | 特点 |
|------|------|
| Flexbox | 一维布局（行 或 列），内容对齐 |
| Grid | 二维布局（行+列），页面级 |
| Position | absolute/relative/fixed/sticky |
| Float | 历史遗留，已被 Flexbox/Grid 取代 |
| Media Query | 响应式设计 `@media (max-width: 768px)` |

### 层叠与优先级

优先级 (Specificity)：`!important` > 行内 style > `#id` > `.class` > `tag` > `*`

## 现代 CSS 趋势

- **Tailwind CSS**：实用优先（utility-first），`class="flex items-center gap-4"`
- **CSS-in-JS**：Styled Components / CSS Modules
- **CSS Variables**：`--primary: #333; color: var(--primary);`
- **Container Queries**：基于父容器大小而非视口

## CSS 常见痛点

| 痛点 | 方案 |
|------|------|
| 垂直居中 | Flexbox: `align-items: center` |
| 响应式 | Media Query / Container Query |
| 浏览器兼容 | PostCSS + Autoprefixer |
| CSS 冗余 | Tailwind / CSS Modules / Scoped CSS |

## 关系

- [[javascript]] — JS 操控 DOM 和 CSS
- [[react]] — JSX 混合 HTML + JS
- [[http]] — HTML/CSS/JS 通过 HTTP 传输
