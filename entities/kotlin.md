---
title: Kotlin
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [programming, kotlin, android, jvm]
sources: []
confidence: high
---

# Kotlin

## 概览

Kotlin 是 JetBrains 于 2011 年发布的**现代 JVM 语言**，2017 年被 Google 宣布为 Android 官方开发语言。100% 与 [[java]] 互操作，同时引入了大量现代语言特性。

## 核心特性

| 特性 | 说明 |
|------|------|
| Null Safety | 类型系统区分 `String` 和 `String?`，编译期防 NPE |
| 数据类 | `data class` 自动生成 equals/hashCode/toString/copy |
| 扩展函数 | 给已有类添加方法，不改源码 |
| 协程 (Coroutines) | 结构化并发，比线程轻量得多 |
| 类型推断 | `val x = 42` 自动推断 Int |
| 一等公民的函数 | 高阶函数、Lambda、内联 |
| 属性 | 替代 Java 的 getter/setter 样板 |
| Smart Cast | `if (x is String) x.length` 自动转型 |

## 与 Java 对比

```kotlin
// Kotlin
data class User(val name: String, val age: Int)
val adults = users.filter { it.age >= 18 }
val name: String? = map["name"]  // 可能为 null

// Java
class User { ... 30 行 getter/setter/equals/hashCode }
List<User> adults = users.stream().filter(u -> u.getAge() >= 18).collect(...);
String name = map.get("name");  // 忘了 null 检查 → NPE 💥
```

## 协程 vs 线程

```kotlin
// 协程：轻量级，可以同时启动数千个
suspend fun fetchUser(id: String): User = withContext(Dispatchers.IO) {
    api.getUser(id)
}

// 并发多个请求
val users = coroutineScope {
    val u1 = async { fetchUser("1") }
    val u2 = async { fetchUser("2") }
    u1.await() to u2.await()
}
```

## 多平台 (KMP)

Kotlin Multiplatform：共享业务逻辑代码（iOS + Android + Web + Server），非跨平台 UI。

## 关系

- [[java]] — JVM 生态完全互通
- [[android]] — Android 官方首选语言
- [[functional-programming]] — Kotlin 的函数式特性
