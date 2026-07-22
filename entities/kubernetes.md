---
title: Kubernetes (k8s)
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [kubernetes, devops, container, orchestration]
sources: []
confidence: high
---

# Kubernetes (k8s)

## 概览

Kubernetes（k8s）是 Google 于 2014 年开源的**容器编排平台**。它自动化了 [[docker]] 容器的部署、扩缩容、负载均衡和自愈。目前是云原生生态的事实标准。

## 核心概念

| 概念 | 说明 |
|------|------|
| Pod | 最小部署单元，包含一个或多个容器 |
| Service | 为 Pod 提供稳定的网络入口和负载均衡 |
| Deployment | 声明式管理 Pod 的期望状态（副本数、滚动更新） |
| ConfigMap / Secret | 配置和密钥管理 |
| Ingress | HTTP/HTTPS 流量路由到 Service |
| PVC (PersistentVolumeClaim) | 持久化存储请求 |

## 架构

```
Control Plane (Master)
├── API Server    ← 一切操作的入口
├── etcd          ← 分布式 KV 存储（集群状态）
├── Scheduler     ← 决定 Pod 放在哪个 Node
└── Controller    ← 维持期望状态

Worker Node
├── kubelet       ← 管理 Pod 的 agent
├── kube-proxy    ← 网络规则
└── Container Runtime (containerd/CRI-O)
```

## 为什么用 k8s

- **自动扩缩**：HPA（水平自动扩缩）根据 CPU/内存/自定义指标扩容
- **自愈**：容器挂了自动重启，Node 故障自动迁移 Pod
- **滚动更新**：零停机部署，失败自动回滚
- **服务发现**：内置 DNS + Service 抽象
- **声明式基础设施**：YAML 描述期望状态，k8s 保证实现

## 局限

- **复杂度高**：学习曲线陡峭，运维成本大
- **资源开销**：Control Plane 本身消耗不少资源
- **过度使用**：小项目可能不需要 k8s（Docker Compose 更合适）
- **网络/存储**：需要额外插件（CNI, CSI）

## 关系

- [[docker]] — 最常用的容器运行时
- [[linux]] — k8s 运行的操作系统
- [[ci-cd]] — GitOps + ArgoCD

## 相关概念

- [[docker-compose-vs-kubernetes]] — 轻量编排 vs 企业级编排
