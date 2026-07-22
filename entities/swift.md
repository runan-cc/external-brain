---
title: Swift
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [programming, swift, apple, ios]
sources: []
confidence: high
---

# Swift

## 概览

Swift 是 Apple 于 2014 年发布的**现代编译型语言**，用于替代 Objective-C 成为 Apple 平台（iOS、macOS、watchOS、visionOS）的主力语言。2015 年开源，如今也用于服务端。

## 核心特性

| 特性 | 说明 |
|------|------|
| 类型安全 | 编译期类型检查，Optionals 防空指针 |
| ARC (自动引用计数) | 编译期插入内存管理代码，无 GC 停顿 |
| 值类型优先 | struct 和 enum 是值类型，默认不可变 |
| 协议导向编程 | Protocol + Extension 优于 Class 继承 |
| 函数式支持 | map/filter/reduce、闭包、一等函数 |
| Result Builder | DSL 构建（SwiftUI 的基础） |
| async/await | Swift 5.5 内置结构化并发 |
| Ownership (5.9+) | 类似 [[rust]] 的所有权特性 |

## SwiftUI

```swift
struct ContentView: View {
    @State private var count = 0

    var body: some View {
        VStack {
            Text("Count: \(count)")
                .font(.largeTitle)
            Button("Tap me!") { count += 1 }
        }
    }
}
```

声明式 UI 框架，Apple 平台的未来方向（替代 UIKit/AppKit）。

## 与 Rust 的对比

| 维度 | Swift | [[rust]] |
|------|-------|----------|
| 内存安全 | ARC + 编译检查 | 所有权 + 借用检查 |
| 学习曲线 | 中 | 高 |
| 生态系统 | Apple 生态 | 系统编程、WASM |
| 服务端 | Vapor 框架 | 高速增长 |
| 互操作 | 与 ObjC/[[cpp]] 无缝 | C FFI |

## 服务端 Swift

Vapor 框架让 Swift 进入服务端领域。优势：Apple 生态内统一的语言栈。

## 关系

- [[rust]] — 内存安全的两种不同路径
- [[cpp]] — Swift 的 C++ 互操作 (Swift 5.9+)
