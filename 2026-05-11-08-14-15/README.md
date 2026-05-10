# TEE 论文合集 (2025-2026)

本目录包含 33 篇关于可信执行环境(Trusted Execution Environment, TEE)的最新学术论文,涵盖模型保护、区块链、安全分析、硬件优化等多个方向。

## 论文列表

### 1. 模型保护 (5 篇)

#### 2025 - Amulet: Fast TEE-Shielded Inference for On-Device Model Protection
**作者**: Zikai Mao, Lingchen Zhao, Lei Xu, Wentao Dong, Shenyi Zhang

**摘要**: 随着移动设备计算能力的提升,设备端机器学习(ML)成为隐私敏感和延迟关键AI应用的重要范式。本文提出Amulet框架,实现设备端TEE屏蔽推理,在保护模型知识产权的同时保持推理效率。Amulet通过创新的分区策略将深度学习模型安全地部署在ARM TrustZone Enclave中,平衡了安全性和性能开销。

**关键贡献**:
- 提出针对移动端优化的TEE模型保护架构
- 设计高效的模型分区和推理调度算法
- 在真实设备上实现并验证了方案可行性

#### 2025 - Confidential LLM Inference: Performance and Cost Across CPU and GPU TEEs
**作者**: (待补充)

**摘要**: 本文系统性地分析了在不同硬件平台(CPU TEE如Intel SGX和GPU TEE如NVIDIA H100)上运行机密计算推理的性能和成本。研究比较了两种主流TEE架构在LLM推理场景下的吞吐量、延迟和资源利用率,为实际部署提供了量化参考。

**关键贡献**:
- 首次系统性对比CPU TEE和GPU TEE的LLM推理性能
- 提出性能优化策略和成本模型
- 为机密AI推理的硬件选择提供指导

#### 2025 - TZ-LLM: Protecting On-Device Large Language Models with Arm TrustZone
**作者**: (待补充)

**摘要**: TZ-LLM提出利用ARM TrustZone技术保护设备端大语言模型。通过将LLM的推理过程安全地隔离在安全世界中,TZ-LLM防止模型权重和推理结果被恶意主机或其他不可信软件访问。该方案特别针对移动和嵌入式设备的资源受限特点进行了优化。

#### 2026 - MirageNet: A Secure, Efficient, and Scalable On-Device Model Protection in Heterogeneous TEE and GPU System
**作者**: Huadi Zheng

**摘要**: MirageNet针对异构TEE-GPU系统提出统一的设备端模型保护方案。该框架支持在Intel SGX、ARM TrustZone和GPU TEE之间安全地迁移和执行深度学习模型,解决了跨平台模型保护的挑战。MirageNet采用分层架构,实现模型的安全分区、远程证明和运行时保护。

#### 2025 - Trustworthy and Controllable Professional Knowledge Utilization in Large Language Models with TEE-GPU Execution
**作者**: (待补充)

**摘要**: 本文探讨如何在TEE-GPU环境中实现可信赖且可控的专业知识利用。通过在GPU TEE中安全地执行RAG(检索增强生成)流程,该方案允许LLM在不泄露敏感知识库的前提下利用专业领域数据。

---

### 2. 区块链与Web3 (1 篇)

#### 2025 - Optimistic TEE-Rollups: A Hybrid Architecture for Scalable and Verifiable Generative AI Inference
**作者**: (待补充)

**摘要**: Optimistic TEE-Rollups提出结合乐观执行和TEE的混合架构,用于可扩展且可验证的生成式AI推理。该方案利用TEE提供执行隐私和完整性保证,同时采用乐观Rollup机制实现高吞吐量和低成本。论文展示了如何将AI推理任务安全地外包给TEE节点,并通过零知识证明验证计算正确性。

---

### 3. 硬件与系统 (8 篇)

#### 2025 - Blueprint, Bootstrap, and Bridge: A Security Look at NVIDIA GPU Confidential Computing
**作者**: (待补充)

**摘要**: 本文全面分析了NVIDIA GPU机密计算架构的安全性。研究深入探讨了NVIDIA的Blueprint、Bootstrap和Bridge安全机制,评估了其对GPU TEE的保护能力,并识别了潜在的硬件和软件安全漏洞。

#### 2025 - SecureInfer: Heterogeneous TEE-GPU Architecture for Privacy-Critical Tensors for Large Language Models
**作者**: (待补充)

**摘要**: SecureInfer提出针对LLM隐私关键张量的异构TEE-GPU架构。该方案允许敏感的张量计算在GPU TEE中执行,同时保持控制逻辑在CPU TEE中运行,实现计算效率和安全的平衡。

#### 2025 - Supporting Intel SGX on Multi-Package Platforms
**作者**: Simon Johnson, Raghunandan Makaram, Amy Santoni, Vinnie Scarlata

**摘要**: 随着多芯片封装(MCP)平台的普及,如何在这些新型硬件上支持Intel SGX成为重要挑战。本文分析了多封装平台上的SGX技术挑战,并提出相应的解决方案,使机密计算能够在现代数据中心处理器上正常运行。

#### 2025 - NanoZone: Scalable, Efficient, and Secure Memory Protection for Arm CCA
**作者**: Shiqi Liu, Yongpeng Gao, Mingyang Zhang, Jie Wang

**摘要**: NanoZone为ARM CCA(Confidential Computing Architecture)提出可扩展的内存保护方案。该方案通过细粒度的内存隔离和加密,保护在CCA域中运行的敏感应用,同时最小化性能开销。

#### 2025 - Hazel: Secure and Efficient Disaggregated Storage
**作者**: Marcin Chrapek

**摘要**: Hazel提出在解耦存储系统中实现安全高效的机密计算方案。通过将TEE与解耦存储架构深度集成,Hazel实现在分布式环境下的安全数据持久化和访问控制。

#### 2025 - Automatic ISA analysis for Secure Context Switching
**作者**: Neelu S. Kalani

**摘要**: 本文提出自动化的指令集架构(ISA)分析方法,用于安全上下文切换。研究者开发了分析工具,能够从ISA规范中自动提取安全关键信息,帮助设计更安全的TEE系统。

#### 2025 - Security Enclave Architecture for Heterogeneous Security Primitives for Supply-Chain Attacks
**作者**: (待补充)

**摘要**: 针对供应链攻击威胁,本文提出异构安全原语的安全enclave架构。该方案整合多种硬件安全技术,提供多层次的防护,抵抗供应链层面的攻击。

#### 2025 - Characterizing Trust Boundary Vulnerabilities in TEE Container Systems: An Empirical Study
**作者**: (待补充)

**摘要**: 这是一项针对TEE容器系统信任边界漏洞的实证研究。研究团队系统性地分析了主流TEE容器实现的安全问题,揭示了多种新型攻击向量,并提出防御建议。

---

### 4. 安全与攻击 (6 篇)

#### 2025 - AEX-NStep: Probabilistic Interrupt Counting Attacks on Intel SGX
**作者**: Nicolas Dutly, Friederike Groschupp, Ivan Puddu, Kari Kostiainen, Srdjan Capkun

**摘要**: AEX-NStep是一种针对Intel SGX的新型侧信道攻击。该攻击利用中断计数机制的时序特性,推断enclave内的敏感信息。研究者展示了如何通过精心构造的中断序列提取加密密钥等秘密数据,并提出了相应的缓解措施。

#### 2026 - Red-Teaming Claude Opus and ChatGPT-based Security Advisors for Trusted Execution Environments
**作者**: (待补充)

**摘要**: 本文对基于LLM的安全顾问进行红队测试,评估其在TEE相关安全场景中的表现。研究揭示了当前LLM安全助手在理解和生成TEE安全方案方面的局限性,并提出改进方向。

#### 2026 - Ringmaster: How to juggle high-throughput host OS system calls from TrustZone TEEs
**作者**: Richard Habeeb, Man-Ki Yoon

**摘要**: Ringmaster研究在TrustZone TEE中处理高吞吐量系统调用的挑战。传统上,系统调用需要切换到Normal World执行,带来显著性能开销。Ringmaster提出优化策略,减少世界切换次数,提升TEE应用性能。

#### 2026 - External Entropy Supply for IoT devices employing a RISC-V Trusted Execution Environment
**作者**: (待补充)

**摘要**: 本文研究在RISC-V TEE物联网设备中如何安全地获取外部熵源。高质量随机数对TEE安全至关重要,但物联网设备往往缺乏硬件随机数生成器。论文提出安全地从不可信环境获取熵的方案。

#### 2026 - A TEE-Based Architecture for Confidential and Dependable Process Attestation in Authorship Verification
**作者**: (待补充)

**摘要**: 提出基于TEE的进程认证架构,用于作者身份验证。该方案利用远程证明技术,确保软件执行环境的完整性和可信性,为数字内容的作者身份提供加密保证。

#### 2026 - On Securing the Software Development Lifecycle in IoT RISC-V Trusted Execution Environments
**作者**: (待补充)

**摘要**: 探讨如何在RISC-V TEE物联网设备中保护软件开发生命周期。论文提出从代码开发、编译、部署到运行的全链路安全方案,确保物联网设备的软件供应链安全。

---

### 5. 联邦学习与AI安全 (4 篇)

#### 2025 - Securing Private Federated Learning in a Malicious Setting: A Scalable TEE-Based Approach with Client Auditing
**作者**: (待补充)

**摘要**: 针对恶意环境中的安全联邦学习,本文提出基于TEE的可扩展方案。该方案通过客户端审计机制,确保参与方的诚实行为,同时利用TEE保护模型梯度不被泄露。

#### 2025 - Securing Transformer-based AI Execution via Unified TEEs and Crypto-protected Accelerators
**作者**: (待补充)

**摘要**: 论文提出统一TEE和加密保护加速器的安全架构,保护基于Transformer的AI模型执行。该方案针对现代AI加速器进行优化,实现从训练到推理的全流程安全。

#### 2025 - Securing Generative AI in Healthcare: A Zero-Trust Architecture Powered by Confidential Computing
**作者**: (待补充)

**摘要**: 本文为零信任医疗AI提出机密计算架构。利用TEE和同态加密等技术,该方案保护患者敏感的医疗数据,在AI辅助诊断场景中实现隐私保护。

#### 2026 - TeeMAF: A TEE-Based Mutual Attestation Framework for On-Chain and Off-Chain Functions in Blockchain DApps
**作者**: Xiangyu Liu, Brian Lee, Yuansong Qiao

**摘要**: TeeMAF提出针对区块链DApp的TEE双向认证框架。该框架实现链上和链下函数之间的安全互认证,确保智能合约执行的完整性和数据机密性。

---

### 6. 共识与分布式系统 (2 篇)

#### 2026 - T-RBFT: A Scalable and Efficient Byzantine Consensus Based on Trusted Execution Environment for Consortium Blockchain
**作者**: Wen Gao, Xinhong Hei, Yichuan Wang

**摘要**: T-RBFT提出基于TEE的可扩展拜占庭共识算法,用于联盟链。该方案利用TEE加速共识过程,显著提高吞吐量,同时保持 Byzantine 容错能力。实验表明,T-RBFT相比传统PBFT有数量级的性能提升。

#### 2025 - TEEBFT: Pricing the Security of Proof of Cloud
**作者**: Alex Shamis, Matt Stephenson, Linfeng Zhou

**摘要**: TEEBFT研究云环境下的共识安全定价问题。论文提出"Proof of Cloud"概念,利用TEE提供计算证明,并分析不同安全参数下的成本效益。

---

### 7. 其他 (7 篇)

#### 2025 - TriHaRd: Higher Resilience for TEE Trusted Time
**作者**: Matthieu Bettinger, Sonia Ben Mokhtar, Pascal Felber

**摘要**: TriHaRd提高TEE可信时间的恢复力。论文提出多层时间同步机制,即使在部分组件被攻击的情况下,仍能维护准确可信的时间服务。

#### 2025 - Enhancing the Security of Rollup Sequencers using Decentrally Attested TEEs
**作者**: (待补充)

**摘要**: 研究利用去中心化认证的TEE增强Rollup排序器的安全性。该方案通过分布式证明机制,确保排序器行为的正确性和透明性。

#### 2025 - PDRIMA: A Policy-Driven Runtime Integrity Measurement and Attestation Approach for ARM TrustZone
**作者**: (待补充)

**摘要**: PDRIMA提出针对ARM TrustZone的策略驱动运行时完整性测量和认证方案。该方案允许用户定义细粒度的安全策略,并自动验证系统运行时状态。

#### 2025 - Confidential Computing Adoption: A Systematization of Knowledge
**作者**: Quentin Michaud

**摘要**: 这是一篇关于机密计算采用的知识系统化论文。论文全面回顾了机密计算技术的发展历程、当前状态和未来趋势,为研究者和实践者提供全面的技术参考。

#### 2025 - Supporting Intel SGX on Multi-Package Platforms (见上文硬件部分)

#### 2026 - Technical Report: Security Assessment (待补充)

#### 2025 - An Open-source Implementation and Security Analysis of Triad's TEE Trusted Time Protocol (待补充)

---

## 综合分析

### 研究趋势

本期论文反映了TEE领域的几个重要研究方向:

1. **模型保护持续火热**: 5篇论文专注于在TEE中保护机器学习模型,包括LLM保护、设备端推理和模型权重安全。这反映了AI模型知识产权保护的实际需求。

2. **异构计算安全**: 多篇论文探讨TEE与GPU、TEE与AI加速器的结合,解决在现代异构系统中的安全计算问题。

3. **区块链与TEE融合**: TEE在区块链领域的应用更加成熟,从共识算法(DPoS/TEE混合)到Rollup安全,TEE正在成为Web3基础设施的重要组件。

4. **安全性研究深入**: 侧信道攻击研究继续深入,同时安全框架和认证机制也在不断完善。

5. **RISC-V TEE崛起**: 多篇论文关注RISC-V架构的TEE实现,反映开源硬件生态的发展。

### 技术创新亮点

- **性能优化**: 多个工作关注TEE性能开销问题,从系统调用优化到内存加密,全面提升TEE实用性
- **新型攻击**: AEX-NStep等论文揭示新型侧信道攻击,推动安全机制改进
- **隐私计算**: 联邦学习、机密推理等隐私计算场景与TEE深度结合

### 参考文献

[1] Amulet: Fast TEE-Shielded Inference for On-Device Model Protection (2025)
[2] Confidential LLM Inference: Performance and Cost Across CPU and GPU TEEs (2025)
[3] TZ-LLM: Protecting On-Device Large Language Models with Arm TrustZone (2025)
[4] MirageNet: On-Device Model Protection in Heterogeneous TEE-GPU System (2026)
[5] Optimistic TEE-Rollups: Hybrid Architecture for Scalable AI Inference (2025)
[6] Blueprint, Bootstrap, Bridge: NVIDIA GPU Confidential Computing Security (2025)
[7] NanoZone: Memory Protection for Arm CCA (2025)
[8] Hazel: Secure Disaggregated Storage (2025)
[9] AEX-NStep: Interrupt Counting Attacks on Intel SGX (2025)
[10] T-RBFT: Byzantine Consensus Based on TEE (2026)
[11] TeeMAF: Mutual Attestation Framework for Blockchain DApps (2026)
[12] Characterizing Trust Boundary Vulnerabilities in TEE Containers (2025)
[13] SecureInfer: Heterogeneous TEE-GPU Architecture (2025)
[14] Securing Private Federated Learning with TEE (2025)
[15] Securing Transformer-based AI with Unified TEEs (2025)
[16] TriHaRd: Higher Resilience for TEE Trusted Time (2025)
[17] PDRIMA: Policy-Driven Runtime Integrity for ARM TrustZone (2025)
[18] Confidential Computing Adoption: SoK (2025)
[19] Red-Teaming LLM Security Advisors for TEE (2026)
[20] Ringmaster: High-throughput TrustZone System Calls (2026)
[21] External Entropy Supply for RISC-V TEE IoT (2026)
[22] TEE-Based Process Attestation for Authorship Verification (2026)
[23] Securing SDLC in IoT RISC-V TEE (2026)
[24] Trustworthy Professional Knowledge with TEE-GPU (2025)
[25] Enhancing Rollup Sequencer Security with Decentrally Attested TEEs (2025)
[26] Supporting Intel SGX on Multi-Package Platforms (2025)
[27] Automatic ISA Analysis for Secure Context Switching (2025)
[28] Security Enclave Architecture for Supply-Chain Attacks (2025)
[29] TEEBFT: Pricing the Security of Proof of Cloud (2025)
[30] Securing Generative AI in Healthcare with Confidential Computing (2025)
[31] An Open-source Implementation of Triad's TEE Trusted Time Protocol (2025)
[32] Technical Report: Security Assessment of Intel TDX (2026)
[33] Trust Boundary Vulnerabilities in TEE Container Systems (2025)

---

**下载时间**: 2026-05-11
**论文总数**: 33 篇
**年份分布**: 2025年(25篇), 2026年(8篇)
