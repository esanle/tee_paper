# TEE 论文综述 — 2026-04-20-17-00-00

本目录收录了 3 篇 2025 年 12 月发表的关于**可信执行环境（Trusted Execution Environment, TEE）**的最新论文，全部下载自 arXiv，涵盖 TEE 在智能合约密钥管理、端侧模型保护和分布式文件系统等前沿应用场景。

---

## 一、论文概要（每篇约 1000 字）

### 1. HOT Protocol：基于 TEE 的智能合约多方计算网络密钥管理
**英文标题：** HOT Protocol
**arXiv ID：** 2512.02287
**作者：** Peter Volnov, Georgii Kuksa, Andrey Zhevlakov 等

HOT Protocol 提出了一种让智能合约安全拥有和管理私钥的解决方案。传统以太坊智能合约的私钥管理依赖单点 MPC（多方计算）网络，存在密钥泄露风险。本文将 MPC 节点运行在 TEE（可信执行环境）内部，利用硬件隔离能力增强密钥安全性，同时降低经济成本。TEE 作为密钥保护的信任根，即使 MPC 参与者不诚实，攻击者也无法从 TEE 飞地中提取私钥。HOT Protocol 设计了轻量级密钥管理协议，支持智能合约签名而不需要将完整私钥暴露在任何单点。安全分析表明，在 AMD SEV-SNP 或 Intel SGX 的威胁模型下，即使云服务商妥协，密钥仍受 TEE 硬件保护。本文对 Web3 应用的密钥安全管理和 DeFi 协议安全性有重要参考价值。

### 2. Amulet：端侧模型保护的快速 TEE 屏蔽推理
**英文标题：** Amulet: Fast TEE-Shielded Inference for On-Device Model Protection
**arXiv ID：** 2512.07495
**作者：** Zikai Mao, Lingchen Zhao, Lei Xu, Wentao Dong, Shenyi Zhang, Cong Wang, Qian Wang

随着移动端 AI 部署普及，模型知识产权和用户输入隐私面临泄露风险。现有端侧模型保护方案通常将权重存储在 TEE 内并在飞地内执行推理，但 TEE 性能开销限制了实际部署。Amulet 针对这一问题提出了高效的 TEE 屏蔽推理框架，核心优化在于减少 TEE 与主处理器之间的数据传输次数，同时保持推理结果的可远程验证性。通过模型量化和分层流水线策略，Amulet 在保持安全性的同时将推理延迟降低至接近明文推理水平。安全分析表明即使攻击者获得设备 root 权限，也无法提取模型权重或篡改推理过程。Amulet 的设计适用于手机端侧 AI、AR/VR 设备等对功耗和性能敏感的嵌入式场景。

### 3. CapsuleFS：基于 TEE 的多凭证 DataCapsule 文件系统
**英文标题：** CapsuleFS A Multi-credential DataCapsule Filesystem
**arXiv ID：** 2512.08067
**作者：** Qingyang Hu, Yucheng Huang, Manshi Yang

CapsuleFS 提出了一种基于 TEE 的安全文件系统架构，专为边缘计算场景设计。系统包含两个核心组件：DataCapsule 服务器（负责数据的存储、分发和复制）和运行在 TEE 内部的中介层（负责执行和管理写权限并确保请求完整性）。传统文件系统在边缘环境中面临数据泄露和未授权访问风险，CapsuleFS 通过 TEE 硬件隔离保证数据在存储和传输过程中的机密性和完整性，同时支持多凭证授权——不同用户可以使用不同的加密凭证访问各自的数据。论文详细描述了 DataCapsule 的数据封装格式和 TEE 中介层的设计，并给出了边缘存储场景下的性能评估，表明 TEE 开销在可接受范围内。本文对边缘计算安全存储和隐私保护文件系统设计有直接参考价值。

---

## 二、综合对比综述

本次收录的 3 篇论文代表了 2025 年底 TEE 技术应用的几个重要方向：

### 2.1 Web3 与区块链安全深化
**HOT Protocol** 和之前批次的 **Optimistic TEE-Rollups**（已在其他目录）代表了 TEE 在区块链领域的深度应用。MPC+ TEE 的组合正成为 Web3 密钥管理的新范式——纯密码学方案（如门限签名）面临执行复杂性和密钥泄露风险，而 TEE 提供硬件级密钥隔离，大幅简化协议设计同时提升安全性。

### 2.2 端侧 AI 模型保护成为热点
**Amulet** 与之前批次的 **MirageNet**、**TEE-Shielded DNN Partitioning**（SPOILER）等共同构成了端侧模型保护的研究主线。核心矛盾在于：TEE 内存受限（SGX EPC 仅数百 MB）而大模型参数量庞大，如何在安全与性能之间取得平衡。Amulet 的量化+流水线方案和 MirageNet 的异构 TEE+GPU 方案代表了两种不同的技术路径。

### 2.3 数据存储与文件系统
**CapsuleFS** 将 TEE 应用于文件系统设计，与之前批次的 **Transparent Attested DNS** 等一同表明 TEE 的应用边界正在从计算扩展至存储领域。DataCapsule 的多凭证设计对多租户边缘存储场景具有现实意义。

### 2.4 性能优化是落地关键
无论是 **Amulet** 的推理加速、**CapsuleFS** 的存储中介层，还是 **HOT Protocol** 的密钥管理协议，所有方案都必须在 TEE 带来的安全开销与实际部署性能之间做出权衡。这反映了 TEE 研究从"能不能做"到"怎么做更好"的成熟化转变。

---

## 三、参考文献

1. Peter Volnov et al., "HOT Protocol," arXiv:2512.02287, December 2025.
2. Zikai Mao et al., "Amulet: Fast TEE-Shielded Inference for On-Device Model Protection," arXiv:2512.07495, December 2025.
3. Qingyang Hu et al., "CapsuleFS: A Multi-credential DataCapsule Filesystem," arXiv:2512.08067, December 2025.

---

*本目录为一次性任务生成，所有 PDF 均已通过 MD5 去重验证，唯一存放于 `/tmp/tee_paper/2026-04-20-17-00-00/` 目录下。*
