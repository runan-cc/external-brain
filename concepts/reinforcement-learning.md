---
title: Reinforcement Learning (RL)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [algorithm, training, agent]
sources: []
confidence: high
---

# Reinforcement Learning (RL)

## 定义

强化学习是机器学习的第三大范式（与监督学习、无监督学习并列）。Agent 通过**与环境交互**、获得**奖励信号**来学习最优策略——不依赖标注数据，而是通过试错学习。

## 核心框架：MDP

Markov Decision Process（马尔可夫决策过程）：

- **State (S)**：环境状态
- **Action (A)**：Agent 可执行的动作
- **Reward (R)**：即时反馈信号
- **Policy (π)**：从状态到动作的映射（即"策略"）
- **Value Function (V)**：从状态开始预期的累积奖励

## 关键算法

| 类别 | 代表算法 | 核心思想 |
|------|----------|----------|
| Value-based | DQN | 学习最优 Q 值函数，选择 Q 值最高的动作 |
| Policy-based | REINFORCE, PPO | 直接优化策略函数 |
| Actor-Critic | A3C, SAC | 同时学习 Actor (策略) 和 Critic (价值) |
| Model-based | AlphaZero, MuZero | 学习环境模型来模拟推演 |

## PPO (Proximal Policy Optimization)

PPO 是目前最广泛使用的 RL 算法，也是 [[rlhf]] 的训练算法：

- 高效的策略梯度方法
- 通过 clip 限制更新幅度，比 TRPO 更简单
- 在 ChatGPT 对齐和游戏 AI 中广泛使用

## RL 在 LLM 中的应用

- **RLHF**：见 [[rlhf]]
- **DeepSeek-R1**：纯 RL 训练推理能力
- **Tool use**：Agents 通过 RL 学习何时调用哪个工具

## 经典应用

| 领域 | 成就 |
|------|------|
| 游戏 | AlphaGo, OpenAI Five, AlphaStar |
| 机器人 | 机械臂操控、自动驾驶决策 |
| LLM | RLHF / DPO / R1 推理训练 |

## 关系

- [[rlhf]] — RL 在 LLM 对齐中的应用
- [[deepseek]] — R1 的纯 RL 推理训练
