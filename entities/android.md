---
title: Android
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [mobile, android, platform]
sources: []
confidence: high
---

# Android

## 概览

Android 是 Google 主导的**基于 [[linux]] 内核的开源移动操作系统**，2008 年首次发布。全球 ~70% 的智能手机运行 Android。架构分层清晰，从 Linux 内核到应用框架。

## 架构

```
┌── Applications ───────────────┐
│  System Apps + Third-Party    │
├── Java API Framework ─────────┤
│  Activity Manager, Content    │
│  Provider, View System, etc.  │
├── Android Runtime (ART) ──────┤
│  DEX bytecode, AOT + JIT      │
├── Native C/C++ Libraries ─────┤
│  OpenGL, SQLite, WebKit, etc. │
├── Hardware Abstraction Layer ─┤
│  Camera, Audio, Bluetooth HAL │
├── Linux Kernel ───────────────┤
│  Drivers, Memory, Process,    │
│  Power Management             │
└───────────────────────────────┘
```

## 关键组件

### Activity & 生命周期

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent { /* Compose UI */ }
    }
}
```

| 回调 | 触发 |
|------|------|
| onCreate | 创建 |
| onStart | 可见但不可交互 |
| onResume | 可交互（前台） |
| onPause | 部分遮挡 |
| onStop | 完全不可见 |
| onDestroy | 销毁 |

### Jetpack Compose

声明式 UI 框架（2021-），替代 XML + View 系统。

```kotlin
@Composable
fun Greeting(name: String) {
    Text("Hello $name!")
}
```

## Dalvik → ART

| 阶段 | 技术 | 说明 |
|------|------|------|
| Android 1-4 | Dalvik VM | JIT 编译 |
| Android 5+ | ART (Ahead-of-Time) | 安装时 AOT 编译 |
| Android 7+ | ART + JIT | 混合：AOT + profile-guided JIT |

## 开发工具

| 工具 | 用途 |
|------|------|
| Android Studio | 官方 IDE (IntelliJ 改造) |
| [[kotlin]] | 官方首选语言 |
| Gradle | 构建系统 |
| ADB | 调试桥接 |
| Firebase | Google 的移动后端 BaaS |

## iOS vs Android

| 维度 | Android | iOS |
|------|---------|-----|
| 语言 | Kotlin / Java | Swift / ObjC |
| IDE | Android Studio | Xcode |
| 市场 | Google Play | App Store |
| 碎片化 | 高（设备/版本繁多） | 低 |
| 审核 | 宽松 | 严格 |
| 收入 | 下载多、付费少 | 付费高 |

## 关系

- [[kotlin]]
- [[java]]
- [[linux]]
