---
title: 软件测试
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [testing, programming, quality, devops]
sources: []
confidence: high
---

# 软件测试

## 定义

软件测试是验证软件是否**符合需求、发现缺陷、确保质量**的过程。它是软件工程的基石——不测试的代码就是不可信的代码。

## 测试金字塔

```
       ╱ E2E ╲         ← 少量，慢，脆弱
      ╱────────╲
     ╱Integration╲      ← 中量，验证组件交互
    ╱──────────────╲
   ╱ Unit Tests     ╲    ← 大量，快，稳定
  ╱──────────────────╲
```

### 单元测试 (Unit Test)
测试单个函数/方法：快速、隔离、稳定。

```python
def test_add():
    assert add(2, 3) == 5
```

### 集成测试 (Integration Test)
验证多个模块协同工作。

```python
def test_user_creation_flow():
    user = create_user("alice")
    db_user = db.get_user(user.id)
    assert db_user.name == "alice"
```

### 端到端测试 (E2E)
模拟真实用户操作整个系统。

```python
def test_checkout():
    browser.login("alice")
    browser.add_to_cart("book")
    browser.checkout()
    assert browser.text == "Order confirmed"
```

## 测试类型

| 类型 | 测什么 |
|------|--------|
| 功能测试 | 功能符合需求 |
| 性能测试 | 速度、并发 |
| 负载/压力测试 | 极限负载下行为 |
| 安全测试 | 漏洞、注入 |
| 回归测试 | 修改没破坏已有的 |
| 冒烟测试 (Smoke) | 基本功能是否可用 |
| 探索性测试 | 人工自由探索 |
| 突变测试 | 修改代码后测试是否发现 |

## 测试策略

| 策略 | 说明 |
|------|------|
| TDD (Test-Driven Development) | 红→绿→重构：先写测试，再写代码 |
| BDD (Behavior-Driven Development) | Given-When-Then 格式 |
| Property-based Testing | 自动生成随机输入验证性质 (QuickCheck, Hypothesis) |
| Snapshot Testing | 对比当前输出与保存的快照 (Jest) |

## Mock vs Stub vs Fake

| 概念 | 说明 |
|------|------|
| Dummy | 传进来但不用的对象 |
| Stub | 返回预设值 |
| Spy | 记录被如何调用 |
| Mock | 预设行为 + 验证交互 |
| Fake | 简化版真实实现（内存数据库） |

## 测试覆盖率

| 指标 | 含义 | 目标 |
|------|------|------|
| 行覆盖率 | 哪些代码行被执行 | >80% |
| 分支覆盖率 | 每个分支 (if/else) 都被覆盖 | >70% |
| 功能覆盖率 | 哪些需求被测试 | 100% |

> 100% 覆盖率 ≠ 没有 bug。覆盖率是必要的但不充分。

## 关系

- [[ci-cd]] — 测试是 CI/CD 的核心环节
- [[tdd]]
- [[object-oriented-programming]] — 好的 OOP 设计更容易测试
