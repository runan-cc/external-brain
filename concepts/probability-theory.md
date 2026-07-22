---
title: 概率论基础
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [probability, mathematics, statistics, machine-learning]
sources: []
confidence: high
---

# 概率论基础

## 定义

概率论是研究**随机性和不确定性**的数学——问的不是"会发生什么"，而是"这件事发生的可能性有多大"。ML 的全部分类、生成、强化学习都建立在概率论之上。

## 基本概念

| 概念 | 定义 | 示例 |
|------|------|------|
| 样本空间 Ω | 所有可能结果 | {1,2,3,4,5,6} |
| 事件 | Ω 的子集 | 掷出偶数 {2,4,6} |
| 概率 P | 事件发生的可能性 | P(偶数) = 3/6 = 0.5 |
| 条件概率 P(A\|B) | 已知 B 发生，A 的概率 | P(A\|B) = P(A∩B)/P(B) |

## 贝叶斯定理

$$P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}$$

- **先验 P(A)**：事件 A 的自然概率
- **似然 P(B|A)**：已知 A 发生的情况下 B 出现的概率
- **后验 P(A|B)**：看到证据 B 后，A 有多可能

**在 ML 中**：

```python
P(label|data) = P(data|label) × P(label) / P(data)
# 后验        = 似然         × 先验       / 证据
```

- 朴素贝叶斯分类器直接用这个
- [[reinforcement-learning]] 中根据环境反馈更新信念
- [[diffusion-models]] 中逐步从噪声推导出数据分布

## 随机变量与分布

| 分布 | 用途 | 参数 |
|------|------|------|
| 伯努利 (Bernoulli) | 二值事件（抛硬币） | p |
| 二项 (Binomial) | n 次独立伯努利 | n, p |
| 均匀 (Uniform) | 每个值等概率 | a, b |
| **正态/高斯** (Normal) | 自然界无处不在 | μ, σ² |
| 指数 (Exponential) | 等待时间 | λ |
| 泊松 (Poisson) | 单位时间的随机事件数 | λ |
| 多项 (Multinomial) | 多分类 | n, p₁...pₖ |
| Dirichlet | 分布的分布（多项的先验） | α₁...αₖ |

> Laplace 中心极限定理：大量独立同分布的随机变量之和 → 正态分布（为什么正态无处不在）

## 期望与方差

| 概念 | 公式 | 含义 |
|------|------|------|
| 期望 E[X] | Σ x·p(x) | "平均"结果 |
| 方差 Var(X) | E[(X-E[X])²] | 离均值的分散程度 |
| 标准差 σ | √Var | 与数据同量级的分散度 |
| 协方差 Cov(X,Y) | E[(X-E[X])(Y-E[Y])] | X 和 Y 怎么一起变化 |

## 最大似然估计 (MLE)

给定观测数据，找出**最可能产生这些数据的参数**。

$$θ_{MLE} = \argmax_θ P(D|θ)$$

- [[gradient-descent]] 通常就是在最小化负对数似然
- 交叉熵损失 = MLE 的等价形式

## 在 ML 中的关键应用

| ML 概念 | 概率基础 |
|---------|----------|
| Softmax | 将分数转为概率分布 |
| 交叉熵损失 | 两个分布的距离 → MLE |
| [[vae]] | 从分布中采样 |
| [[diffusion-models]] | 逐步去噪 = 概率推断 |
| Dropout | 随机丢弃 = 概率正则化 |
| 贝叶斯推断 | 概率更新信念 |
| GMM | 数据由多个高斯混合生成 |

## 关系

- [[information-theory]] — 概率 → 熵
- [[machine-learning]]
- [[gradient-descent]]
