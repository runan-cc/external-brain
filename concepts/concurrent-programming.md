---
title: 并发编程
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [concurrency, programming, systems, performance]
sources: []
confidence: high
---

# 并发编程

## 定义

并发编程是**同时处理多个任务**的技术。它不一定是并行（同时执行），而是将任务交错执行以提升吞吐量和响应性。是多核时代的核心编程挑战。

## 并发 vs 并行

| 概念 | 定义 |
|------|------|
| **并发 (Concurrency)** | 多个任务在**同一时间段**内推进（可能交替执行） |
| **并行 (Parallelism)** | 多个任务在**同一时刻**真正同时执行（需多核） |

单核也可以并发，但不能并行。

## 线程与同步

### 竞态条件 (Race Condition)
多线程访问共享数据，结果取决于执行顺序。

```cpp
// 竞态！两个线程同时 x++
// 可能是 2 而非期望的 3
int x = 1;
thread1: x++;  // 读 x=1 → 加 1 → 写 2
thread2: x++;  // 读 x=1 → 加 1 → 写 2  （读到了旧值）
```

### 互斥锁 (Mutex)
确保只有一个线程访问临界区。

```python
lock = threading.Lock()
with lock:
    x += 1  # 原子化
```

代价：阻塞、死锁风险、上下文切换开销。

### 信号量 (Semaphore)
限制同时访问资源的线程数（Mutex 是 count=1 的特例）。

## 死锁 (Deadlock)

**四个必要条件（Coffman 条件）：**
1. **互斥**：资源不能同时共享
2. **持有等待**：持有资源 + 等待其他资源
3. **非抢占**：不能强行夺走其他线程的资源
4. **循环等待**：线程 A 等 B 释放，B 等 A 释放

**预防策略：**
- 统一加锁顺序
- 锁超时 (try_lock)
- 死锁检测 + 回滚

## 高级同步原语

| 原语 | 说明 |
|------|------|
| Read-Write Lock | 多读单写，提高并发读性能 |
| Condition Variable | 线程等待直到条件满足（生产者-消费者） |
| Barrier | N 个线程都到达后才继续 |
| Spinlock | 忙等待（短临界区时优于 Mutex） |

## 无锁编程 (Lock-Free)

| 技术 | 说明 |
|------|------|
| CAS (Compare-And-Swap) | 原子操作：`if *addr == old { *addr = new; return true }` |
| Atomic 变量 | 硬件保证的原子读写 |
| Memory Ordering | Relaxed, Acquire, Release, SeqCst |
| ABA 问题 | CAS 的经典陷阱（指针被回收重用） |

## 并发模型

| 模型 | 代表 | 特点 |
|------|------|------|
| 线程 + 共享内存 (Lock) | C/C++/Java | 灵活但容易出错 |
| 消息传递 (Actor) | Erlang, Akka | 无共享状态，天生安全 |
| CSP (Channel) | [[go]] | goroutine + channel |
| async/await | JS, [[python]], [[rust]] | 单线程事件循环 |
| STM (Software Transactional Memory) | Clojure, Haskell | 事务式并发 |

## 关系

- [[operating-system]] — 进程/线程调度
- [[rust]] — 类型系统保证并发安全
- [[go]] — goroutine + channel 模型
