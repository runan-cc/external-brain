---
title: Reinforcement Learning from Human Feedback (RLHF)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [training, alignment, fine-tuning, technique]
sources: []
confidence: high
---

# RLHF (Reinforcement Learning from Human Feedback)

## 定义

RLHF 是通过人类偏好反馈来**对齐** [[large-language-model]] 行为的技术。它是 ChatGPT 成功的关键环节——让模型从"完成文本"进化为"遵循人类意图的对话助手"。

## 三阶段

### Step 1: Supervised Fine-Tuning (SFT)

用高质量的人类标注对话数据微调预训练模型。

### Step 2: Reward Model Training

- 人类标注员对多个模型输出排序（A > B > C）
- 训练奖励模型（RM）学习"人类偏好"函数
- RM 的输入是 (prompt, response)，输出是偏好分数

### Step 3: PPO 强化学习

- 用 PPO 算法（Proximal Policy Optimization）优化模型
- 模型生成回答 → RM 打分 → 梯度更新 → 循环
- 加入 KL 惩罚，防止模型过度偏离 SFT 版本

## DPO（Direct Preference Optimization）替代

DPO 于 2023 年发表，**跳过奖励模型**，直接在偏好数据上优化。公式：

$$\text{Loss}_{DPO} = -\log \sigma\left(\beta(\log\frac{\pi_\theta(y_w|x)}{\pi_{ref}(y_w|x)} - \log\frac{\pi_\theta(y_l|x)}{\pi_{ref}(y_l|x)})\right)$$

- 比 RLHF 更简单、更稳定
- 不需要训练单独的奖励模型
- 性能与 RLHF 相当或更好

## 问题

| 问题 | 说明 |
|------|------|
| Reward hacking | 模型学会游戏化 RM 而非真正对齐 |
| 标注成本 | 高质量人类标注很贵 |
| 偏好漂移 | 不同人群偏好不同 |
| 过度对齐 | 模型可能过于保守（refusal 增多） |

## 关系

- [[large-language-model]]
- [[fine-tuning]]
- [[openai]] — ChatGPT 背后的 RLHF 实践
- [[anthropic]] — Constitutional AI 是 RLHF 的替代方案
