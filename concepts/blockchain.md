---
title: 区块链基础
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [blockchain, cryptography, distributed]
sources: []
confidence: high
---

# 区块链基础

## 定义

区块链是**去中心化的分布式账本**——通过密码学保证数据不可篡改，通过共识机制在网络节点间达成一致。2008 年 Satoshi Nakamoto 在 Bitcoin 白皮书中首次实现。

## 核心概念

### 区块结构

```
Block N
├── Block Header
│   ├── Previous Block Hash  ← 链式连接
│   ├── Merkle Root          ← 交易摘要
│   ├── Timestamp
│   ├── Difficulty Target
│   └── Nonce                ← PoW 试出来的数
└── Transactions
    ├── Tx 1: Alice → Bob 0.5 BTC
    ├── Tx 2: Carol → Dave 2.0 BTC
    └── ...
```

### 链式结构

```
Block 0 ← Block 1 ← Block 2 ← Block 3 ← ...
(创世块)   Hash(0)   Hash(1)   Hash(2)
```

任何修改 Block 1 都会改变 Hash(1)，破坏整个链 → **不可篡改性**。

### Merkle Tree

```
       Merkle Root
      /          \
   Hash(AB)    Hash(CD)
   /    \       /    \
 Hash(A) Hash(B) Hash(C) Hash(D)
  ↑       ↑       ↑       ↑
 Tx A    Tx B    Tx C    Tx D
```

- 高效验证某交易是否在区块中：O(log n)
- SPV (Simplified Payment Verification)：轻节点只需 Block Header，不需要全部交易

## 共识机制

### Proof of Work (PoW)
矿工求解难题（找 nonce 使 hash < target），先解出的出块+得奖励。

| 特性 | 说明 |
|------|------|
| 安全性 | 攻击者需 >50% 算力 |
| 能耗 | 极高（Bitcoin ~100 TWh/年） |
| 出块 | ~10 分钟 |
| 使用 | Bitcoin, Litecoin, Dogecoin(仅变体) |

### Proof of Stake (PoS)
按持有 token 量选验证者出块，不需要算力竞赛。

| 特性 | 说明 |
|------|------|
| 安全性 | 攻击者需 >2/3 token（且可被罚没） |
| 能耗 | 极低（>99.9% 减排） |
| 出块 | 12 秒（Ethereum） |
| 使用 | Ethereum (2022 Merge), Cardano, Solana |

### 其他共识

| 机制 | 说明 | 使用 |
|------|------|------|
| DPoS | 持币者投票选超级节点 | EOS, TRON |
| PBFT | 实用拜占庭容错 | Hyperledger |
| PoH | 历史证明（时间序列） | Solana |

## 智能合约

**运行在区块链上的程序代码**，自动执行预设规则。

```solidity
// Ethereum 智能合约 (Solidity)
contract SimpleStorage {
    uint256 storedData;
    function set(uint256 x) public { storedData = x; }
    function get() public view returns (uint256) { return storedData; }
}
```

| 平台 | 语言 | 特点 |
|------|------|------|
| Ethereum | Solidity, Vyper | EVM，最大生态 |
| Solana | Rust, C | 高性能 (~65K TPS) |
| Polkadot | Rust (Substrate) | 跨链互操作 |

## 关键属性

| 属性 | 含义 |
|------|------|
| 去中心化 | 无单一控制方 |
| 不可篡改 | 已确认区块无法修改 |
| 透明 | 所有人可验证交易 |
| 无需信任 | 不需要信任对方，信任密码学 |

## 区块链三角 (Trilemma)

```
     安全性
      /\
     /  \
    /    \
   /  ?   \
  /________\
去中心化    可扩展性
```
三者取二，难以三者兼得。Ethereum 通过 L2 (Rollups) 解决扩展性。

## 关系

- [[cryptography]] — 哈希、数字签名是区块链的基石
- [[distributed-consensus]]
- [[distributed-systems]]
