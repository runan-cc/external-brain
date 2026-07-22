---
title: Zig
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [programming, zig, systems]
sources: []
confidence: high
---

# Zig

## 概览

Zig 是 Andrew Kelley 于 2016 年创建的**系统级编程语言**，定位为"更好的 C"——保留 C 的简洁和控制力，同时加入现代安全特性和优秀的编译工具链。核心哲学：**无隐藏控制流、无隐藏分配、无预处理器、无宏**。

## 与 C 的关系

| 维度 | [[c-language]] | Zig |
|------|---------------|-----|
| 标准库 | libc（系统依赖） | 自备标准库（跨平台） |
| 编译 | 需要 Make/CMake | Zig Build System |
| 交叉编译 | 痛苦 | 原生支持，一条命令 |
| 内存安全 | 无 | Debug 模式检查 UAF/OOB |
| 错误处理 | errno / return -1 | Error Union + try/catch |
| 泛型 | 宏 / void* | comptime（编译时求值） |

## 核心特性

### comptime（编译时计算）

```zig
fn List(comptime T: type) type {
    return struct {
        items: []T,
        fn add(self: *@This(), item: T) void { ... }
    };
}

const IntList = List(i32);  // 在编译时生成类型
```

比 C 模板和 C++ 模板更直观——就是用 Zig 写编译时代码。

### 无隐藏分配

```zig
// Zig 中所有分配都显式传入 allocator
var list = std.ArrayList(u8).init(allocator);
defer list.deinit();
```

没有隐式 malloc——你能看清每一处内存分配。

### 错误处理

```zig
fn openFile(path: []const u8) !File {
    const file = try std.fs.cwd().openFile(path, .{});
    return file;
}
```

`try` 语法糖：如果是错误则向上传播。没有异常机制的运行时开销。

### C ABI 互操作

```zig
const c = @cImport({
    @cInclude("stdio.h");
    @cInclude("sqlite3.h");
});
```

直接 `#include` C 头文件，zig 编译器能内置解析。

### Zig 作为 C 编译器

Zig 自带完整的 C 交叉编译器：
```bash
zig cc -target x86_64-linux-musl main.c -o main
```

一条命令交叉编译到任何平台。

## Zig vs Rust

| 维度 | [[rust]] | Zig |
|------|----------|-----|
| 内存安全 | ✅ 编译期保证 | Debug 模式检查（Release 不保证） |
| 学习曲线 | 陡峭（所有权/借用） | 平缓（接近 C） |
| 编译速度 | 慢 | ✅ 快 |
| 泛型 | Trait + Generics | comptime |
| 适合 | 需要极致安全的系统 | C 的替代品 |
| 哲学 | 安全第一 | 简单第一 |

## 适合场景

- C 库的替代实现（Bun, TigerBeetle）
- 操作系统/内核开发
- 游戏引擎底层
- WASM 编译目标

## 关系

- [[c-language]]
- [[rust]]
- [[webassembly]]
