# 2026-04-19-17-08-24

本目录包含 2 篇最新下载的 TEE 相关论文，均来自 NDSS 2025（网络与分布式系统安全研讨会）。

## 论文列表

| 文件名 | 年份 | 会议 | DOI |
|--------|------|------|-----|
| 2025 - The Forking Way - When TEEs Meet Consensus.pdf | 2025 | NDSS | 10.14722/ndss.2025.241934 |
| 2025 - TME-Box - Scalable In-Process Isolation through Intel TME-MK Memory Encryption.pdf | 2025 | NDSS | — |

---

## 论文一：The Forking Way: When TEEs Meet Consensus

**作者**：Annika Wilde, Tim Niklas Gruel, Claudio Soriente, Ghassan Karame（Ruhr University Bochum, NEC Laboratories Europe）

**核心问题**：TEE（可信执行环境）与区块链结合时，如何抵御"分叉攻击"（forking attack）——攻击者通过状态回滚或实例克隆对 TEE 进行攻击？

**主要贡献**：

1. **系统化分类**：对 29 种基于 TEE 的区块链方案进行系统分析，将其反分叉技术分为四大类
2. **新型攻击**：发现了三个生产级 TEE 区块链（Ten、Phala、Secret Network）此前未文档化的分叉攻击漏洞，包括基于克隆的攻击
3. **实用对策**：提出针对这些漏洞的有效防御措施，并负责任地披露给了相关平台开发方

**技术要点**：
- TEE 分叉攻击分为两类：**回滚攻击**（rollback）和**克隆攻击**（cloning）
- 现有研究只考虑了回滚攻击，而本文首次系统分析了克隆攻击
- 无状态飞地可通过临时飞地身份（ephemeral enclave identity）防御分叉攻击
- 有状态飞地的保护方案取决于共识层类型（最终共识 vs 确定共识）和吞吐量

**与本合集中其他论文的关系**：
- 与 *The Road to Trust*（同期下载）同属 NDSS 2025，研究 TEE 的安全属性
- 与 *Transparent Attested DNS*（2026-04-19-16-46-35）共享机密计算 + 区块链交叉主题

---

## 论文二：TME-Box: Scalable In-Process Isolation through Intel TME-MK Memory Encryption

**作者**：Martin Unterguggenberger, Lukas Lamster, David Schrammel, Stefan Mangard（Graz University of Technology），Martin Schwarzl（Cloudflare）

**核心问题**：如何在不引入进程间通信开销的情况下，利用 Intel TME-MK（全内存加密）实现进程内的可扩展隔离？

**主要贡献**：

1. **TME-MK 隔离方案**：利用 Intel TME-MK 硬件内存加密，在单一进程内通过 VMPL（虚拟机特权级）实现可扩展隔离
2. **性能优化**：相比传统进程隔离，TME-MK 无额外加密开销，适合云环境
3. **安全模型**：抵御来自同一进程内其他代码（untrusted code）的攻击

**技术要点**：
- Intel TME-MK（Total Memory Encryption - Multi-Key）：在硬件层面加密整个内存，支持多密钥
- VMPL（Virtual Machine Privilege Level）：Intel TDX 引入的特权级机制，可在同一进程内实现隔离域
- 与 TME（单密钥）相比，TME-MK 支持每个隔离域使用不同密钥，适合多租户场景
- 本文是第一篇利用 TME-MK 实现进程内可扩展隔离的学术工作

**与本合集中其他论文的关系**：
- 与 *The Road to Trust* 均涉及 Intel TDX/TME 硬件安全机制
- 与进程隔离相关工作（如 TEE-MR 等）关注点不同：本文专注于内存加密硬件而非软件隔离

**关键词**：TME-MK, 内存加密, 进程内隔离, Intel TDX, 云安全, 多租户
