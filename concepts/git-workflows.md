---
title: Git Workflows & Code Review
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [git, workflow, methodology, collaboration]
sources: []
confidence: high
---

# Git 工作流与代码审查

## Git 工作流

### GitFlow (Vincent Driessen, 2010)

```
main    ─●────────────●──────────●──  (发布)
          \          / \        /
release    ●────────●   ●──────●      (预发布)
            \        /
develop      ●──●───●──●──●──●──     (集成)
                \  /
feature           ●──●                (功能分支)
```

| 分支 | 用途 |
|------|------|
| main | 生产代码 |
| develop | 集成分支 |
| feature/* | 功能开发 |
| release/* | 发布准备（bug fix、版本号） |
| hotfix/* | 生产紧急修复 |

✅ 适合：定期发布的传统软件（如游戏发布、年度产品）
❌ 问题：分支太多、合并复杂、不适合持续部署

### Trunk-Based Development

```
main ─●─●─●─●─●─●─●─●─●─  (所有东西在这里)
       \/
    short-lived branch
    (< 1 day)
```

| 实践 | 说明 |
|------|------|
| 短分支 | 最多一天就合并回主干 |
| Feature Flags | 未完成功能藏起来，不影响发布 |
| 小 PR | < 200 行改动 |
| Diamond Dependency | 多人改同一文件更频繁沟通 |

✅ 适合：持续部署、DevOps、Google/Facebook 等科技巨头
✅ CI/CD 天然适配

### GitHub Flow

```
main ─●────────●────────●──  (可部署)
        \      / \      /
feature   ●────●   ●────●
```

- 从 main 拉 feature 分支
- 开 PR → Review → 合并 → 部署
- 简单：只 main + feature 分支
- 适合：SaaS/Web 服务

## Code Review

### 为什么 Review

| 收益 | 说明 |
|------|------|
| 知识分享 | 团队了解代码库，减少 bus factor |
| 发现 bug | 第二双眼睛（不是 QA 替代） |
| 统一代码风格 | 保持一致性 |
| 设计审查 | 在代码定型前发现架构问题 |
| 责任感 | 知道有人会看，写得更认真 |

### 好 Review 的原则

| 原则 | 说明 |
|------|------|
| **小 PR** | < 400 行，15 分钟内能 review 完 |
| **描述清晰** | 做了什么、为什么这样做 |
| **Review 及时** | 24 小时内给出反馈 |
| **友善** | "建议"不是"要求"，"我们"不是"你" |
| **不是找茬** | 风格让 linter/formatter 管，Review 关注逻辑和设计 |
| **测试** | PR 应该包含测试 |

### 坏 Review 的迹象

- PR 几百行几千行（没人能认真看完）
- 拖了一周没看
- Review 意见是"重写吧"
- 永远不给 approve，吹毛求戒

## 关系

- [[git]]
- [[github]]
- [[ci-cd]]
- [[agile]]
