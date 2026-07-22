---
title: Character Encoding (字符编码)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [encoding, unicode, text, fundamentals]
sources: []
confidence: high
---

# Character Encoding (字符编码)

## 定义

字符编码是将**人类可读的字符映射为字节序列**的标准。不理解字符编码，"乱码"就是你最常遇到的问题。

## 从 ASCII 到 Unicode

### ASCII (1963)
7 位编码，128 个字符：英文大小写 + 数字 + 符号 + 控制字符。
- `'A'` = 65 (0x41), `'a'` = 97 (0x61), `'0'` = 48 (0x30)

### 扩展 ASCII 混乱期
各国用 128-255 区域编码自己的字符：
- Latin-1 (ISO-8859-1): 西欧语言
- GB2312/GBK: 中文
- Shift-JIS: 日文
- **同一字节在不同编码下是不同字符 → 乱码根源**

### Unicode (1991)
统一字符集——一个字符一个码点 (Code Point)。
- `A` = U+0041, `中` = U+4E2D, `😀` = U+1F600
- 目前 15 万个字符，17 个平面 (Plane)
- BMP (基本多语言平面) = U+0000 到 U+FFFF (常用字符)

## UTF-8 vs UTF-16 vs UTF-32

| 编码 | 最小单位 | ASCII 兼容 | 空间效率 (英文) | 空间效率 (中文) |
|------|----------|-----------|---------------|---------------|
| UTF-8 | 1 字节 | ✅ | 1 字节/字符 | 3 字节/字符 |
| UTF-16 | 2 字节 | ❌ | 2 字节/字符 | 2 字节/字符 (BMP) |
| UTF-32 | 4 字节 | ❌ | 4 字节/字符 | 4 字节/字符 |

### UTF-8 编码规则

```
U+0000 - U+007F   → 0xxxxxxx                      (1 byte)
U+0080 - U+07FF   → 110xxxxx 10xxxxxx              (2 bytes)
U+0800 - U+FFFF   → 1110xxxx 10xxxxxx 10xxxxxx     (3 bytes)
U+10000 - U+10FFFF → 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx (4 bytes)
```

| 字符 | Unicode | UTF-8 字节 |
|------|---------|-----------|
| A | U+0041 | `0x41` |
| é | U+00E9 | `0xC3 0xA9` |
| 中 | U+4E2D | `0xE4 0xB8 0xAD` |
| 😀 | U+1F600 | `0xF0 0x9F 0x98 0x80` |

## BOM (Byte Order Mark)

`U+FEFF` 放在文件开头标识字节序：
- UTF-8: `EF BB BF`（可选，Linux/Unix 不推荐）
- UTF-16 LE: `FF FE` | UTF-16 BE: `FE FF`

> ⚠️ Windows 记事本保存 UTF-8 会加 BOM → shell 脚本 `#!/bin/bash` 变 `﻿#!/bin/bash` → 错误

## 常见问题

| 问题 | 原因 | 解决 |
|------|------|------|
| 锟斤拷 | GBK 解码 UTF-8 的连续 0xE4 0xB8 0xAD | 统一用 UTF-8 |
| � (U+FFFD) | 字节序列在当前编码中无效 → 替换字符 | 同上 |
| 烫烫烫 | Visual Studio 调试器的未初始化内存填充 `0xCC` | 初始化变量 |

## Base64

将二进制数据编码为可打印的 ASCII 字符（A-Z, a-z, 0-9, +, /, =）。

```
3 bytes → 4 Base64 characters
Man → TWFu
```

用途：Email 附件 (MIME)、Data URL (`data:image/png;base64,...`)、JWT、HTTP Basic Auth

## 实践建议

- **UTF-8 everywhere**：文件、数据库、API、日志
- 编辑器设置默认 UTF-8 without BOM
- 数据库连接指定 `charset=utf8mb4`（MySQL 的完整 Unicode）

## 关系

- [[computational-complexity]] — 编码的底层基础
- [[http]] — Content-Type charset
- [[sql]] — 数据库字符集
