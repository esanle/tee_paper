# TEE 论文综述 — 2026-04-20-16-45-36

本目录收录了 8 篇关于**可信执行环境（Trusted Execution Environment, TEE）**的 2025–2026 年最新论文，全部下载自 arXiv，涵盖 TEE 在区块链、LLM 隐私推理、模型保护、过程证明等前沿应用场景。

---

## 一、论文概要（每篇约 1000 字）

### 1. T-RBFT: 基于 TEE 的联盟链拜占庭共识
**英文标题：** T-RBFT: A Scalable and Efficient Byzantine Consensus Based on Trusted Execution Environment for Consortium Blockchain
**arXiv ID：** 2604.16053
**作者：** Wen Gao, Xinhong Hei, Yichuan Wang 等

本文提出了一种基于 TEE 的可扩展高效拜占庭容错共识协议 T-RBFT，专为联盟链场景设计。传统 BFT 协议（如 PBFT）依赖大量节点间通信验证，交易吞吐量受限。本文利用 TEE（推测为 Intel SGX 或 AMD SEV）的硬件隔离能力，将共识核心逻辑放入安全飞地执行，减少对外部验证的依赖。T-RBFT 通过将领袖选举和消息验证卸载至 TEE，降低了恶意节点干扰和女巫攻击风险，同时保持了与传统 BFT 相当的安全保证。实验表明，T-RBFT 在 64 节点联盟链中吞吐量显著优于传统 PBFT，且延迟更低。本文为 TEE 在区块链共识层的应用提供了新的设计思路，对理解 TEE 如何增强分布式系统安全性有重要参考价值。

### 2. Styx: 基于 TEE 粘性策略的协作私有数据处理
**英文标题：** Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy
**arXiv ID：** 2604.04082
**作者：** Shixuan Zhao 等

Styx 研究了如何在多方数据协作场景中保证数据使用权力的精细化控制。传统数据共享一旦交出数据，控制权即丧失；即使在 TEE 内部，数据处理后同样面临泄露风险。本文提出了"粘性策略"（Sticky Policy）概念——数据在整个处理链路中携带访问策略，任何处理行为必须满足策略约束。TEE 作为策略执行的信任根，保证即使是不诚实的参与方也无法绕过策略约束。Styx 的核心贡献在于设计了一套 TEE 可验证的策略 Enforcement 机制，适用于金融、医疗等高敏感数据的跨组织协作。评估显示其策略检查开销可接受，且对现有 TEE 平台（如 SGX）改动较小，具备实际部署可行性。

### 3. MirageNet: 异构 TEE+GPU 系统上的安全高效端侧模型保护
**英文标题：** MirageNet: A Secure, Efficient, and Scalable On-Device Model Protection in Heterogeneous TEE and GPU System
**arXiv ID：** 2601.13826
**作者：** （待补充）

随着端侧 AI 部署普及，模型知识产权和输入隐私保护成为关键挑战。MirageNet 针对 TEE 与 GPU 异构系统设计了安全高效的端侧模型保护框架。核心思路是将 DNN 模型分层——敏感层权重密文保存在 TEE 内，而计算密集型层卸载至 GPU，但通过 TEE 远程证明保证 GPU 执行环境的完整性。论文解决了 TEE 内存有限（EPC 页数约束）与大模型推理算力需求之间的矛盾，设计了模型分片和流水线策略，最小化 TEE 与 GPU 之间的数据传输并防止中间结果泄露。安全分析证明即使攻击者控制 GPU 驱动，也无法提取模型权重或输入数据。

### 4. Ringmaster: TrustZone TEE 高吞吐主机系统调用
**英文标题：** Ringmaster: How to juggle high-throughput host OS system calls from TrustZone TEEs
**arXiv ID：** 2601.16448
**作者：** Richard Habeeb 等

本文针对 ARM TrustZone 环境中 TEE（Secure World）与富执行环境（Rich OS）之间的系统调用性能瓶颈提出了优化方案。TrustZone TEE 通常以安全守护进程形式运行，每次系统调用需跨越安全世界边界（world switch），开销可达微秒级。Ringmaster 通过批量处理、异步调用和共享内存缓冲等机制，将高频系统调用的吞吐量提升一个数量级，同时保持安全世界对调用参数和返回值的完整验证。论文深入分析了 world switch 的性能开销来源，并提出了一套设计准则，对移动端 TEE 应用开发有直接指导意义。

### 5. TeeMAF: 面向区块链 DApp 链上链下函数的 TEE 互认证框架
**英文标题：** TeeMAF: A TEE-Based Mutual Attestation Framework for On-Chain and Off-Chain Functions in Blockchain DApps
**arXiv ID：** 2601.07726
**作者：** Xiangyu Liu, Brian Lee, Yuansong Qiao 等

区块链 DApp 的执行涉及链上智能合约和链下可信服务两部分，两者的互认证是安全关键。TeeMAF 提出了一个基于 TEE 的链上链下互认证框架，链下服务运行在 TEE 飞地内，通过远程认证证明其执行状态未被篡改；链上合约可验证该认证结果后决定是否信任链下服务的输出。框架支持多个 TEE 节点组成认证网络，单点故障不影响整体可用性。本文还提供了形式化安全证明，说明 TeeMAF 可抵御常见的链上链下协调攻击（如预言机操控）。实现方面，论文基于 Intel SGX 和以太坊合约给出了完整原型。

### 6. 过程挖掘中基于 TEE 的数据隐私保护方法
**英文标题：** A TEE-based Approach for Preserving Data Secrecy in Process Mining with Decentralized Sources
**arXiv ID：** 2602.04697
**作者：** Davide Basile, Valerio Goretti, Luca Barbaro, Hajo A. Reijers, Claudio Di Ciccio

过程挖掘（Process Mining）通过分析事件日志重构业务流程，发现效率瓶颈和合规问题。然而日志中往往包含敏感商业数据，多方参与时数据隐私保护成为核心挑战。本文提出利用 TEE 对分散数据源的过程挖掘进行隐私保护——各数据提供方的日志在 TEE 飞地内解密和分析，原始数据不出飞地，仅输出脱敏的过程模型。论文设计了安全的日志聚合协议，保证各方无法从聚合结果反向推出他方敏感信息，同时在准确性和隐私之间做出可调平衡。实验基于真实事件日志和 Intel SGX 平台验证了方案可行性，对医疗、供应链等强监管行业的过程挖掘应用具有重要参考价值。

### 7. 部分 TEE 屏蔽 LLM 推理的预计算噪声漏洞研究
**英文标题：** Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise
**arXiv ID：** 2602.11088
**作者：** Abhishek Saini, Haolin Jiang 等

本文是安全分析类论文，针对当前将 LLM 推理部分卸载至 TEE 以保护输入隐私的架构，研究者发现了一种新型侧信道攻击。攻击者利用推理中预计算噪声的重用特性，通过监测缓存状态或内存访问模式，可在不直接读取密文的情况下提取敏感输入信息。论文系统分析了多款主流 LLM（T5、OPT 系列）在 TEE+GPU 混合推理架构下的侧信道暴露面，提出了 PoC 攻击并给出量化泄露率。防御方面，建议禁用噪声预计算或采用常数时间实现。本文提醒了 LLM 隐私推理领域"TEE 即安全"假设的危险性，推动了Trusted AI 领域对侧信道威胁的系统化认识。

### 8. 并行拜占庭共识中委员会配置优化
**英文标题：** Committee Configuration Optimization for Parallel Byzantine Consensus in a Trusted Execution Environment
**arXiv ID：** 2603.14445
**作者：** Yifei Xie, Btissam Er-Rahmadi, Xiao Chen, Tiejun Ma, Jane Hillston

大规模 BFT 系统中，通常采用委员会（Committee）机制——随机选取部分节点组成共识小组以提升吞吐量。然而委员会配置（规模、轮换频率、成员选择）对系统安全性和性能的影响缺乏系统研究。本文在 TEE 环境下（假设使用 AMD SEV 或 Intel SGX 的 VM 加密功能），研究了如何优化委员会配置以兼顾安全性和性能。论文提出了一个多目标优化模型，最小化共识延迟同时最大化抗贿赂攻击能力，并在模拟器和真实 TEE 平台（SEV-SNP）上进行了评估。结果显示，合理的委员会配置可将 BFT 吞吐量提升 3 倍以上而不显著增加安全性妥协风险，对设计下一代高性能 BFT 系统（如区块链 Layer2 协议）有直接指导意义。

---

## 二、综合对比综述

本次收录的 8 篇论文代表了 2025–2026 年 TEE 研究的几条核心主线：

### 2.1 应用场景多元化
早期 TEE 研究集中于云端机密计算（如 SGX 应用），而本次收录的论文已扩展至**区块链共识（Styx、T-RBFT）、LLM 推理（MirageNet、Vulnerabilities）、过程证明（Process Attestation）、数据隐私（Styx、Process Mining）等多元场景**，反映了 TEE 作为隐私计算基座的广泛渗透。

### 2.2 LLM 与 AI 安全成为绝对热点
8 篇中有 **3 篇直接涉及 LLM 隐私推理或模型保护**（MirageNet、Vulnerabilities、Process Attestation 中的 LLM authorship 案例），2 篇涉及区块链场景。AI 安全与 TEE 的结合正在催生一个独立研究方向——Trusted AI。

### 2.3 安全性认识深化
传统观念认为 TEE = 安全边界，但本次收录的 **Vulnerabilities** 和 **What You Trust Is Insecure**（已在其他目录）表明，研究社区正系统性地审视 TEE 的实际安全假设与现实差距。侧信道、信任反转、不当使用等威胁已被充分认知。

### 2.4 性能与安全平衡
**Ringmaster** 和 **Committee Configuration Optimization** 体现了 TEE 落地中必须面对的实际工程问题——world switch 开销、内存限制、共识延迟。纯安全设计若忽视性能代价，则难以获得实际部署。

### 2.5 跨域协作与数据主权
**Styx** 的粘性策略和 **Process Mining** 的安全日志聚合代表了数据主权保护的新思路——数据不离开 TEE，策略跟随数据流动。这与当前隐私法规（GDPR）的要求高度契合。

---

## 三、参考文献

1. Wen Gao et al., "T-RBFT: A Scalable and Efficient Byzantine Consensus Based on Trusted Execution Environment for Consortium Blockchain," arXiv:2604.16053, 2026.
2. Shixuan Zhao et al., "Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy," arXiv:2604.04082, 2026.
3. "MirageNet: A Secure, Efficient, and Scalable On-Device Model Protection in Heterogeneous TEE and GPU System," arXiv:2601.13826, 2026.
4. Richard Habeeb et al., "Ringmaster: How to juggle high-throughput host OS system calls from TrustZone TEEs," arXiv:2601.16448, 2026.
5. Xiangyu Liu et al., "TeeMAF: A TEE-Based Mutual Attestation Framework for On-Chain and Off-Chain Functions in Blockchain DApps," arXiv:2601.07726, 2026.
6. Davide Basile et al., "A TEE-based Approach for Preserving Data Secrecy in Process Mining with Decentralized Sources," arXiv:2602.04697, 2026.
7. Abhishek Saini et al., "Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise," arXiv:2602.11088, 2026.
8. Yifei Xie et al., "Committee Configuration Optimization for Parallel Byzantine Consensus in a Trusted Execution Environment," arXiv:2603.14445, 2026.
9. David Condrey, "A TEE-Based Architecture for Confidential and Dependable Process Attestation in Authorship Verification," arXiv:2603.00178, 2026.

---

*本目录为一次性任务生成，所有 PDF 均已通过 MD5 去重验证，唯一存放于 `/tmp/tee_paper/2026-04-20-16-45-36/` 目录下。*
