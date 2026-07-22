---
title: 信息论基础
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [information-theory, mathematics, compression]
sources: []
confidence: high
---

# 信息论基础

## 定义

信息论是 Claude Shannon 于 1948 年创立的数学理论，研究信息的**量化、存储和传输**。它是数据压缩、纠错编码、密码学、机器学习和通信系统的理论基础。

## 核心概念

### 信息熵 (Entropy)

$$H(X) = -\sum_{x \in X} p(x) \log_2 p(x)$$

熵衡量事件的不确定性。单位：bit。

| 场景 | 熵 |
|------|-----|
| 公平硬币 | $H = 1$ bit（最大不确定） |
| 99% 正面 | $H \approx 0.08$ bit（几乎确定） |
| 确定的硬币（两面正面） | $H = 0$ bits（零不确定） |

### 交叉熵 (Cross-Entropy)

$$H(p, q) = -\sum_{x} p(x) \log_2 q(x)$$

- $p$：真实分布，$q$：预测分布
- 衡量 $q$ 描述 $p$ 需要的额外 bit 数
- **交叉熵 ≈ 普遍 + 散度**
- **ML 中交叉熵损损失用于分类任务**

### KL 散度

$$D_{KL}(p \| q) = \sum_{x} p(x) \log_2 \frac{p(x)}{q(x)}$$

- 两个分布之间的"距离"（非对称）
- 也叫做**相对熵**
- 总是 $\geq 0$，为 0 时 $p = q$

### 互信息 (Mutual Information)

$$I(X;Y) = H(X) - H(X|Y)$$

衡量 $Y$ 所含关于 $X$ 的信息量。ML 中用于特征选择和表示学习。

## 数据压缩

| 方法 | 类型 | 原理 |
|------|------|------|
| Huffman Coding | 无损 | 频率高的符号用短码 |
| LZ77/LZ78 | 无损 | 滑动窗口 + 字典（ZIP, gzip） |
| Arithmetic Coding | 无损 | 整个消息编码为一个浮点数 |
| JPEG | 有损 | DCT 变换 + 量化丢弃高频 |
| H.264/H.265 | 有损 | 帧间预测 + 变换编码 |
| FLAC | 无损音频 | 线性预测 |

### 压缩极限

- **无损压缩**：Shannon Source Coding Theorem——平均码长不能低于熵
- **有损压缩**：Rate-Distortion Theory——给定失真下所需的 bit 率

## 信道容量与纠错

### 信道容量

$$C = B \log_2(1 + \text{SNR})$$

Shannon-Hartley 定理：给定带宽 $B$ 和信噪比 SNR，理论上最大无差错传输速率。

### 纠错码

| 码 | 用途 |
|-----|------|
| Hamming Code | 纠正 1 位错误 |
| Reed-Solomon | CD/DVD/QR 码，纠正突发错误 |
| LDPC | 5G, Wi-Fi 6, 接近 Shannon 极限 |
| Turbo Code | 3G/4G, 深空通信 |
| Polar Code | 5G 控制信道 |

## 在 AI/ML 中的应用

| 概念 | 应用 |
|------|------|
| 交叉熵 | 分类损失函数的标准选择 |
| 熵 | 决策树分裂准则 (ID3/C4.5) |
| KL 散度 | VAE 的 latent space 正则化 |
| 互信息 | 表示学习 (InfoNCE, SimCLR 对比学习) |
| 最小描述长度 (MDL) | 模型选择 (奥卡姆剃刀形式化) |

## 关系

- [[cryptography]] — 信息论定义完美加密
- [[data-structures-and-algorithms]] — Huffman 编码
- [[large-language-model]] — perplexity / CE Loss
