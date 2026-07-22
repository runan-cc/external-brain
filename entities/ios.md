---
title: iOS
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [mobile, ios, apple, swift]
sources: []
confidence: high
---

# iOS

## 概览

iOS 是 Apple 的**移动操作系统**，2007 年随初代 iPhone 发布。基于 Darwin (XNU 内核)，是世界上最封闭也是最具盈利能力的移动平台。

## 架构

```
┌── Cocoa Touch ───────────────┐
│  UIKit, SwiftUI, Foundation  │
├── Media ─────────────────────┤
│  Core Graphics, Core         │
│  Animation, AVFoundation     │
├── Core Services ─────────────┤
│  Core Data, CloudKit,        │
│  StoreKit, Core Location     │
├── Core OS ───────────────────┤
│  Security, libSystem,        │
│  Accelerate, Metal           │
├── Kernel (XNU) ──────────────┤
│  Mach + BSD + IOKit          │
└──────────────────────────────┘
```

## 开发生态

| 组件 | 说明 |
|------|------|
| [[swift]] | 主力语言 |
| SwiftUI | 声明式 UI (2019+) |
| UIKit | 传统 UI 框架 |
| Xcode | 唯一官方 IDE |
| Swift Package Manager | 包管理 |
| TestFlight | 内测分发 |
| App Store Connect | 发布管理 |

## iOS 关键技术

### ARC (自动引用计数)
编译时插入 retain/release，无 GC。注意循环引用（用 weak/unowned 打破）。

### GCD (Grand Central Dispatch)
```swift
DispatchQueue.global().async {
    let data = loadData()
    DispatchQueue.main.async {
        updateUI(data)
    }
}
```

### Swift Concurrency (async/await)
```swift
func fetchUser() async throws -> User {
    let (data, _) = try await URLSession.shared.data(from: url)
    return try JSONDecoder().decode(User.self, from: data)
}
```

### SwiftData
Core Data 的 Swift 原生替代（2023+），持久化框架。

## App Store

| 规则 | 影响 |
|------|------|
| 沙盒 (Sandbox) | 每个 App 隔离运行 |
| 审核 (Review) | 人工+自动审核 |
| 30% 抽成 | IAP 必须走 App Store |
| 签名 (Signing) | 证书+Provisioning Profile |
| 隐私标签 | 必须声明数据收集 |

## 关系

- [[swift]]
- [[linux]] — Darwin 内核来自 NeXTSTEP/BSD/Mach
- [[android]] — 最大的竞争对手
