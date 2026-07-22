---
title: Regular Expressions
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [tool, programming, text]
sources: []
confidence: high
---

# Regular Expressions (正则表达式)

## 定义

正则表达式是一种描述**字符串模式**的形式语言，用于搜索、匹配和替换文本。几乎所有编程语言和 CLI 工具都内置支持。

## 基础语法

| 模式 | 含义 | 示例 |
|------|------|------|
| `.` | 任意字符 | `h.t` → hat, hot, hit |
| `*` | 0+ 次 | `ab*c` → ac, abc, abbc |
| `+` | 1+ 次 | `ab+c` → abc, abbc |
| `?` | 0 或 1 次 | `colou?r` → color, colour |
| `{n,m}` | n 到 m 次 | `a{2,4}` → aa, aaa, aaaa |
| `^` | 行首 | `^Hello` |
| `$` | 行尾 | `world$` |
| `[]` | 字符类 | `[aeiou]` → 任意元音 |
| `[^]` | 否定字符类 | `[^0-9]` → 非数字 |
| `|` | 或 | `cat|dog` |
| `()` | 捕获组 | `(ab)+` |
| `\d` | 数字 | `[0-9]` |
| `\w` | 单词字符 | `[a-zA-Z0-9_]` |
| `\s` | 空白 | 空格、Tab、换行 |
| `\b` | 单词边界 | `\bcat\b` → cat 但不包含 scatter |

## 实战示例

```regex
# Email
[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}

# 中国手机号
1[3-9]\d{9}

# URL
https?://[^\s/$.?#].[^\s]*

# IP 地址
\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}

# 提取中文
[\u4e00-\u9fff]+
```

## 引擎类型

| 类型 | 特点 | 代表 |
|------|------|------|
| DFA | 线性时间，无回溯 | awk, grep |
| NFA (传统) | 有回溯，支持更多特性 | PCRE, JS, Python |
| NFA (POSIX) | 最长匹配 | POSIX |

**警惕灾难性回溯 (Catastrophic Backtracking)**

```regex
# 坏正则（嵌套量词）
(a+)+b  # 匹配 "aaaaaaaaac" 可能需要数小时
```

## 相关概念

- [[python]] — `re` 模块
- [[javascript]] — `/pattern/flags`
- [[grep]] — 命令行搜索
