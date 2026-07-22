---
title: Git
created: 2026-07-22
updated: 2026-07-22
type: entity
tags: [tool, cli, devops]
sources: []
confidence: high
---

# Git

## 概览

Git 是 Linus Torvalds 于 2005 年创建的**分布式版本控制系统**。它是现代软件开发的基础设施，几乎所有的代码协作都基于 Git。

## 核心概念

| 概念 | 说明 |
|------|------|
| Repository | 代码仓库，包含完整历史 |
| Commit | 一次代码快照，有唯一 SHA 标识 |
| Branch | 独立的开发线，支持并行工作 |
| Remote | 远程仓库（GitHub, GitLab 等） |
| Staging Area | 暂存区，提交前的检查站 |

## 关键命令

```bash
git init          # 初始化仓库
git clone <url>   # 克隆远程仓库
git add <file>    # 添加到暂存区
git commit -m ""  # 提交
git push          # 推送到远程
git pull          # 拉取远程更新
git branch        # 分支管理
git merge         # 合并分支
git rebase        # 变基（线性历史）
git stash         # 暂存未提交修改
```

## 工作流

- **GitHub Flow**：feature branch → PR → merge to main
- **Git Flow**：main + develop + feature + release + hotfix 分支
- **Trunk-Based Development**：直接在 main 上开发，通过 feature flag 和短分支控制

## 托管平台

| 平台 | 特点 |
|------|------|
| GitHub | 最大的开源社区，Copilot 集成 |
| GitLab | 内置 CI/CD，可自托管 |
| Gitee | 国内平台，访问速度快 |
| Bitbucket | Atlassian 生态集成 |

## 关系

- [[github]] — 最大 Git 托管平台
- [[ci-cd]] — Git 触发自动构建部署
