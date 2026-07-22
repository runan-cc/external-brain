---
title: TDD (Test-Driven Development)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [testing, methodology, programming]
sources: []
confidence: high
---

# TDD (Test-Driven Development)

## 定义

TDD 是由 Kent Beck 于 2003 年推广的软件开发方法论，核心是**在写代码之前先写测试**。它不仅是测试技术，更是一种设计方法。

## 三步循环

```
┌──→ RED （写一个失败的测试）
│         ↓
│    GREEN （写最少代码让测试通过）
│         ↓
└── REFACTOR （重构代码，保持测试通过）
```

## 规则

1. **只写一个失败的测试**
2. **只写刚好让测试通过的代码**（哪怕很蠢）
3. **测试通过后立刻重构**

## 示例

```python
# 1. RED：先写测试
def test_fizzbuzz_3_returns_fizz():
    assert fizzbuzz(3) == "Fizz"

# 2. GREEN：写最简代码
def fizzbuzz(n):
    return "Fizz"  # 够让测试通过了

# 3. 继续加测试
def test_fizzbuzz_1_returns_1():
    assert fizzbuzz(1) == "1"

# 4. GREEN：扩展代码
def fizzbuzz(n):
    if n == 3:
        return "Fizz"
    return str(n)

# 5. REFACTOR：模式出现后重构
def fizzbuzz(n):
    if n % 3 == 0:
        return "Fizz"
    return str(n)
```

## 好处

| 好处 | 说明 |
|------|------|
| 设计驱动 | 测试先写 → API 从使用者角度设计 |
| 快速反馈 | 几秒内知道是否破坏了什么 |
| 安全重构 | 重构后跑测试 = 即刻验证 |
| 活文档 | 测试 = 可执行的规格说明 |
| 减少调试 | 小步前进，bug 范围极小 |

## 常见误解

| 误解 | 实际 |
|------|------|
| "TDD 慢" | 减少调试和返工，总体更快 |
| "100% TDD" | Kent Beck 本人也说不是 100% |
| "TDD = 测试活动" | TDD 是**设计方法**，测试是副产品 |
| "不用写设计文档了" | TDD 补充而非替代设计 |

## 何时不用 TDD

- 探索性编程/原型（需求不确定）
- UI 布局代码（测试困难、变化快）
- 一次性脚本
- 遗留代码（先加特征测试，再重构）

## 关系

- [[software-testing]]
- [[ci-cd]]
- [[object-oriented-programming]]
