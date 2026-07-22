---
title: 梯度下降
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [optimization, training, algorithm, machine-learning]
sources: []
confidence: high
---

# 梯度下降 (Gradient Descent)

## 定义

梯度下降是机器学习中**最核心的优化算法**——通过沿着损失函数梯度的反方向迭代更新参数，逐步最小化损失。几乎所有神经网络的训练都基于它。

## 核心公式

$$\theta_{t+1} = \theta_t - \eta \nabla_\theta J(\theta_t)$$

- $\theta$：模型参数（权重）
- $\eta$：学习率（learning rate）
- $\nabla J(\theta)$：损失函数对参数的梯度

## 变体

### Batch Gradient Descent
使用**全部数据**计算梯度，精确但极慢。

### SGD (Stochastic Gradient Descent)
每次用**一个样本**更新，快但不稳定。

### Mini-batch SGD
每次用**一小批样本**（如 32/64 个），平衡速度和稳定性——实际训练的标准做法。

## 优化器演进

| 优化器 | 核心思想 |
|--------|----------|
| SGD + Momentum | 积累历史梯度的"动量"，加速收敛 |
| NAG | 先按动量方向走一步，再计算梯度修正 |
| AdaGrad | 自适应学习率（不同参数不同步长） |
| RMSprop | AdaGrad 的改进，防止学习率过早衰减 |
| **Adam** | Momentum + RMSprop，默认首选 |
| AdamW | Adam + 权重衰减解耦 |
| LION | 只使用梯度符号，更省内存 |
| Muon | 矩阵正交化动量，大 batch 训练 |

## 关键挑战

### 学习率 (lr) 选择

| 太大 | 太小 |
|------|------|
| 振荡/发散 | 收敛极慢 |
| 跳过最优陷 | 陷入局部最优 |

**学习率调度**：
- Step Decay：每隔 N epoch 减半
- Cosine Annealing：余弦函数平滑衰减
- Warmup：从极小 lr 线性增加（大模型训练标配）

### 局部最优与鞍点

- 浅层网络：局部最优是问题
- 深层网络：**鞍点（saddle point）才是主要困境**——梯度为零但不是最优
- 动量 + 自适应学习率帮助逃逸鞍点

### 梯度消失/爆炸

| 问题 | 现象 |
|------|------|
| 梯度消失 | 深层梯度→0，前面的层几乎不更新 |
| 梯度爆炸 | 梯度指数增长，损失 NaN |

**对策**：BatchNorm, LayerNorm, Residual Connection, 梯度剪裁

## 二阶方法

| 方法 | 原理 | 问题 |
|------|------|------|
| Newton's Method | 用 Hessian 矩阵调整步长 | Hessian O(n²) — 太贵 |
| L-BFGS | Hessian 近似，内存友好 | 神经网络中不如 Adam |

## 关系

- [[machine-learning]]
- [[large-language-model]]
- [[transformer-architecture]] — AdamW 是 Transformer 训练标配
