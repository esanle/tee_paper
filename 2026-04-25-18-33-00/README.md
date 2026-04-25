# TEE 论文综述 - 2026-04-25 批次

本目录包含 2026 年 4 月 25 日下载的 6 篇可信执行环境（TEE）相关论文，涵盖 AI 安全审计、模型保护、分布式账本、联邦学习、信息物理系统安全和云安全等领域。

---

## 论文概要

### 1. Attestable Audits: Verifiable AI Safety Benchmarks Using Trusted Execution Environments

**作者：** Christoph Schnabl, Daniel Hugenroth, Bill Marino, Alastair R. Beresford（剑桥大学计算机科学与技术系）

**发表：** ICML 2025（第 42 届国际机器学习会议）

**核心问题：** 随着 AI 模型能力不断增强，各国监管框架（如 EU AI Act、美国行政命令）纷纷要求对 AI 系统进行安全审计。然而，当前审计流程存在根本性缺陷：审计结果不可验证、模型知识产权和基准数据集缺乏保密性、利益相关方之间存在信任鸿沟。如何在不暴露模型权重的前提下，让用户能够可信地验证他们交互的 AI 系统已经通过了合规安全审计？

**技术方案：** 论文提出"可验证审计"（Attestable Audits）协议，利用可信执行环境（TEE）构建三步验证框架。第一步，审计师和模型提供方分别将加密的审计代码/数据集和 AI 模型加载到独立的硬件级 TEE 中。第二步，在 TEE 内部运行基准测试，TEE 的机密计算特性保证执行过程不受宿主操作系统或管理程序的干扰，所有内存内容经过加密。第三步，审计结果通过远程证明（Remote Attestation）技术进行密码学签名，并发布到公共透明日志中，用户可独立验证。整个流程基于 AWS Nitro Enclaves（第二代 VM 级 TEE）实现原型，克服了第一代 TEE（如 Intel SGX）内存受限的问题。

**实验评估：** 作者在 Llama-3.1 模型上运行典型安全审计基准测试，结果显示 TEE 内执行的开销为 CPU 推理的 2.2 倍、GPU 推理的 21.7 倍。虽然 GPU 推理开销较高，但考虑到安全审计不要求实时性，这个代价是可接受的。作者还详细分析了 TEE 证明链的完整性，包括平台配置寄存器（PCR）的度量机制和零知识证明式保证。

**贡献与意义：** 这项工作填补了 AI 治理政策与技术实现之间的关键空白。它首次提出了一个在模型提供方不共享权重、审计师仅与监管方共享代码和数据、且运行在不可信第三方基础设施上的现实约束条件下仍然可行的验证方案。该方案直接回应了 EU AI Act 和 NIST AI RMF 等框架提出的技术审计需求。

---

### 2. TEESlice: Protecting Sensitive Neural Network Models in Trusted Execution Environments When Attackers Have Pre-Trained Models

**作者：** Ding Li, Ziqi Zhang, Mengyu Yao, Yifeng Cai, Yao Guo, Xiangqun Chen（北京大学高可信软件技术教育部重点实验室）

**发表：** ACM Transactions on Software Engineering and Methodology (TOSEM), 2025

**核心问题：** 在端侧设备上部署的深度神经网络（DNN）模型面临严重的安全威胁——恶意用户可以直接访问模型的白盒信息（权重值），从而轻松实施模型窃取（Model Stealing, MS）和成员推理攻击（Membership Inference Attack, MIA）。TEE 虽然可以保护模型，但直接将整个 DNN 放入 TEE 会导致 50 倍的性能下降。现有的 TEE 屏蔽 DNN 划分（TSDP）方案将模型分为敏感和非敏感部分，但忽略了攻击者可以利用大量公开预训练模型这一现实威胁。

**技术方案：** TEESlice 提出了一种"训练前划分"（partition-before-training）策略，与传统"训练后划分"方法根本不同。核心思想是在训练阶段就将隐私敏感的权重与其他模型组件有效分离。具体而言，该方法首先识别模型中哪些功能对隐私最为关键，然后通过特殊的训练策略将这些功能压缩到轻量级的"切片"中，这些切片可以在 TEE 内高效运行，而模型的其余部分则在 GPU 上执行。对于大语言模型（LLM），TEESlice 同样适用——可以将私有功能压缩为轻量级切片，实现与屏蔽整个模型相同级别的保护。

**安全分析：** 论文深入分析了在"知识型对手"（knowledgeable adversary）威胁模型下现有 TSDP 方案的脆弱性。知识型对手可以利用互联网上大量公开可用的预训练模型和数据集，显著提升攻击效果。实验表明，现有方法在面对此类对手时无法兑现其安全承诺。TEESlice 通过在训练阶段就建立隔离，从根本上解决了这一问题。

**实验评估：** 在 CNN 和 LLM 上的评估表明，TEESlice 能够提供完整的模型保护，同时将计算成本降低 10 倍。与传统屏蔽整个模型方案相比，TEESlice 在安全性上不妥协，在性能上大幅提升。该方法已验证可扩展到大型语言模型。

**贡献与意义：** 这是一项非常系统深入的工作（49 页），首次揭示了预训练模型时代下 TSDP 方案的安全盲区，并提出了切实可行的解决方案。将模型保护从"训练后补救"转向"训练时设计"的范式转换具有重要意义。

---

### 3. CyFence: Securing Cyber-physical Controllers Via Trusted Execution Environment

**作者：** Stefano Longari, Alessandro Pozone, Jessica Leoni, Mario Polino, Michele Carminati, Mara Tanelli, Stefano Zanero（米兰理工大学电子与信息系）

**发表：** arXiv:2506.10638, 2025（投稿中）

**核心问题：** 信息物理系统（CPS）在过去几十年经历了巨大的技术进步，但也带来了日益增长的网络安全风险。由于许多 CPS 用于安全关键场景（如汽车防抱死制动系统 ABS、工业机器人），网络攻击可能导致严重的人身伤害。现有防御策略大多从传统 IT 安全领域移植而来，很少充分利用 CPS 本身的物理反馈特性。

**技术方案：** CyFence 提出了一种新颖的架构，利用 CPS 的物理反馈本质来增强闭环控制系统对网络攻击的韧性。核心思想是在控制回路中添加一个"语义检查"（semantic check）模块，该模块基于系统的物理模型验证控制器输出的合理性。语义检查代码运行在 TEE 内，确保即使主系统被攻破，安全检查逻辑仍然可信。当检测到异常控制指令时，CyFence 可以触发安全降级或停机保护。TEE 的使用保证了安全检查代码的完整性和机密性，防止攻击者篡改或绕过安全机制。

**实验评估：** 作者以真实世界的主动制动数字控制器为测试场景进行评估。实验证明 CyFence 能够有效缓解多种类型的攻击，且计算开销几乎可以忽略不计。这得益于语义检查基于预计算的物理模型边界，运行时只需要简单的数值比较。

**贡献与意义：** 这项工作的创新之处在于将 TEE 安全与物理模型语义相结合，开创了"物理感知安全"（physics-aware security）的新范式。与传统的加密通信、安全启动等方案不同，CyFence 不仅保护通信和代码完整性，还通过物理一致性检查来检测攻击，为安全关键 CPS 提供了纵深防御。

---

### 4. A Performance Analysis of VM-based Trusted Execution Environments for Confidential Federated Learning

**作者：** Bruno Casella 等（都灵大学计算机科学系 Alpha 研究组）

**发表：** PDP 2025（第 33 届 Euromicro 国际并行、分布式和基于网络的计算会议）

**核心问题：** 联邦学习（FL）在利用第三方云计算和高性能计算（HPC）资源时面临严峻的安全挑战。第一代 TEE（如 Intel SGX、ARM TrustZone）存在诸多限制：受保护的内存容量有限、不支持 GPU、代码移植困难、运行时开销显著。新一代基于虚拟机的 TEE（如 Intel TDX）能否有效解决这些问题，使机密联邦学习（CFL）成为默认部署模式？

**技术方案：** 本文对 Intel TDX 这一新一代 VM 级 TEE 进行了系统性的基准测试，将其与 Intel SGX 在联邦学习场景下的性能进行全面比较。Intel TDX 提供整个虚拟机级别的隔离，而非 SGX 的进程级隔离，从而克服了内存限制和 GPU 兼容性问题。实验在三个图像分类数据集和两种不同的神经网络上进行广泛的 CFL 实验。

**实验评估：** 研究发现 VM 级 TEE 对运行时开销的影响很小，相比 SGX 有显著改善。SGX 在 CFL 场景中可能引入 2-3 倍的开销（如 PPFL 方案），而 TDX 的开销接近原生性能。这一结果表明基于 VM 的 TEE 有望成为部署 AI 模型的默认安全模式，特别是在大语言模型（LLM）时代，需要依赖不可信的 HPC 和云设施时。

**贡献与意义：** 这项工作为 CFL 从研究走向实际部署提供了重要的性能基准。结论表明，新一代 VM 级 TEE 已经克服了第一代 TEE 的主要技术瓶颈，使"默认安全"的联邦学习部署成为可能。

---

### 5. Confidential Computing for Cloud Security: Exploring Hardware based Encryption Using Trusted Execution Environments

**作者：** Dhruv Deepak Agarwal, Aswani Kumar Cherukuri（韦洛尔理工学院计算机科学与工程系）

**发表：** 2025

**核心问题：** 云计算的数据处理和存储能力带来了前所未有的可扩展性和灵活性，但同时也带来了严重的安全挑战。数据在使用过程中（data-in-use）的加密保护一直是三大安全支柱中最薄弱的环节（数据传输中和存储中的保护相对成熟）。TEE 和机密计算能否系统地解决云端数据全生命周期安全问题？

**技术方案：** 本文是一篇系统性综述，全面梳理了基于硬件加密的机密计算技术在云安全中的应用。涵盖了 AMD SEV（Secure Encrypted Virtualization）、Intel SGX、Intel TDX、ARM TrustZone 等主流 TEE 技术。论文从架构层面分析了加密容器（如 Singularity）、加密虚拟机、加密存储（如 Quobyte 的 AES-XTS）和资源隔离（如 OpenStack）等多种安全机制的组合方案。

**文献综述：** 论文提供了详细的文献对比表，从安全机制、目标平台、性能指标和评估方法四个维度系统化比较了现有研究。涵盖了加密云架构、CPU-GPU TEE 推理评估、TEE 框架（如 LuaGuardia、HasTEE/HasTEE+）和性能基准（如 TS-Perf）等多个方向。

**挑战分析：** 论文深入分析了 TEE 在云环境中面临的挑战：缺乏跨平台标准化开发框架、安全 I/O 处理困难、证明机制碎片化、回滚/重放攻击风险、以及大规模云端和边缘系统中的生命周期管理复杂性。同时也讨论了 TEE 的商业价值，包括 GDPR/HIPAA 合规、远程证明和多云环境下的信任建立。

**贡献与意义：** 作为一篇综述性工作，它为研究者和工程师提供了进入机密计算领域的系统性入口，特别适合快速了解 TEE 技术全景和当前研究热点。

---

### 6. Proteus: Append-Only Ledgers for (Mostly) Trusted Execution Environments

**作者：** Shubham Mishra, João Gonçalves, Chawinphat Tankuranand, Neil Giridharan, Natacha Crooks, Heidi Howard, Chris Jensen（UC Berkeley, Microsoft Azure Research, IST U. Lisboa & INESC-ID）

**发表：** 2026

**核心问题：** 分布式账本越来越被行业用于提供可信赖的问责、强完整性保护和高可用性。当前的 TEE 增强共识协议存在一个根本性问题：如果 TEE 被攻破，攻击者可以分叉整个日志而不会被检测到（除非客户端主动干预）。如何构建一种分布式账本，在正常情况下享受 TEE 带来的高性能，同时在 TEE 被攻破时仍能提供强有力的安全保证？

**技术方案：** Proteus 提出了"平台容错"（platform-fault-tolerance）这一新的故障模型。在该模型中，系统由多个独立平台（信任域）组成，每个平台包含若干节点。节点可能独立崩溃，但 TEE 漏洞会危及整个平台。核心创新是将 BFT（Byzantine Fault Tolerance）协议嵌入到 CFT（Crash Fault Tolerance）协议内部：前台使用简化的 CFT 协议（如 Raft）快速提交操作，后台同时运行 BFT 审计来检测 TEE 被攻破导致的状态分叉。

**关键技术：** Proteus 复用了三项关键 BFT 技术：(1) 借鉴 Upright 的平台概念来建模故障域；(2) 增量化仲裁（incremental quorums）——利用哈希链确保对某个批次投票等同于对其所有前驱批次投票，迟到的投票可以补完旧的仲裁；(3) 将流水线与增量仲裁结合，确保 BFT 审计永远不会落后 CFT 共识超过一个常数边界，从而将攻击的"爆炸半径"限制在已提交但未审计的日志尾部。

**实验评估：** Proteus 的吞吐量和延迟与当前 TEE 账本（包括签名版 Raft 和微软 CCF）相当，但提供了更强的安全保证。审计延迟比 Autobahn（最先进的 BFT 协议）低 15%，吞吐量仅损失 11%。在五个应用上的评估表明，用户可以灵活地在普通提交和增强审计之间导航。

**贡献与意义：** Proteus 首次实现了"TEE 正常时高性能、TEE 被攻破时仍可检测"的优雅折中，避免了当前方案"要么全信、要么全废"的两难选择。这对于生产级分布式信任系统（如 Azure Confidential Ledger、Signal SVR3）具有重要的实际价值。

---

## 对比综述

本批次六篇论文从不同维度展示了 TEE 技术在 2025-2026 年的前沿进展。以下从应用场景、威胁模型、TEE 使用方式和性能权衡四个角度进行交叉对比分析。

### 应用场景的多元化

六篇论文覆盖了 TEE 技术的广阔应用谱系。**Proteus** 和 **Attestable Audits** 关注高完整性保证的审计场景——前者用于分布式账本的状态审计，后者用于 AI 模型的安全合规审计，两者都利用 TEE 的完整性（integrity）属性而非仅仅依赖机密性。**TEESlice** 和 **Casella 等人的性能分析**聚焦于机器学习场景，前者解决端侧模型保护问题，后者评估联邦学习在 VM 级 TEE 中的性能表现。**CyFence** 将 TEE 引入安全关键的信息物理系统，开辟了 TEE 在物理控制回路中的新应用。**Agarwal 和 Cherukuri 的综述**则提供了整个领域的全景视图。

### 威胁模型的演进

一个显著趋势是威胁模型的持续强化。**TEESlice** 突破性地考虑了"知识型对手"——攻击者可以获取大量公开预训练模型和公开数据集，这一威胁模型在 LLM 时代尤其现实。现有 TSDP 方案在此威胁模型下完全失效，因为攻击者可以通过预训练模型推断出被保护模型的敏感信息。**Proteus** 假设 TEE 可能在某些平台被攻破（而非假设 TEE 完全可信），这与行业实践中频发的 TEE 侧信道攻击和微架构漏洞（如 BadRAM、Plundervolt 等）相呼应。**CyFence** 则面对 CPS 场景中攻击者可能已经控制操作系统的现实威胁。

### TEE 使用方式的差异

六篇论文在 TEE 的使用方式上呈现有趣的差异。**Attestable Audits** 使用第二代 VM 级 TEE（AWS Nitro Enclaves），利用其较大的内存容量来运行完整的 LLM 推理。**TEESlice** 针对资源受限的端侧设备，只将模型的轻量级"切片"放入 TEE。**Proteus** 将 TEE 作为分布式共识的信任锚，多个独立 TEE 平台共同维护账本完整性。**CyFence** 将 TEE 用于保护安全检查代码的完整性，而非保护主控制逻辑——这是一种最小化 TCB 的设计哲学。**Casella 等人**的系统对比表明，VM 级 TEE（Intel TDX）相比进程级 TEE（Intel SGX）在联邦学习场景中具有显著优势，特别是在 GPU 兼容性和内存容量方面。

### 性能与安全的权衡

性能开销始终是 TEE 应用中的核心矛盾。**TEESlice** 通过"训练前划分"策略将计算成本降低 10 倍，**Proteus** 通过将 BFT 审计嵌入 CFT 协议在几乎不牺牲性能的情况下提供更强的安全保证。**Casella 等人**的基准测试表明新一代 VM 级 TEE 已经将性能开销降低到接近原生水平。**CyFence** 的语义检查基于预计算的物理模型边界，运行时开销几乎可忽略。**Attestable Audits** 的 GPU 推理开销（21.7 倍）虽然较高，但考虑到审计的非实时性，这一代价在可接受范围内。

### 跨论文交叉引用

值得注意的技术传承关系包括：**TEESlice** 的模型划分思想与 **Casella 等人**评估的 CFL 场景形成互补——前者保护端侧模型，后者保护训练过程。**Proteus** 的平台容错模型与 **Attestable Audits** 都依赖远程证明（Remote Attestation）技术，但用途不同——前者用于共识协议的正确性验证，后者用于 AI 系统的合规性验证。**CyFence** 的"最小化 TCB"哲学与 **TEESlice** 的"只保护敏感切片"思想在系统设计层面异曲同工。**Agarwal 和 Cherukuri 的综述**中提到的 TS-Perf 基准和 HasTEE 框架为 **Casella 等人**的性能评估提供了方法论基础。

---

## 总结

本批次论文共同描绘了 TEE 技术在 2025-2026 年的关键发展趋势：(1) 从第一代进程级 TEE 向第二代 VM 级 TEE 的迁移正在实质性降低性能开销，使 TEE 在 ML 和分布式系统中的广泛部署成为可能；(2) 威胁模型持续强化，研究者不再假设 TEE 完全可信，而是在 TEE 可能被部分攻破的前提下设计系统；(3) TEE 的应用场景正在从传统的数据保护扩展到 AI 治理、物理系统安全和分布式信任等新领域；(4) "最小化 TCB"的设计哲学被广泛采纳，从模型切片到语义检查代码，研究者都在尝试将 TEE 保护聚焦在最关键的组件上。
