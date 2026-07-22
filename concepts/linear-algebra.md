---
title: 线性代数核心
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [mathematics, linear-algebra, machine-learning, fundamentals]
sources: []
confidence: high
---

# 线性代数核心 (Linear Algebra Essentials)

## 定义

线性代数是机器学习和计算机图形学的**数学语言**——数据是矩阵、变换是矩阵乘法、特征提取是特征值分解。不懂线性代数，AI/ML 就是黑盒。

## 标量、向量、矩阵、张量

| 概念 | 维度 | 示例 |
|------|------|------|
| Scalar | 0D | 3.14 |
| Vector | 1D | [1, 2, 3] (3D 向量) |
| Matrix | 2D | [[1,2],[3,4]] (2×2 矩阵) |
| Tensor | 3D+ | 一张图片 = 3D (H×W×C) |

## 矩阵乘法

`C = AB`：C 的第 i 行第 j 列 = A 的第 i 行 **点积** B 的第 j 列。

```python
# A(2×3) × B(3×2) = C(2×2)
A = [[1, 2, 3],
     [4, 5, 6]]
B = [[7, 8],
     [9, 10],
     [11, 12]]
C[0][0] = 1×7 + 2×9 + 3×11 = 58
```

### ML 中矩阵乘法的意义

- 全连接层：`y = Wx + b`
- Attention：`QK^T` — 所有词两两点积 → 相似度矩阵
- Embedding 查找：one-hot × Embedding Matrix = 取出对应行

## 转置

`A^T`：行列互换。`(A^T)_{ij} = A_{ji}`

## 点积 (Dot Product)

`a·b = Σ a_i × b_i = ‖a‖‖b‖cosθ`

- θ=0 (同方向) → 点积最大
- θ=90° → 点积=0 (正交)
- θ=180° → 点积最小 (反向)

→ Attention 中的 `QK^T` 就是计算所有词向量的点积相似度！

## 范数 (Norm)

| 范数 | 公式 | 含义 |
|------|------|------|
| L1 (曼哈顿) | Σ\|x_i\| | 稀疏性、特征选择 |
| L2 (欧氏) | √(Σ x_i²) | 最常见距离 |
| L∞ | max\|x_i\| | 最大元素 |

L2 正则化 = 权重向量的 L2 范数加入损失 → 权重衰减。

## 矩阵分解

### 特征分解 (Eigendecomposition)

$$A v = \lambda v$$

- 矩阵 A 作用于特征向量 v，只缩放不旋转
- 特征值 λ 表示缩放因子
- **PCA = 协方差矩阵的特征分解**

### SVD (奇异值分解)

$$A = U \Sigma V^T$$

| 矩阵 | 含义 |
|------|------|
| U | 左奇异向量（A 的行空间） |
| Σ | 奇异值（对角，降序） |
| V^T | 右奇异向量（A 的列空间） |

- ML 应用：**LoRA** 本质就是低秩分解（只用前 r 个奇异值）
- 图像压缩：保留前 k 个奇异值 → 远小于原图但视觉相近
- [[lora]] = 用两个小矩阵 `B·A` 近似 full-rank 权重更新

## 行列式

`det(A)` = 矩阵代表的"体积缩放因子"。
- det = 0 → 不可逆 → 列线性相关 → 信息冗余

## 在 ML 中的应用总结

| ML 概念 | 线性代数 |
|---------|----------|
| 数据集 | 矩阵 (N 样本 × D 特征) |
| 神经网络层 | 矩阵乘法 `y = Wx` |
| 嵌入 | 矩阵的某一行 |
| Attention | 矩阵乘法 + Softmax |
| [[lora]] | 低秩矩阵近似 (SVD) |
| [[pca]] | 协方差矩阵的 SVD |
| [[gradient-descent]] | 梯度 = 向量 |
| 图像 | 3D 张量 (H×W×C) |
| Batch | 4D 张量 (B×H×W×C) |

## 关系

- [[machine-learning]]
- [[gradient-descent]]
- [[lora]]
