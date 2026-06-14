# Wiki Schema

## Domain
通用知识库 — AI/ML 研究、软件开发、DevOps、系统架构、工具链、技术笔记等全领域知识积累。

## Conventions
- 文件名: 小写 + 连字符, 无空格 (e.g., `transformer-architecture.md`)
- 每个 wiki 页面开头需 YAML frontmatter (见下)
- 使用 `[[wikilinks]]` 跨页面链接 (每页至少 2 个出链)
- 更新页面时务必更新 `updated` 日期
- 每个新页面必须加入 `index.md` 对应分类下
- 每个操作必须追加到 `log.md`
- **Provenance markers (溯源标记):** 整合 3+ 来源的页面, 在段落末尾用 `^[raw/articles/source-file.md]` 标注具体来源, 让读者能追踪每个论断的来源。
- 中文为主，英文术语保留原文。同时可处理中英文内容。

## Frontmatter
```yaml
---
title: 页面标题
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query | summary
tags: [来自下面分类的标签]
sources: [raw/articles/source-name.md]
# 可选质量信号:
confidence: high | medium | low        # 论断的可靠程度
contested: true                         # 页面存在未解决矛盾时设置
contradictions: [other-page-slug]       # 与本页冲突的页面
---
```

### raw/ 源文件 Frontmatter
```yaml
---
source_url: https://example.com/article
ingested: YYYY-MM-DD
sha256: <正文内容的 SHA256 摘要>
---
```
`sha256` 用于重入时检测内容是否变更: 计算正文部分的 SHA256, 与存储值对比, 相同则跳过, 不同则标记漂移。

## 标签分类 (Tag Taxonomy)

### 核心分类
- **模型/算法:** model, architecture, benchmark, training, inference, algorithm
- **人/组织:** person, company, lab, open-source, community
- **技术:** optimization, fine-tuning, alignment, data, scaling, quantization, distillation
- **开发:** python, javascript, rust, go, typescript, framework, testing, debugging
- **DevOps:** docker, kubernetes, ci-cd, monitoring, networking, security, linux, database
- **工具:** editor, cli, tool, agent, automation, productivity
- **元分类:** comparison, timeline, controversy, prediction, tutorial, reference
- **硬件:** gpu, cpu, memory, storage, hardware
- **系统设计:** architecture, pattern, distributed, api, protocol, performance

规则: 每个页面标签必须来自此分类。需新增标签时先加到这里再用。

## 页面创建阈值 (Page Thresholds)
- **创建页面:** 当实体/概念在 2+ 来源中出现, 或是对一个来源至关重要时
- **追加到已有页面:** 当来源提到已有页面覆盖的内容时
- **不要创建页面:** 一次性的简单提及、次要无关细节、或领域外内容
- **拆分页面:** 超过 ~200 行时拆分, 用交叉链接关联子主题
- **归档页面:** 内容完全被取代时, 移到 `_archive/`, 从 index 移除

## 实体页面 (Entities)
每个值得记录的实体一个页面。包括:
- 概览 / 是什么
- 关键事实和日期
- 与其他实体的关系 ([[wikilinks]])
- 来源引用

## 概念页面 (Concepts)
每个概念或主题一个页面。包括:
- 定义 / 解释
- 当前知识状态
- 待解决问题或争议
- 相关概念 ([[wikilinks]])

## 比较页面 (Comparisons)
并列分析。包括:
- 比什么和为什么
- 比较维度 (表格优先)
- 总结或结论
- 来源

## 更新策略 (Update Policy)
新信息与已有内容冲突时:
1. 检查日期 — 新来源通常优于旧来源
2. 确实矛盾时, 标注双方立场及日期来源
3. 在 frontmatter 标记矛盾: `contradictions: [page-name]`
4. 在 lint 报告中提示用户审核
