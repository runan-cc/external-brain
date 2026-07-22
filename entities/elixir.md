---
title: Elixir
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [programming, elixir, functional, concurrency]
sources: []
confidence: high
---

# Elixir

## 概览

Elixir 是 José Valim 于 2011 年创建的**函数式、并发优先**的编程语言，运行在 Erlang VM (BEAM) 上。继承了 Erlang 的容错和并发模型，同时提供现代化的语法和工具链。

## 核心特性

| 特性 | 说明 |
|------|------|
| 函数式 | 不可变数据、模式匹配、管道 |
| Actor 并发 | 轻量进程（≠ OS 进程），百万级并发 |
| 容错 | "Let it crash" + Supervisor 树自动恢复 |
| OTP | 经过 30 年打磨的分布式设计框架 |
| 宏 | 编译时代码生成 |
| Phoenix | Web 框架之王，WebSocket 原生支持 |
| LiveView | 服务端渲染 + WebSocket 实时推送，写 SPA 不写 JS |

## Phoenix LiveView

```elixir
defmodule MyApp.CounterLive do
  use Phoenix.LiveView

  def mount(_params, _session, socket) do
    {:ok, assign(socket, count: 0)}
  end

  def render(assigns) do
    ~H"""
    <h1>Count: <%= @count %></h1>
    <button phx-click="inc">+1</button>
    """
  end

  def handle_event("inc", _params, socket) do
    {:noreply, update(socket, :count, &(&1 + 1))}
  end
end
```

无需 JS 框架即可实现实时交互——状态全在服务端，通过 WebSocket 同步 DOM diff。

## BEAM VM 并发模型

```
OS Process
  └── BEAM VM
       ├── Lightweight Process 1  (few KB)
       ├── Lightweight Process 2
       ├── Lightweight Process 3
       └── ... (轻松百万个)

每个 process 独立 GC、独立 crash、通过消息通信
无共享状态 → 无锁 → 无死锁
```

## 适用场景

| 场景 | 说明 |
|------|------|
| 高并发 WebSockets | Discord 从 Go 迁到 Elixir |
| 实时应用 | 聊天、直播、协作编辑 |
| 分布式系统 | OTP 自带分布式原语 |
| API 服务 | Phoenix 的 JSON API |
| 嵌入式/IoT | Nerves 框架 |

## Erlang vs Elixir

| 维度 | Erlang | Elixir |
|------|--------|--------|
| 语法 | Prolog 风格，陡峭 | Ruby 风格，友好 |
| 工具链 | rebar3 | Mix + Hex |
| 生态 | 电信、数据库 | Web、创业公司 |
| 社区增长 | 稳定 | ✅ 快速增长 |

## 关系

- [[functional-programming]]
- [[concurrent-programming]] — Actor 模型
- [[distributed-systems]] — BEAM 天生为分布式设计
