# TEE 论文综述 — 2026-04-12-12-41-20

> 本批次 16 篇论文均为**重复下载**（已存在于其他时间戳目录），已统一重命名并去重。

## 综述（Comparative Synthesis）

本批次 16 篇论文涵盖 2025—2026 年可信执行环境（TEE）研究的前沿方向，可归纳为以下几个主题：

### 1. TEE 生态抽象与标准化

以 [Abstraction-2025] 为代表，系统性梳理了 Intel SGX、AMD SEV、ARM TrustZone/CCA、RISC-V Keystone 等异构 TEE 平台的抽象层方案，论证了 WebAssembly 作为统一运行时的优势。[TEEBFT-2025] 则从量化角度评估不同 TEE 实现的安全强度，为跨平台选择提供依据。[AutoTEE-2025] 通过 LLM 自动化降低 TEE 迁移门槛，与 [WhatYouTrust-2025] 揭示的开发者误用问题形成对照——前者用自动化解决"不会用"，后者提醒即使自动化也需要安全工程实践。

### 2. LLM 与 TEE 的深度融合

这是本批次最集中的主题。[VulnerabilitiesLLM-2026] 和 [RedTeaming-2026] 揭示了 TEE-Shielded LLM 部署中的新型攻击面——前者针对预计算噪声的侧信道，后者针对 LLM 自身的提示注入风险。[Styx-2026] 提出了支持粘性策略的多方 LLM 协作框架。整体趋势是：学界已经从"LLM in TEE"的存在性研究，转向对具体攻击面和实用安全协作机制的深入挖掘。

### 3. 垂直行业应用深化

本批次出现了多个强行业导向的工作：[PMDedup-2025] 针对云边协同场景的加密去重；[DecisionSupport-2025] 针对医疗决策支持；[ReplicationCrisis-2026] 独辟蹊径将 TEE 应用于科研诚信；[SpaceFabric-2026] 拓展至卫星通信领域；[IoTRISC-VSDLC-2026] 和 [ExternalEntropy-2026] 则专注物联网 RISC-V 生态的安全开发与熵源供给。这些工作共同指向一个趋势：TEE 正在从通用安全底座走向领域深度定制。

### 4. 信任工作流与去中心化系统

[SharingIsCaring-2026] 提出了跨不信任组件构建可认证工作流的框架。[TEEBFT-2025] 为 PoS 区块链的 TEE 集成提供量化安全模型。[ProcessAttestation-2026] 将 TEE 应用于著作权验证。这些工作共同探讨了如何在缺乏全局可信第三方的环境中建立局部信任链。

---

## 各论

### 1. PM-Dedup: Secure Deduplication with Partial Migration from Cloud to Edge Servers
**arXiv**: `2501.02350` | **年份**: 2025
**作者**: Zhaokang Ke, Haoyu Wang, David H.C. Du — University of Minnesota

**摘要**：本文针对云边协同场景下的加密数据去重问题，提出了一种名为 PM-Dedup 的新型安全源端去重方案。传统加密去重技术面临两大挑战：一是目标端去重需要客户端上传所有密文块，带宽开销大；二是源端去重虽可减少上传量，但引入侧信道攻击风险和高计算开销。PM-Dedup 的核心思想是将去重检查和所有权证明（PoW）任务从云端迁移到客户端边缘服务器的 TEE 可信执行环境中执行，从而在保证安全性的同时显著降低网络延迟和云端计算开销。作者设计了多种优化方案来增强安全性和效率，包括在 TEE 内完成指纹比较和 PoW 验证，避免敏感数据暴露给不可信的云端操作系统。实验结果表明，PM-Dedup 在保证数据机密性和完整性的前提下，能够有效减少网络传输量，适合边缘计算和云存储协同场景。

**主要贡献**：
- 提出基于 TEE 的源端加密去重框架
- 将 PoW 任务卸载到边缘 TEE
- 显著降低网络带宽和云端计算开销
- 形式化安全分析

**引用**: [PMDedup-2025]

---

### 2. AutoTEE: Automated TEE Adaptation with LLMs — Identifying, Transforming, and Porting Sensitive Functions in Programs
**arXiv**: `2502.13379` | **年份**: 2025
**作者**: Chen et al.

**摘要**：本文针对 TEE 应用开发的高门槛问题，提出 AutoTEE，一个利用大语言模型（LLM）自动将普通程序中的敏感函数迁移到 TEE 可信执行环境的系统。TEE 开发需要开发者深入理解特定硬件平台的 enclave 模型、接口和限制，学习曲线陡峭。AutoTEE 通过 LLM 自动分析程序代码，识别适合放入 TEE 的敏感函数（如密钥管理、隐私数据处理），并自动完成代码转换和移植工作。作者构建了一个包含多种 TEE 平台（Intel SGX、ARM TrustZone）的基准测试集，评估了 AutoTEE 在识别准确率、转换正确性和移植效率方面的表现。实验表明，AutoTEE 能够显著降低 TEE 应用开发的人力成本，同时保持较高的迁移正确率，为非 TEE 专家开发者提供了实用的自动化工具。

**主要贡献**：
- LLM 驱动的 TEE 敏感函数自动识别
- 自动化代码转换与移植
- 多 TEE 平台支持
- 降低 TEE 开发门槛

**引用**: [AutoTEE-2025]

---

### 3. An Open-source Implementation and Security Analysis of Triad's TEE Trusted Time Protocol
**arXiv**: `2507.20851` | **年份**: 2025
**作者**: Matthieu Bettinger, Sonia Ben Mokhtar, Anthony Simonet-Boulogne et al.

**摘要**：本文对 Triad 团队提出的 TEE 可信时间协议（Trusted Time Protocol）进行了完整的开源实现和安全分析。在分布式系统和区块链场景中，不同节点需要就时间顺序达成共识，但依赖不可信外部时间源会带来安全隐患。Triad 的方案利用 TEE 硬件创建一个可信的时间参考框架，节点可通过远程证明验证时间信息的真实性。本文作者实现了该协议的开源版本，并通过系统性的安全分析，验证了其在防止时间操纵攻击、保证时间同步一致性方面的安全属性。研究还发现了原协议在某些边界条件下的一些潜在弱点，并提出了相应的改进建议，为可信时间服务在分布式系统中的实际部署提供了重要参考。

**主要贡献**：
- Triad TTP 开源实现
- 系统性安全分析
- 发现边界条件弱点
- 提出改进方案

**引用**: [Triad-2025]

---

### 4. A TEE-based Approach for Security and Privacy in Decision Support
**arXiv**: `2509.02413` | **年份**: 2025
**作者**: Edoardo Marangone, Eugenio Nerio Nemmi et al.

**摘要**：决策支持系统在医疗、金融等领域处理大量敏感数据，传统架构中数据处理逻辑在不可信环境中执行，存在数据泄露风险。本文提出一种基于 TEE 可信执行环境的决策支持安全架构，在 TEE 内完成敏感数据的处理和分析，确保决策过程中的数据机密性。作者设计了安全的决策协议，允许用户在保持数据控制权的同时获取个性化决策建议。系统通过远程证明机制向用户证明决策引擎的可信性，用户可以验证运行在 TEE 中的代码未被篡改。研究还分析了该方案在隐私保护方面的形式化安全属性，讨论了与现有医疗法规（如 GDPR）的合规性。实验表明，基于 TEE 的方案在保证安全性的同时，开销处于可接受范围内。

**主要贡献**：
- TEE 保护的决策支持架构
- 远程证明验证
- 隐私合规性分析
- 医疗/金融场景适用

**引用**: [DecisionSupport-2025]

---

### 5. TEEBFT: Pricing the Security of Proof of Cloud
**arXiv**: `2510.26091` | **年份**: 2025
**作者**: Alex Shamis, Matt Stephenson, Linfeng Zhou

**摘要**：本文探讨了在去中心化计算中如何量化可信执行环境所提供的安全价值，提出 TEEBFT 框架，对"云端证明"（Proof of Cloud）机制的安全性进行定价分析。在 PoS 区块链等去中心化系统中，验证者需要证明其在特定硬件上运行了正确代码，TEE 可以提供这种证明，但不同的 TEE 实现（Intel TDX、AMD SEV、ARM CCA）提供不同级别的安全保障。本文作者提出了一个量化模型，将 TEE 安全性映射到 BFT（拜占庭容错）共识中的信任参数，使得系统设计者可以据此选择合适的 TEE 方案并确定所需的验证者数量。TEEBFT 还分析了不同攻击场景（硬件攻击、侧信道攻击）对安全性的影响，为实际部署提供了量化依据。

**主要贡献**：
- TEE 安全性量化模型
- 安全性与 BFT 参数映射
- 多 TEE 平台比较
- 实际部署量化依据

**引用**: [TEEBFT-2025]

---

### 6. What You Trust Is Insecure: Demystifying How Developers (Mis)Use Trusted Execution Environments in Practice
**arXiv**: `2512.17363` | **年份**: 2025
**作者**: Cheng et al.

**摘要**：本文是一项关于开发者实际使用 TEE 的实证研究，通过对真实世界中 TEE 应用的代码分析和开发者访谈，揭示了普遍存在的 TEE 误用模式和安全隐患。作者收集了来自多个开源项目和商业应用中的 TEE 代码样本，发现开发者对 TEE 的使用存在大量问题，包括不正确的内存布局、过度的可信区域膨胀、缺失的输入验证以及不安全的密钥管理实践。研究识别出几类典型的反模式（anti-patterns），并分析了这些误用可能导致的安全后果。论文还提出了改进建议，包括更好的开发工具、文档和自动化检测方案。本文为 TEE 安全研究提供了真实世界的 threat model 参考，对 TEE 开发者社区具有重要的警示意义。

**主要贡献**：
- 大规模 TEE 代码实证分析
- 识别典型误用反模式
- 开发者行为研究
- 改进建议和工具

**引用**: [WhatYouTrust-2025]

---

### 7. Abstraction of Trusted Execution Environments as the Missing Layer for Broad Confidential Computing Adoption: A Systematization of Knowledge
**arXiv**: `2512.22090` | **年份**: 2025
**作者**: Quentin Michaud, Sara Ramezanian, Dhouha Ayed, Olivier Levillain, Joaquin Garcia-Alfaro

**摘要**：本文是一篇关于 TEE 抽象层的系统性综述论文（SoK），旨在填补机密计算生态中"抽象层"这一关键组件的研究空白。TEE 硬件实现多元化（Intel SGX、AMD SEV、ARM TrustZone/CCA、RISC-V Keystone 等），每种方案有各自 API、编程模型和安全属性，这种碎片化给应用开发者带来巨大障碍。本文梳理了现有主要的 TEE 抽象层方案，包括库操作系统（library OS）、容器化方案、WebAssembly 运行时等，分类分析了它们的设计选择、支持的特性集合和安全属性。研究发现 WebAssembly 是最具前景的抽象层方向，能够在保持安全性的同时提供最广泛的特性支持。论文最后讨论了未来抽象层的发展方向，以及如何与更广泛的机密计算生态融合，对理解 TEE 生态全貌有重要价值。

**主要贡献**：
- TEE 抽象层全面综述
- 分类对比分析
- WebAssembly 优势论证
- 未来研究方向

**引用**: [Abstraction-2025]

---

### 8. Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise
**arXiv**: `2602.11088` | **年份**: 2026
**作者**: Abhishek Saini

**摘要**：本文研究了部分 TEE 屏蔽的 LLM 推理中的安全漏洞，特别是在使用预计算噪声（precomputed noise）保护模型权重时的隐私泄露问题。随着在第三方设备上部署 LLM 的需求增长，TEE 被广泛用于保护专有模型权重，但完全在 TEE 内运行 LLM 成本高昂，因此出现了"部分屏蔽"方案，仅将敏感计算部分放入 TEE。本文作者发现，即使在 TEE 保护下，预计算噪声方案仍存在严重漏洞：攻击者可以通过侧信道分析恢复输入数据或模型权重信息。具体来说，他们展示了如何利用密文域中的噪声分布特征来推断原始数据。文章分析了漏洞的成因（噪声复用、时序侧信道等），并在多个主流 TEE 平台上验证了攻击的可行性，提出了针对预计算噪声方案的改进防护措施，对 LLM 隐私保护实践具有重要警示作用。

**主要贡献**：
- 发现 TEE-Shielded LLM 推理漏洞
- 预计算噪声侧信道攻击
- 多平台验证
- 防护改进措施

**引用**: [VulnerabilitiesLLM-2026]

---

### 9. Red-Teaming Claude Opus and ChatGPT-based Security Advisors for Trusted Execution Environments
**arXiv**: `2602.19450` | **年份**: 2026
**作者**: Kunal Mukherjee

**摘要**：本文通过红队测试方法对集成在 TEE 可信执行环境中的 Claude Opus 和 ChatGPT 安全顾问进行了系统性安全评估。随着 LLM 在安全关键系统中的应用增加，基于 TEE 的 LLM 部署成为一种保护模型和数据的方案，但这种"安全顾问"本身是否可信需要验证。本文作者从多个角度对部署在 TEE 内的 LLM 安全顾问进行了红队攻击测试，包括提示注入、角色混淆、指令规避、知识污染等攻击面。研究发现，即使有 TEE 硬件保护，LLM 本身的安全性问题仍然突出，特别是在多轮对话场景下攻击者可以通过精心构造的输入序列诱导模型产生不安全输出或泄露历史上下文信息。研究提出了针对 LLM 安全顾问的加固建议，对安全关键的 AI 部署具有参考价值。

**主要贡献**：
- 系统性 LLM 红队测试
- 多攻击面覆盖
- TEE 场景特殊风险分析
- 加固建议

**引用**: [RedTeaming-2026]

---

### 10. A TEE-Based Architecture for Confidential and Dependable Process Attestation in Authorship Verification
**arXiv**: `2603.00178` | **年份**: 2026
**作者**: Li et al.

**摘要**：本文针对数字创作领域的著作权验证问题，提出了一种基于 TEE 可信执行环境的保密且可靠的进程认证架构。随着 AI 生成内容的兴起，判断一段内容是否由特定人类作者创作变得越来越困难。本文提出在 TEE 内执行创作过程，当作者完成创作后，TEE 可以生成关于创作过程和结果的可验证证明，既保护了创作内容的机密性（未发布前内容不会泄露），又提供了可验证的创作证明。系统通过远程证明机制允许第三方验证创作证明的真实性，而无需暴露实际内容。这种"可信创作环境"的概念为数字著作权保护提供了新的技术思路，对于知识产权保护和内容真实性验证具有应用前景。

**主要贡献**：
- 可信创作认证架构
- TEE 保护创作过程
- 远程可验证证明
- 著作权保护新思路

**引用**: [ProcessAttestation-2026]

---

### 11. Sharing is Caring: Attestable and Trusted Workflows out of Distrustful Components
**arXiv**: `2603.03403` | **年份**: 2026
**作者**: Amir Al Sadi et al.

**摘要**：本文研究如何在由互不信任的组件组成的分布式系统中构建可认证的信任工作流。现代系统经常需要整合多个不可信或半可信的组件来完成任务，而每个组件都有各自的安全假设和信任边界。本文提出一种框架，利用 TEE 可信执行环境作为"信任锚点"，将不可信组件的工作流串联起来，同时在每个关键节点生成可验证的认证证明。文章解决了跨组织、跨平台工作流中的信任传递问题——即如何在一个不可信的执行环境中生成可在后续步骤中被验证的证明。框架支持条件隐私保护（组件可以选择性隐藏敏感输入），同时保证整体的执行完整性。研究展示了如何将这一框架应用于供应链溯源、数据湖隐私计算等实际场景。

**主要贡献**：
- 不可信组件信任工作流
- TEE 信任锚点设计
- 跨组织认证证明
- 供应链/数据湖应用

**引用**: [SharingIsCaring-2026]

---

### 12. External Entropy Supply for IoT Devices Employing a RISC-V Trusted Execution Environment
**arXiv**: `2603.09311` | **年份**: 2026
**作者**: Wilde et al.

**摘要**：本文针对资源受限的 RISC-V 物联网设备，提出了一种利用外部熵源为 TEE 提供高质量随机数的方案。物联网设备通常缺乏高质量的硬件随机数生成器，而安全的 TEE 操作（如密钥生成、远程证明）需要可靠的熵源。传统方案依赖本地伪随机数生成器，但这在资源受限的嵌入式设备上可能成为安全瓶颈。本文提出一种将外部高质量熵源安全注入到 RISC-V TEE 的架构，通过硬件信任根和 TEE 安全通道确保即使在设备本地 PRNG 受损的情况下，TEE 仍能获得密码学安全的随机数。研究分析了该方案在各种攻击场景下的安全性，并提供了在开源 RISC-V TEE 实现上的原型验证。

**主要贡献**：
- RISC-V TEE 熵源架构
- 外部熵源安全注入
- 硬件信任根集成
- 资源受限设备适配

**引用**: [ExternalEntropy-2026]

---

### 13. On Securing the Software Development Lifecycle in IoT RISC-V Trusted Execution Environments
**arXiv**: `2603.17757` | **年份**: 2026
**作者**: Annika Wilde et al.

**摘要**：本文探讨了如何保障物联网 RISC-V TEE 可信执行环境的软件开发生命周期（SDLC）安全。TEE 的安全性不仅取决于硬件，还取决于在 TEE 内运行的软件——如果软件构建过程被攻破，则 TEE 的信任链也会断裂。本文作者分析了 RISC-V TEE 生态系统中软件供应链的各个环节（编译工具链、构建环境、固件签名和分发），识别出多个潜在的攻击面，提出了对应的防护措施。特别关注了固件签名验证的盲点、构建 Reproducibility 问题的安全隐患，以及如何利用 TEE 本身来保护 SDLC 环节。研究还提出了一种基于 RISC-V TEE 的安全构建协议，确保软件从源码到二进制再到设备部署的全链路完整性，对提升 RISC-V 物联网生态安全性有重要参考价值。

**主要贡献**：
- RISC-V TEE SDLC 安全分析
- 软件供应链攻击面识别
- 安全构建协议
- 全链路完整性保护

**引用**: [IoTRISC-VSDLC-2026]

---

### 14. Space Fabric: A Satellite-Enhanced Trusted Execution Architecture
**arXiv**: `2603.23745` | **年份**: 2026
**作者**: Filip Rezabek et al.

**摘要**：本文提出 Space Fabric，一种利用卫星通信增强地面 TEE 可信执行环境安全性和可用性的架构设计。随着低轨卫星（LEO）通信的普及，利用卫星作为可信信息传输通道成为一个新的研究方向。Space Fabric 将卫星通信纳入 TEE 信任模型，利用卫星链路的物理特性（高空、无遮挡、难以地面窃听）增强远程证明的安全性——特别是可以抵抗地面中间人攻击和伪基站攻击。架构中还利用卫星作为 TEE 状态的备份和恢复节点，在地面基础设施受损时仍能保证关键 TEE 服务的可用性。作者分析了卫星通信延迟、带宽和可用性对整体架构的影响，探讨了在实际卫星星座上部署的可行性，为天地一体化机密计算提供了新的研究思路。

**主要贡献**：
- 天地一体化 TEE 架构
- 卫星增强远程证明
- TEE 备份与恢复
- 低轨卫星可行性分析

**引用**: [SpaceFabric-2026]

---

### 15. Trusted-Execution Environment for Solving the Replication Crisis in Academia
**arXiv**: `2603.24878` | **年份**: 2026
**作者**: Jiasun Li

**摘要**：本文创新性地将 TEE 可信执行环境应用于学术研究的"可复现性危机"问题。学术研究中许多关键实验难以独立复现，原因之一是研究者在数据处理和分析过程中存在大量手动操作，无法保证完全透明和可复现。本文提出在 TEE 内运行科研数据分析流程，通过远程证明让审稿人和读者能够验证研究者确实使用了声明的数据和方法，而无需访问原始数据的详细内容。这种方案在保护研究数据隐私的同时，提供了计算过程的可验证性，显著提升了科研结果的可信度。作者讨论了该方案在多个学科（医学、心理学、经济学）中的适用性，并探讨了与现有科研诚信验证机制的结合方式，是 TEE 在科学诚信领域的一个有创意的应用探索。

**主要贡献**：
- TEE 应用于科研可复现性
- 隐私保护下的过程可验证
- 多学科适用性分析
- 科研诚信新机制

**引用**: [ReplicationCrisis-2026]

---

### 16. Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy
**arXiv**: `2604.04082` | **年份**: 2026
**作者**: Shixuan Zhao et al.

**摘要**：本文提出 Styx 系统，在 TEE 可信执行环境中实现协作式私有数据处理，并首次引入"粘性策略"（sticky policy）概念。传统的隐私保护数据处理方案通常在数据处理开始前指定策略，之后难以更改。Styx 的"粘性策略"允许数据拥有者在数据中嵌入不可篡改的使用策略，这些策略会随数据一起在 TEE 中执行，任何违反策略的数据使用都会被 TEE 强制阻止。系统支持多方数据协作场景——各方的数据在各自 TEE 中处理，仅共享处理结果而不上报原始数据，通过 TEE 间的安全协议实现跨域数据关联分析。这种设计在保护数据所有权的同时实现了灵活的数据价值发掘，适用于医疗数据联盟、金融风控等强隐私监管场景，为数据要素流通提供了新的技术路径。

**主要贡献**：
- 粘性策略（sticky policy）概念
- TEE 强制策略执行
- 多方协作隐私计算
- 医疗/金融场景应用

**引用**: [Styx-2026]

---

## 参考文献

- [PMDedup-2025] PM-Dedup: Secure Deduplication with Partial Migration from Cloud to Edge Servers, arXiv:2501.02350, 2025
- [AutoTEE-2025] AutoTEE: Automated TEE Adaptation with LLMs, arXiv:2502.13379, 2025
- [Triad-2025] An Open-source Implementation and Security Analysis of Triad's TEE Trusted Time Protocol, arXiv:2507.20851, 2025
- [DecisionSupport-2025] A TEE-based Approach for Security and Privacy in Decision Support, arXiv:2509.02413, 2025
- [TEEBFT-2025] TEEBFT: Pricing the Security of Proof of Cloud, arXiv:2510.26091, 2025
- [WhatYouTrust-2025] What You Trust Is Insecure: Demystifying How Developers (Mis)Use TEEs in Practice, arXiv:2512.17363, 2025
- [Abstraction-2025] Abstraction of Trusted Execution Environments as the Missing Layer, arXiv:2512.22090, 2025
- [VulnerabilitiesLLM-2026] Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise, arXiv:2602.11088, 2026
- [RedTeaming-2026] Red-Teaming Claude Opus and ChatGPT-based Security Advisors for TEEs, arXiv:2602.19450, 2026
- [ProcessAttestation-2026] A TEE-Based Architecture for Process Attestation in Authorship Verification, arXiv:2603.00178, 2026
- [SharingIsCaring-2026] Sharing is Caring: Attestable and Trusted Workflows out of Distrustful Components, arXiv:2603.03403, 2026
- [ExternalEntropy-2026] External Entropy Supply for IoT Devices Employing a RISC-V TEE, arXiv:2603.09311, 2026
- [IoTRISC-VSDLC-2026] On Securing the Software Development Lifecycle in IoT RISC-V TEEs, arXiv:2603.17757, 2026
- [SpaceFabric-2026] Space Fabric: A Satellite-Enhanced Trusted Execution Architecture, arXiv:2603.23745, 2026
- [ReplicationCrisis-2026] Trusted-Execution Environment for Solving the Replication Crisis in Academia, arXiv:2603.24878, 2026
- [Styx-2026] Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy, arXiv:2604.04082, 2026
