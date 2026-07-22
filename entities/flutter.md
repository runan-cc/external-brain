---
title: Flutter
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [framework, mobile, flutter, dart]
sources: []
confidence: high
---

# Flutter

## 概览

Flutter 是 Google 于 2018 年发布的**跨平台 UI 框架**，使用 Dart 语言，以自绘引擎著称。一套代码运行在 iOS、Android、Web 和桌面——且性能和原生体验非常接近。

## 核心理念

> Everything is a Widget

Flutter 不使用原生控件，而是用自己的**Skia/Impeller 渲染引擎**直接在 Canvas 上绘制一切。这避免了跨平台框架常见的"最小公分母"问题。

## 架构

```
┌── Dart Framework ────────────┐
│  Material / Cupertino        │
│  Widgets, Rendering          │
├── Engine (C++) ──────────────┤
│  Impeller (渲染), Dart VM,   │
│  Text, Accessibility         │
├── Embedder ──────────────────┤
│  Platform-specific: Android  │
│  Surface, iOS, Windows, etc. │
└──────────────────────────────┘
```

## Widget 三件套

| 概念 | 说明 |
|------|------|
| Widget | 不可变配置（轻量） |
| Element | Widget 的实例化，管理生命周期 |
| RenderObject | 实际负责布局和绘制 |

## 示例

```dart
class CounterPage extends StatefulWidget {
  @override
  State<CounterPage> createState() => _CounterPageState();
}

class _CounterPageState extends State<CounterPage> {
  int _count = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Counter')),
      body: Center(child: Text('$_count', style: TextStyle(fontSize: 48))),
      floatingActionButton: FloatingActionButton(
        onPressed: () => setState(() => _count++),
        child: Icon(Icons.add),
      ),
    );
  }
}
```

## Flutter vs React Native

| 维度 | Flutter | React Native |
|------|---------|--------------|
| 渲染 | 自绘引擎 (Impeller) | 桥接原生控件 |
| 性能 | 接近原生 | 用桥(需优化) |
| UI 一致性 | ✅ 100% 跨平台统一 | 可能有平台差异 |
| 热重载 | ✅ 极快 | ✅ 快 |
| 原生交互感 | "像原生" | "是原生" |
| 语言 | Dart | JS/TS |
| 生态成熟度 | 中 | ✅ 高 |
| Web | 有 (Canvas/HTML) | 需 react-native-web |

## 状态管理

| 方案 | 特点 |
|------|------|
| setState | 最简单，小项目 |
| Provider | Google 推荐，轻量 |
| Riverpod | Provider 的现代化替 |
| BLoC | 事件驱动，企业级 |
| GetX | 全功能但争议大 |

## Dart 语言

- AOT 编译（iOS 等发布模式）→ 快速启动
- JIT 编译（开发模式）→ 热重载
- Null Safety、类型系统、async/await

## 关系

- [[android]] / [[ios]] — Flutter 目标平台
- [[react]] — 跨平台竞品
- [[swift]] / [[kotlin]] — 原生开发对比
