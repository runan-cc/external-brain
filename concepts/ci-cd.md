---
title: CI/CD
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [ci-cd, devops, automation, testing]
sources: []
confidence: high
---

# CI/CD（持续集成/持续部署）

## 定义

CI/CD 是一组软件开发实践：
- **CI（持续集成）**：代码频繁合并到主干，自动构建和测试
- **CD（持续交付/部署）**：自动将通过测试的代码发布到生产环境

## 典型 Pipeline

```
代码提交 → Build → Test → Security Scan → Staging → Approval → Production
   ↑                                                                    |
   └──────────────────── 问题反馈 ──────────────────────────────────────┘
```

## 常用工具

| 工具 | 类型 | 特点 |
|------|------|------|
| GitHub Actions | SaaS | GitHub 原生，免费额度友好 |
| GitLab CI | SaaS/自托管 | GitLab 深度集成 |
| Jenkins | 自托管 | 老牌，高度可定制 |
| CircleCI | SaaS | 构建速度快 |
| ArgoCD | Kubernetes | GitOps 部署 |

## 关键实践

- **基础设施即代码（IaC）**：Pipeline 配置写入代码仓库
- **GitOps**：Git 作为唯一真实源，自动同步到基础设施
- **Feature Flag**：部署与上线解耦
- **Canary / Blue-Green 部署**：零停机升级
- **回滚策略**：失败时自动回滚到上一版本

## 相关概念

- [[git]] — CI/CD 的触发源
- [[docker]] — 构建环境标准化
- [[kubernetes]] — 部署目标
