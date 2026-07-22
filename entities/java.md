---
title: Java
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [java, language, programming, enterprise]
sources: []
confidence: high
---

# Java

## 概览

Java 是 Sun Microsystems 于 1995 年发布的**面向对象编程语言**，以"一次编写，到处运行"（JVM）著称。是企业级应用、Android 开发和大数据基础设施的核心语言。

## 核心特性

- **JVM（Java Virtual Machine）**：字节码运行在 JVM 上，跨平台
- **自动垃圾回收**：无需手动内存管理
- **强类型 + OOP**：严格的类型系统和类继承
- **丰富的生态**：Spring, Maven/Gradle, JUnit
- **JIT 编译**：热点代码编译为本地机器码

## 生态

| 领域 | 框架/工具 |
|------|-----------|
| Web 后端 | Spring Boot, Quarkus, Micronaut |
| 大数据 | Hadoop, Spark, Flink, Kafka |
| Android | Android SDK (Kotlin 逐渐取代) |
| 构建工具 | Maven, Gradle |
| ORM | Hibernate, MyBatis |

## Java vs Kotlin

| 维度 | Java | Kotlin |
|------|------|--------|
| Null 安全 | 无（NullPointerException） | 编译时检查 |
| 语法简洁性 | 啰嗦 | 简洁 |
| Android | 传统选择 | 官方推荐 |
| 协程 | Loom (Java 21+) | 内置协程 |

## 关系

- [[kotlin]] — JVM 生态的现代替代
- [[scala]] — JVM 上的函数式编程
- [[spring-boot]] — 最流行的 Java Web 框架
