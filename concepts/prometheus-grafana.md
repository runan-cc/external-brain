---
title: Prometheus & Grafana
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [monitoring, devops, observability]
sources: []
confidence: high
---

# Prometheus & Grafana

## Prometheus

Prometheus 是 SoundCloud 于 2012 年创建的**开源监控和告警系统**，2016 年加入 CNCF，已成为云原生监控的事实标准。

### 核心理念

| 特点 | 说明 |
|------|------|
| **Pull 模型** | Prometheus 主动抓取 metrics（不依赖推送） |
| **多维数据模型** | Metric + Labels（时间序列 + 标签） |
| **PromQL** | 强大的查询语言 |
| **不依赖外部存储** | 本地 TSDB，适合短期数据 |
| **服务发现** | 自动发现 k8s/Consul/DNS 中的目标 |

### 数据模型

```
http_requests_total{method="GET", status="200", endpoint="/api"}
                    ↑ metric name                        ↑ labels
```

### 四大指标类型

| 类型 | 适用 |
|------|------|
| Counter | 只增不减：请求数、错误数 |
| Gauge | 可增减：内存、CPU、温度 |
| Histogram | 分布统计：请求延迟分桶 |
| Summary | 客户端分位数 |

### 架构

```
Short-lived Jobs
     ↓ push
Pushgateway ← pull ← Prometheus Server → 告警 → Alertmanager → PagerDuty/Email
                       ↓                         ↑
                    local TSDB                 Grafana
```

## Grafana

Grafana 是**可视化平台**——从 Prometheus、InfluxDB、Elasticsearch、PostgreSQL 等数据源创建仪表板和图表。

### 关键功能

| 功能 | 说明 |
|------|------|
| Dashboard | 拖拽式面板组合（Graph, Stat, Table, Heatmap） |
| Variables | 模板变量，动态切换数据范围 |
| Alerting | Grafana 内置告警（替代 Alertmanager） |
| Explore | 即时查询和数据探索 |
| Transformations | 数据变换和聚合 |

## 黄金信号（Four Golden Signals）

| 信号 | 指标 |
|------|------|
| **Latency** | 请求响应时间（P50/P95/P99） |
| **Traffic** | 请求量（QPS/RPS） |
| **Errors** | 错误率（5xx/连接失败） |
| **Saturation** | 饱和程度（CPU/内存/连接数） |

## RED vs USE

| 方法 | 适用 | 指标 |
|------|------|------|
| RED | 服务端 | Rate, Errors, Duration |
| USE | 资源端 | Utilization, Saturation, Errors |

## SLI / SLO / SLA

| 缩写 | 含义 | 示例 |
|------|------|------|
| SLI | 服务水平指标 | P99 延迟 < 200ms |
| SLO | 服务水平目标 | 99.9% 请求满足 SLI |
| SLA | 服务水平协议 | 低于 SLO 退钱 |

> 错误预算 (Error Budget) = 100% − SLO。用来决策"能不能接着发布"。

## 关系

- [[kubernetes]] — Prometheus 是 k8s 标准监控方案
- [[ci-cd]] — 监控是持续运维的闭环
