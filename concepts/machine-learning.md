---
title: 机器学习基础
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [machine-learning, model, training, algorithm]
sources: []
confidence: high
---

# 机器学习基础

## 定义

机器学习（ML）是**让计算机从数据中学习模式和规律**的方法，无需显式编程。它是 AI 的子领域，也是 [[large-language-model]] 的学科基础。

## 三大范式

| 范式 | 数据 | 目标 | 示例 |
|------|------|------|------|
| **监督学习** | 有标签 (X → y) | 学习映射 f(X)≈y | 分类、回归 |
| **无监督学习** | 无标签 (X only) | 发现隐藏结构 | 聚类、降维 |
| **强化学习** | 交互 (S, A, R) | 最大化累积奖励 | 游戏、机器人 |

见 [[reinforcement-learning]]

## 监督学习

### 分类 vs 回归

| 任务 | 输出类型 | 损失函数 | 示例 |
|------|----------|----------|------|
| 二分类 | {0, 1} | Cross-Entropy | 垃圾邮件检测 |
| 多分类 | {1, ..., K} | Categorical CE | 图像分类 |
| 回归 | 连续值 | MSE, MAE | 房价预测 |

### 经典算法

| 算法 | 特点 | 适用 |
|------|------|------|
| 线性回归 | 最简单，可解释 | 基线模型 |
| 逻辑回归 | 概率输出 | 二分类 |
| SVM | 最大间隔，核技巧 | 高维小样本 |
| 决策树 | 可解释、非线性 | 特征重要性 |
| 随机森林 | 集成学习、稳健 | 通用分类/回归 |
| XGBoost/LightGBM | 梯度提升树 SOTA | 结构化数据王者 |
| KNN | 惰性学习、无训练 | 小数据基线 |

## 无监督学习

| 方法 | 用途 |
|------|------|
| K-Means | 硬聚类 |
| DBSCAN | 密度聚类（航噪声） |
| PCA | 线性降维 |
| t-SNE / UMAP | 可视化降维 |
| Autoencoder | 非线性降维/特征学习 |
| GMM | 概率聚类 |

## 核心概念

### 偏差-方差权衡

| 情况 | 偏差 | 方差 | 表现 |
|------|------|------|------|
| 欠拟合 | 高 | 低 | 训练差、测试差 |
| 过拟合 | 低 | 高 | 训练好、测试差 |
| 良好拟合 | 低 | 低 | 训练好、测试好 |

### 正则化
防止过拟合：
- **L1 (Lasso)**：产生稀疏模型（特征选择）
- **L2 (Ridge)**：权重衰减，防止参数过大
- **Dropout**：训练时随机丢弃神经元（DL 中）
- **Early Stopping**：验证损失不再改善时停止

### 训练/验证/测试分割

```
全部数据 → 训练集 (60-80%) + 验证集 (10-20%) + 测试集 (10-20%)
              ↓                    ↓                    ↓
          训练模型          调参/选模型            最终评估
```

## 评估指标

| 任务 | 指标 |
|------|------|
| 分类 | Accuracy, Precision, Recall, F1, AUC-ROC |
| 回归 | MSE, MAE, R² |
| 聚类 | Silhouette Score, Davies-Bouldin |
| 生成 | BLEU, ROUGE, Perplexity |

## 关系

- [[reinforcement-learning]]
- [[large-language-model]]
- [[information-theory]] — 交叉熵 = ML 的默认损失
- [[diffusion-models]]
