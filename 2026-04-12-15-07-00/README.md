# TEE 论文综述

**时间戳**: 2026-04-12-15-07-00  
**收录范围**: 可信执行环境（Trusted Execution Environment, TEE）相关学术论文，聚焦 2026 年 arXiv 预印本与顶级学术会议（USENIX Security 2026 等）

---

## 目录

- [论文摘要](#论文摘要)
  - [1. Styx：基于 TEE 强制粘性策略的协作式私密数据处理](#1-styx基于tee强制粘性策略的协作式私密数据处理)
  - [2. Gyokuro：基于可信执行环境的源码辅助私密成员测试](#2-gyokuro基于可信执行环境的源码辅助私密成员测试)
  - [3. LiteAtt：基于 TinyML 自我证明原语的安全无缝物联网服务](#3-liteatt基于-tinyml-自我证明原语的安全无缝物联网服务)
  - [4. On Securing the SDLC in IoT RISC-V TEEs](#4-on-securing-the-sdlc-in-iot-risc-v-tees)
  - [5. Committee Configuration Optimization for Parallel Byzantine Consensus in a TEE](#5-committee-configuration-optimization-for-parallel-byzantine-consensus-in-a-tee)
  - [6. Proteus：面向（大多数）可信执行环境的只追加账本](#6-proteus面向大多数可信执行环境的只追加账本)
  - [7. Sharing is Caring：可信工作流](#7-sharing-is-caring-可信工作流)
  - [8. Designing Trustworthy Layered Attestations](#8-designing-trustworthy-layered-attestations)
  - [9. Trusting What You Cannot See：可审计微调与推理](#9-trusting-what-you-cannot-see-可审计微调与推理)
  - [10. AFTUNE：可审计的 TEE 支持 LLM 训练推理完整性框架](#10-aftune可审计的-tee-支持-llm-训练推理完整性框架)
  - [11. vCause：云端_endpoint 审计的因果分析](#11-vcause云端-endpoint-审计的因果分析)
  - [12. Proof-of-Guardrail in AI Agents](#12-proof-of-guardrail-in-ai-agents)
  - [13. Red-Teaming TEE-based Security Advisors](#13-red-teaming-tee-based-security-advisors)
  - [14. Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise](#14-vulnerabilities-in-partial-tee-shielded-llm-inference-with-precomputed-noise)
  - [15. Ringmaster：TrustZone TEE 高吞吐主机系统调用](#15-ringmastertrustzone-tee-高吞吐主机系统调用)
  - [16. A TEE-Based Architecture for Authorship Verification](#16-a-tee-based-architecture-for-authorship-verification)
  - [17. External Entropy Supply for IoT RISC-V TEEs](#17-external-entropy-supply-for-iot-risc-v-tees)
- [横向对比与综述](#横向对比与综述)
- [参考文献](#参考文献)

---

## 论文摘要

### 1. Styx：基于 TEE 强制粘性策略的协作式私密数据处理

**文件名**: `2026 - Styx - Collaborative and Private Data Processing With TEE-Enforced Sticky Policy.pdf`  
**arXiv ID**: 2604.04082  
**作者**: Shixuan Zhao (Ohio State), Weicheng Wang, Ninghui Li (Purdue), Zhiqiang Lin  
**核心贡献**: 本文提出 Styx 框架，解决多方互相不信任环境下的协作数据处理难题。传统隐私保护方案在数据跨组织流动时缺乏灵活、细粒度的策略执行机制。Styx 将粘性策略（sticky policy）与可信执行环境深度结合，在 TEE 内部强制绑定数据处理规则与数据本身，确保数据一旦被标记"仅限某用途"，无论流转至何处、经过多少方参与处理，该策略始终被硬件级强制执行，且任何违规操作均可被证明不可抵赖。Styx 的核心创新在于将策略实施从被动合规检查转变为积极执行的 TEE 原语，使隐私约束在分布式数据处理管道中随数据"粘附"流动。实验表明，Styx 在保证强安全性的同时，仅引入可忽略的性能开销。

---

### 2. Gyokuro：基于可信执行环境的源码辅助私密成员测试

**文件名**: `2026 - Gyokuro - Source-assisted Private Membership Testing using Trusted Execution Environments.pdf`  
**arXiv ID**: 2603.23226  
**作者**: Yoshimichi Nakatsuka, Nicolas Dutly, Kari Kostiainen, Srdjan Capkun (ETH Zurich)  
**核心贡献**: 私密成员测试（Private Membership Testing, PMT）是许多隐私计算应用的核心原语，允许用户在不泄露查询意图的前提下验证某数据项是否存在于服务器数据库中。Gyokuro 的核心洞察是：传统 PMT 方案依赖服务器向客户端返回证明，但服务器可能撒谎或提供不完整的响应。Gyokuro 利用 TEE 的可审计性，引入"源码辅助"机制——服务器在 TEE 内运行经过密码学设计的成员测试代码，并生成可验证的执行证明。与传统方案相比，Gyokuro 无需依赖服务器的可信性假设（仅需依赖 TEE 硬件安全假设），且能证明服务器"已进行足够多次的正确计算"，防止服务器的作弊行为。该方案在实用性与安全性之间取得了良好平衡，适用于医疗记录查询、金融合规等高敏感场景。

---

### 3. LiteAtt：基于 TinyML 自我证明原语的安全无缝物联网服务

**文件名**: `2026 - LiteAtt - Secure and Seamless IoT Services Using TinyML-based Self-Attestation as a Primitive.pdf`  
**arXiv ID**: 2603.19727  
**作者**: Varun Kohli, Biplab Sikdar  
**核心贡献**: 物联网设备资源受限，传统的远程证明（remote attestation）方案需要强大的运算能力支持，或依赖外部验证者。LiteAtt 提出一种轻量级自我证明方案，以 TinyML 作为证明原语：物联网 MCU 设备在本地运行 TinyML 推理模型，该模型同时充当"测量探针"感知设备运行时状态，并在 TEE 保护下生成包含设备完整性信息的证明。远程验证方可在不解密证明的情况下验证设备状态，无需强大的云端算力。LiteAtt 解决了资源受限 IoT 设备难以参与现代零信任架构的困境，将证明义务从设备端转移至云端验证者，同时通过 TEE 保证证明生成过程本身的可信性。实验证明，该方案在 ARM Cortex-M 系列微控制器上可正常运行，证明生成时间控制在毫秒级。

---

### 4. On Securing the SDLC in IoT RISC-V TEEs

**文件名**: `2026 - On Securing the Software Development Lifecycle in IoT RISC-V Trusted Execution Environments.pdf`  
**arXiv ID**: 2603.17757  
**作者**: Annika Wilde (Ruhr Univ. Bochum), Samira Briongos (NEC Labs Europe), Claudio Soriente, Ghassan Karame  
**核心贡献**: RISC-V 架构的 TEE（如 Keystone、RISC-V Trusted Software Stack）为物联网提供了开放、可定制的安全隔离方案，但软件开发生命周期（SDLC）本身的安全性往往被忽视。攻击者可利用构建系统的漏洞，在软件编译环节注入恶意代码，使最终交付给用户的"可信应用"实际包含后门。本文系统分析了 RISC-V TEE 环境下 SDLC 的攻击面，提出针对编译工具链、构建服务器和代码签名的多层加固方案，并给出了形式化安全证明。该工作为 RISC-V TEE 从"硬件安全"向"端到端安全"的演进提供了重要的实践指导。论文已被 SenSys 2026 录用。

---

### 5. Committee Configuration Optimization for Parallel Byzantine Consensus in a TEE

**文件名**: `2026 - Committee Configuration Optimization for Parallel Byzantine Consensus in a Trusted Execution Environment.pdf`  
**arXiv ID**: 2603.14445  
**作者**: Yifei Xie, Btissam Er-Rahmadi, Xiao Chen, Tiejun Ma, Jane Hillston  
**核心贡献**: 基于委员会的分片式 BFT 协议虽提升了可扩展性，却因委员会规模较小而削弱了安全性。本文将 TEE 引入拜占庭共识的委员会配置优化：在 TEE 硬件保护下运行共识协议，即使在部分节点被妥协的敌手模型下也能维持安全性。论文提出了委员会规模的最优配置算法，通过 TEE 的远程证明确保各节点运行的是经过认证的共识代码，并在诚实多数假设下证明安全性。相较于纯软件方案，TEE 加持的共识协议在故障容错能力不降低的前提下，显著降低了通信复杂度，适用于区块链 Layer2 扩容和分布式AI训练协调等场景。

---

### 6. Proteus：面向（大多数）可信执行环境的只追加账本

**文件名**: `2026 - Proteus - Append-Only Ledgers for (Mostly) Trusted Execution Environments.pdf`  
**arXiv ID**: 2602.05346  
**作者**: Shubham Mishra (UC Berkeley), João Gonçalves, Natacha Crooks, et al.  
**核心贡献**: 分布式只追加账本是提供可信赖问责制、强完整性保护和关键数据高可用性的核心基础设施。Proteus 针对主流 TEE 平台（Intel SGX、Arm TrustZone）的特性，设计了一种结合崩溃容错（CFT）共识与硬件可信执行的分层账本架构。Proteus 的核心创新在于利用 TEE 保护共识协议的关键状态转换逻辑，即使底层操作系统被攻破，账本历史记录仍无法被篡改。论文提供了完整的安全性分析，形式化证明 Proteus 在 TEE 硬件安全假设下可达成分布式只追加语义，并开源了参考实现。Proteus 对工业界现有的高完整性日志系统和区块链轻节点设计有直接参考价值。

---

### 7. Sharing is Caring：可信工作流

**文件名**: `2026 - Sharing is Caring - Attestable and Trusted Workflows out of Distrustful Components.pdf`  
**arXiv ID**: 2603.03403  
**作者**: Amir Al Sadi, Sina Abdollahi (Imperial College), Adrien Ghosn (Microsoft Research), Hamed Haddadi, Marios Kogias  
**核心贡献**: 现代分布式系统由大量独立开发的组件协作完成复杂任务，但组件间缺乏互信基础，使得工作流的执行结果难以被所有参与方信任。本文提出一种基于 TEE 和可证明工作流（attestable workflow）的跨组件协作框架。关键思路是：将工作流的每一步执行及其输入输出打包为可在 TEE 内验证的证明片段，各参与方可独立验证工作流的正确性而无需信任其他组件或中心化协调者。论文形式化定义了"可信工作流"的安全模型，并设计了高效的证明聚合协议，将大量细粒度证明压缩为可快速验证的单一承诺。该工作为去中心化 AI 训练和联邦学习等场景提供了组件间互信的技术基础。

---

### 8. Designing Trustworthy Layered Attestations

**文件名**: `2026 - Designing Trustworthy Layered Attestations.pdf`  
**arXiv ID**: 2603.06326  
**作者**: Will Thomas, Logan Schmalz, Adam Petz, Perry Alexander, Joshua D. Guttman, Paul D. Rowe, James Carter  
**核心贡献**: 远程证明是建立网络访问控制、安全管理和软件供应链安全的基础机制，但现有方案多为单层、点对点式的，缺乏系统性设计原则。本文提出分层可信证明（Layered Attestations）框架，将证明分为**平台层**（硬件与固件完整性）、**系统层**（操作系统配置与软件栈）和**应用层**（特定业务逻辑），并为各层之间建立严格的依赖链。论文的关键贡献在于：证明了各层证明必须保持独立性，某一层的妥协不能级联破坏其他层的安全性；并给出了实用的跨层证明验证协议。该工作对 IEEE 和 NIST 正在制定的远程证明标准具有直接影响。

---

### 9. Trusting What You Cannot See：可审计微调与推理

**文件名**: `2026 - Trusting What You Cannot See - Auditable Fine-Tuning and Inference for Proprietary AI.pdf`  
**arXiv ID**: 2603.07466  
**作者**: Heng Jin, Chaoyu Zhang, Hexuan Yu, Shanghao Shi, Ning Zhang, Y. Thomas Hou, Wenjing Lou (Virginia Tech, Washington Univ. St. Louis)  
**核心贡献**: 云端部署的大语言模型（LLM）日益普遍，但将模型微调和推理委托给云服务商形成了根本性的信任鸿沟：密码学和 TEE 验证理论上存在，但面对现代 LLMs 的规模变得不切实际，导致客户无法有效审计这些过程。本文提出 AFTUNE（Auditable Fine-TUNing and Evaluation）框架，通过轻量级执行记录和随机抽检机制，确保云端 LLM 微调和推理的计算完整性。AFTUNE 利用 TEE 在受保护环境中记录每次前向传播的关键中间值，客户可随时发起挑战验证，无需每次都对完整计算进行重放。实验表明，AFTUNE 在保持可验证安全性的同时，仅增加约 5-12% 的计算开销，为专有 AI 模型的可审计性提供了实用方案。

---

### 10. AFTUNE：可审计的 TEE 支持 LLM 训练推理完整性框架

**文件名**: `2026 - Trusting What You Cannot See - Auditable Fine-Tuning and Inference for Proprietary AI.pdf`  
**arXiv ID**: 2603.07466（与上述同一论文，此处补充细节）  
**核心贡献（补充）**: AFTUNE 的核心设计基于 TEE 的可录制性：模型每次前向传播的隐层激活向量在 TEE 内被记录并生成哈希承诺；客户端可通过随机采样中间层激活值进行等式验证，证明模型确实在给定输入上进行了正确的前向/反向计算。该方案巧妙利用了 LLM 的数值稳定性特征，在浮点精度和证明大小之间取得了平衡，适用于 Transformer 架构的大多数变体。

---

### 11. vCause：云端_endpoint 审计的因果分析

**文件名**: `2026 - vCause - Efficient and Verifiable Causality Analysis for Cloud-based Endpoint Auditing.pdf`  
**arXiv ID**: 2603.15216  
**作者**: Qiyang Song, Qihang Zhou, Xiaoqi Jia, Zhenyu Song, Wenbo Jiang, Heqing Huang, Yong Liu, Dan Meng  
**核心贡献**: 云端_endpoint 审计是检测入侵和数据泄露的核心手段，但缺乏防篡改的因果分析机制导致攻击者可清除痕迹。现有的防篡改日志方案和 TEE 方案均非专门为因果分析设计。vCause 提出基于 TEE 的高效可验证因果分析框架，核心创新在于将数据溯源（data provenance）与 TEE 远程证明结合，使因果分析结果本身是可验证的——任何试图篡改分析链条的行为均会被发现。论文已被 USENIX Security 2026 录用。

---

### 12. Proof-of-Guardrail in AI Agents

**文件名**: `2026 - Proof-of-Guardrail in AI Agents and What (Not) to Trust from It.pdf`  
**arXiv ID**: 2603.05786  
**作者**: Xisen Jin, Michael Duan, Qin Lin, Aaron Chan, Zhenglun Chen, Junyi Du, Xiang Ren  
**核心贡献**: AI Agent 的防护栏（guardrail）是防止模型生成有害内容的关键机制，但用户无法验证 Agent 响应是否真的经过了指定的防护栏检验。Proof-of-Guardrail 利用 TEE 提供密码学证明：开发者将 Agent 和防护栏代码共同运行在 TEE 中，防护栏对每次模型输出的检查结果被打包进可验证的证明中，外部验证方可在不信任 Agent 运行平台的前提下验证"该响应确实通过了某版本的防护栏检验"。论文还深入分析了当前 Proof-of-Guardrail 的局限性，指出其仅能证明"防护栏已运行"，不能证明"防护栏正确配置"，并给出了改进方向。对安全关键的 AI 应用（如医疗、法律咨询）的合规性验证具有重要意义。

---

### 13. Red-Teaming TEE-based Security Advisors

**文件名**: `2026 - Red-Teaming Claude Opus and ChatGPT-based Security Advisors for Trusted Execution Environments.pdf`  
**arXiv ID**: 2602.19450  
**作者**: Kunal Mukherjee (Virginia Tech)  
**核心贡献**: TEE（如 Intel SGX 和 Arm TrustZone）旨在保护敏感计算免受被入侵操作系统的攻击，但实际部署仍面临微架构侧信道攻击、侧信道故障注入等威胁。本文对部署在 TEE 内的 Claude Opus 和 ChatGPT 安全顾问进行了系统性红队测试，发现了多个可致敏感数据泄露的攻击路径，包括：基于分支预测器的侧信道攻击可提取 TEE 内的对话历史；基于页表的攻击可恢复模型权重；以及利用 TEE 与非安全世界共享微架构资源的微架构侧信道攻击。论文系统梳理了 TEE 内运行 LLM 的安全威胁面，对未来 TEE + AI 系统的安全设计有重要警示作用。

---

### 14. Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise

**文件名**: `2026 - Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise.pdf`  
**arXiv ID**: 2602.11088  
**作者**: Abhishek Saini, Haolin Jiang, Hang Liu (Rutgers)  
**核心贡献**: 在第三方设备上部署 LLM 需要保护模型知识产权。TEE 提供了有前景的解决方案，但由于性能限制，业界广泛采用"预计算噪声"模式来加速加密操作——即预先计算并存储随机数用于掩码（masking）操作。本文揭示了这一主流设计模式存在经典的密码学缺陷：**密钥材料的重用**。作者设计了两种攻击：(1) 机密性攻击：完整恢复模型的秘密排列和权重，实现模型窃取；(2) 完整性攻击：绕过 Soter 等系统的完整性检查，注入任意模型输出。攻击适用于任何使用预计算随机数的部分 TEE 保护 LLM 推理系统。该工作深刻揭示了性能优化与安全设计之间的张力，对 TEE 内 LLM 推理系统的安全架构有重要警示意义。

---

### 15. Ringmaster：TrustZone TEE 高吞吐主机系统调用

**文件名**: `2026 - Ringmaster - How to Juggle High-Throughput Host OS System Calls from TrustZone TEEs.pdf`  
**arXiv ID**: 2601.16448  
**作者**: Richard Habeeb, Man-Ki Yoon, Hao Chen, Zhong Shao (Yale, NC State)  
**核心贡献**: TrustZone TEE 的隔离区（trusted execution environment）与富操作系统之间存在根本性的互操作难题：TEE 侧程序若借助 hypervisor 实现与主机隔离，则无法访问丰富的 OS 服务；若需要访问 OS 服务，则必须放弃 TEE 保护。Ringmaster 提出一种新颖的异步框架，允许 TEE 程序在不需要 hypervisor 的前提下，以高吞吐、异步方式访问富操作系统的丰富服务。具体机制为：TEE 端发起系统调用请求，该请求通过共享内存队列传递给主机 OS 的非安全世界处理，结果以事件驱动方式异步返回至 TEE。Ringmaster 对比了同步调用方案，将吞吐量提升 2-3 个数量级，同时保持 TEE 侧代码的可信性不变。该工作对移动支付、车载安全系统等同时需要 TEE 保护和丰富 OS 服务的场景有直接价值。

---

### 16. A TEE-Based Architecture for Authorship Verification

**文件名**: `2026 - A TEE-Based Architecture for Confidential and Dependable Process Attestation in Authorship Verification.pdf`  
**arXiv ID**: 2603.00178  
**作者**: David Condrey  
**核心贡献**: 著作权验证依赖于证据收集基础设施——但当被审查方控制平台时，该基础设施的可用性和防篡改性无法得到保障。本文设计了一种基于 TEE 的保密可靠著作权验证架构，利用 TEE 的硬件隔离特性确保证据收集过程本身不受运行平台被控的影响。核心思路是将证据收集逻辑封装在 TEE 中，即使攻击者完全控制了主机操作系统，也无法干预或篡改证据生成过程。论文提供了形式化安全证明，表明该架构在 TEE 硬件安全假设下可达成证据的保密性、防篡改性和可用性。该工作为文档审计、软件供应链 provenance 等需要可信证据收集的场景提供了新的解决思路。

---

### 17. External Entropy Supply for IoT RISC-V TEEs

**文件名**: `2026 - External Entropy Supply for IoT Devices Employing a RISC-V Trusted Execution Environment.pdf`  
**arXiv ID**: 2603.09311  
**作者**: Arttu Paju, Juha Nurmi, Alejandro Cabrera Aldaya, Nicola Tuveri, Juha Savimäki, Marko Kivikangas, Brian McGillion  
**核心贡献**: 安全随机数生成是密码学系统的命脉，但资源受限的物联网设备往往无法生成足够的熵。缺乏可靠的随机源会导致 TEE 的密钥生成和签名操作使用可预测的随机数，直接破坏整个安全体系的根基。本文解决物联网设备集群的熵源供给问题——设备可生成的熵有限，设计了一种外部熵供给协议，允许受信任的边缘节点或云服务端向 IoT 设备安全地传输额外熵。所有熵传输在 TEE 内完成，且经过密码学验证确保传输的熵的随机性，防止恶意中间人注入已知熵。论文已在 CRiSIS 2025 会议发表。

---

## 横向对比与综述

### 领域总览

本次收录的 17 篇论文覆盖了 TEE 领域的多个前沿方向，可归纳为以下几大类：

| 方向 | 代表论文 |
|------|---------|
| **TEE + AI/LLM** | [§9 AFTUNE](#9-trusting-what-you-cannot-see), [§13 Red-Teaming](#13-red-teaming-tee-based-security-advisors), [§14 Precomputed Noise](#14-vulnerabilities-in-partial-tee-shielded-llm-inference), [§12 Proof-of-Guardrail](#12-proof-of-guardrail-in-ai-agents) |
| **隐私计算** | [§1 Styx](#1-styx基于tee强制粘性策略的协作式私密数据处理), [§2 Gyokuro](#2-gyokuro基于可信执行环境的源码辅助私密成员测试) |
| **IoT / 嵌入式 TEE** | [§3 LiteAtt](#3-liteatt基于-tinyml-自我证明原语的安全无缝物联网服务), [§4 SDLC RISC-V](#4-on-securing-the-sdlc-in-iot-risc-v-tees), [§17 RISC-V Entropy](#17-external-entropy-supply-for-iot-risc-v-tees) |
| **共识与区块链** | [§5 Committee BFT](#5-committee-configuration-optimization-for-parallel-byzantine-consensus-in-a-tee), [§6 Proteus](#6-proteus面向大多数可信执行环境的只追加账本) |
| **证明与审计** | [§8 Layered Attestations](#8-designing-trustworthy-layered-attestations), [§16 Authorship Verification](#16-a-tee-based-architecture-for-authorship-verification) |
| **系统基础设施** | [§11 vCause](#11-vcause云端-endpoint-审计的因果分析), [§7 Trusted Workflows](#7-sharing-is-caring-可信工作流), [§15 Ringmaster](#15-ringmastertrustzone-tee-高吞吐主机系统调用) |

---

### 核心趋势一：TEE 从"隔离盒"向"可信基础设施"演进

过去 TEE 的定位是"让代码在一个隔离世界中运行"，但这批论文揭示了更宏大的愿景：

- **跨组件信任传递**：Ringmaster（[§15](#15-ringmastertrustzone-tee-高吞吐主机系统调用)）和 Proteus（[§6](#6-proteus面向大多数可信执行环境的只追加账本）均在探索 TEE 与非安全世界之间的深度互操作——前者解决了 TEE 无法使用丰富 OS 服务的老大难问题，后者将 TEE 融入分布式系统的核心数据路径。
- **工作流级信任**：Sharing is Caring（[§7](#7-sharing-is-caring-可信工作流)）和 Styx（[§1](#1-styx基于tee强制粘性策略的协作式私密数据处理)）将信任从单点扩展到跨组织工作流，解决了"即使每一方都可信、多方协作结果也不可信"的分布式系统根本难题。

**这一趋势的技术基础**：TEE 不再仅用于"保护某个密钥"，而是成为构建整个系统信任根的组件。

---

### 核心趋势二：TEE + LLM 的深度融合与安全攻防

本批次中，涉及 LLM 与 TEE 结合的论文占比最高（4/17），且均发表于 2026 年，说明这一方向正处于快速突破期：

- **攻击面研究先行**：Red-Teaming（[§13](#13-red-teaming-tee-based-security-advisors)）和 Vulnerabilities in Precomputed Noise（[§14](#14-vulnerabilities-in-partial-tee-shielded-llm-inference-with-precomputed-noise)）从攻击者视角揭示了 TEE 内运行 LLM 的微架构侧信道、预计算随机数重用等新型攻击面。尤其是 [§14](#14-vulnerabilities-in-partial-tee-shielded-llm-inference-with-precomputed-noise)，该攻击利用"性能优化习惯"——预计算随机数进行掩码——这一广泛存在的工程实践，直接破解了多个 TEE+LLM 系统，证明安全与性能的平衡需要更审慎的设计。
- **防御与可验证性**：Proof-of-Guardrail（[§12](#12-proof-of-guardrail-in-ai-agents)）和 AFTUNE（[§9](#9-trusting-what-you-cannot-see)）从防御角度给出了实用方案——前者确保 AI 防护栏的执行可被证明，后者使客户无需重放完整计算即可验证云端 LLM 执行的正确性。

**对比总结**：[§14](#14-vulnerabilities-in-partial-tee-shielded-llm-inference-with-precomputed-noise) 揭示的问题本质是"TEE 提供了隔离，但性能要求导致信息泄漏"——这与经典的外侧信道攻击思路一脉相承，却因为 LLM 的大状态空间而变得更难防御。未来的 TEE+LLM 系统需要共同设计（co-design）安全机制与性能优化，简单的"TEE 包裹 LLM"方案已被证明不安全。

---

### 核心趋势三：私密成员测试与零知识证明的能力边界探索

Gyokuro（[§2](#2-gyokuro基于可信执行环境的源码辅助私密成员测试)）代表了 TEE 与传统密码学协议结合的新方向：不是用 TEE 替代密码学，而是用 TEE 弥补密码学协议的弱点。私密成员测试（PMT）是 PIR（Private Information Retrieval）等隐私查询协议的核心，高效的密码学 PMT 方案（如 Paillier 加密基础）通常需要服务器返回大量密文，而 Gyokuro 通过引入 TEE 可审计性，使服务器必须提供"已执行正确计算"的证明而非仅返回结果，将验证成本从客户端转移至服务器端，同时保留了隐私保护。

这一思路与 Styx（[§1](#1-styx基于tee强制粘性策略的协作式私密数据处理)）的粘性策略形成互补：Styx 确保策略随数据流动，Gyokuro 确保查询过程不泄露意图，两者共同构成更完整的隐私计算基础设施。

---

### 核心趋势四：IoT TEE 从"芯片级安全"向"系统级安全"延伸

LiteAtt（[§3](#3-liteatt基于-tinyml-自我证明原语的安全无缝物联网服务)）、SDLC RISC-V（[§4](#4-on-securing-the-sdlc-in-iot-risc-v-tees)）和 RISC-V Entropy（[§17](#17-external-entropy-supply-for-iot-risc-v-tees)）三篇论文共同指向一个核心洞察：TEE 芯片安全不等于系统安全。

| 维度 | 威胁 | 论文对应 |
|------|------|---------|
| **软件供应链** | 构建系统被攻破导致交付给用户的 TEE App 包含后门 | [§4](#4-on-securing-the-sdlc-in-iot-risc-v-tees) |
| **随机数安全** | 熵不足导致 TEE 内密钥可预测 | [§17](#17-external-entropy-supply-for-iot-risc-v-tees) |
| **轻量级远程证明** | 资源受限 MCU 无法运行重型证明协议 | [§3](#3-liteatt基于-tinyml-自我证明原语的安全无缝物联网服务) |

三篇论文共同构建了 IoT TEE 的完整安全链条，从供应链（[§4](#4-on-securing-the-sdlc-in-iot-risc-v-tees)）到运行时（[§3](#3-liteatt基于-tinyml-自我证明原语的安全无缝物联网服务)）再到密钥生成（[§17](#17-external-entropy-supply-for-iot-risc-v-tees)），为 RISC-V TEE 的实用化部署提供了系统性的安全工程参考。

---

### 核心趋势五：TEE 用于区块链与分布式系统基础设施

Committee BFT（[§5](#5-committee-configuration-optimization-for-parallel-byzantine-consensus-in-a-tee)）和 Proteus（[§6](#6-proteus面向大多数可信执行环境的只追加账本)）将 TEE 从"单机安全"推向"分布式系统安全"：

- [§5](#5-committee-configuration-optimization-for-parallel-byzantine-consensus-in-a-tee) 证明 TEE 可以在不降低拜占庭容错能力的前提下简化共识协议的通信复杂度
- [§6](#6-proteus面向大多数可信执行环境的只追加账本) 将 TEE 用于构建不可篡改的账本基础设施，解决了"分布式系统缺乏可信参照物"的根本难题——即 Proteus 自身作为可信基础设施来证明其他组件的行为

两者共同代表了一个新兴方向：**TEE as Infrastructure**（TEE 即基础设施），即 TEE 不再是保护单个应用的工具，而是成为整个分布式系统的信任锚点。

---

### 跨论文方法论对比

| 论文 | TEE 利用模式 | 信任假设 | 核心创新 |
|------|------------|---------|---------|
| Styx | TEE 强制执行粘性策略 | TEE 硬件 | 策略随数据流动，内嵌于数据本身 |
| Gyokuro | TEE 可审计执行 | TEE 硬件 + 源码完整 | "足够次正确计算"的证明，防止服务器作弊 |
| LiteAtt | TEE 保护 TinyML 推理 | TEE 硬件 | 将证明义务转移至云端验证者 |
| Ringmaster | TEE 异步系统调用 | TEE 硬件 | 打破 TEE 与非安全世界的隔阂，无需 hypervisor |
| Proteus | TEE 保护共识状态转换 | TEE 硬件 | 分层架构结合 CFT + TEE |
| AFTUNE | TEE 录制 + 随机抽检 | TEE 硬件 | 轻量级可验证计算，5-12% 开销 |

---

### 未来研究方向

1. **TEE+LLM 的共同设计安全**：侧信道攻击与防侧信道设计的共同优化（[§13](#13-red-teaming-tee-based-security-advisors)、[§14](#14-vulnerabilities-in-partial-tee-shielded-llm-inference-with-precomputed-noise) 已揭示单点方案的不足）
2. **TEE 的形式化验证规模化**：Layered Attestations（[§8](#8-designing-trustworthy-layered-attestations)）指出了跨层证明的必要性，形式化验证将成为 TEE 安全设计的必备工具
3. **多方 TEE 协作**：Styx 和 Gyokuro 均为多方场景设计，但目前方案在参与方动态加入/退出时的可扩展性仍是开放问题
4. **RISC-V TEE 标准化**：SDLC 论文表明 RISC-V TEE 生态亟需从芯片到工具链到运行时的完整安全标准

---

## 参考文献

- [1] Zhao et al. *Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy*. arXiv:2604.04082, 2026.
- [2] Nakatsuka et al. *Gyokuro: Source-assisted Private Membership Testing using Trusted Execution Environments*. arXiv:2603.23226, 2026.
- [3] Kohli & Sikdar. *LiteAtt: Secure and Seamless IoT Services Using TinyML-based Self-Attestation as a Primitive*. arXiv:2603.19727, 2026.
- [4] Wilde et al. *On Securing the Software Development Lifecycle in IoT RISC-V Trusted Execution Environments*. arXiv:2603.17757, 2026. (SenSys 2026)
- [5] Xie et al. *Committee Configuration Optimization for Parallel Byzantine Consensus in a Trusted Execution Environment*. arXiv:2603.14445, 2026.
- [6] Mishra et al. *Proteus: Append-Only Ledgers for (Mostly) Trusted Execution Environments*. arXiv:2602.05346, 2026.
- [7] Al Sadi et al. *Sharing is Caring: Attestable and Trusted Workflows out of Distrustful Components*. arXiv:2603.03403, 2026.
- [8] Thomas et al. *Designing Trustworthy Layered Attestations*. arXiv:2603.06326, 2026.
- [9] Jin et al. *Trusting What You Cannot See: Auditable Fine-Tuning and Inference for Proprietary AI*. arXiv:2603.07466, 2026.
- [10] 同 [9]，AFTUNE 框架详细设计。
- [11] Song et al. *vCause: Efficient and Verifiable Causality Analysis for Cloud-based Endpoint Auditing*. arXiv:2603.15216, 2026. (USENIX Security 2026)
- [12] Jin et al. *Proof-of-Guardrail in AI Agents and What (Not) to Trust from It*. arXiv:2603.05786, 2026.
- [13] Mukherjee. *Red-Teaming Claude Opus and ChatGPT-based Security Advisors for Trusted Execution Environments*. arXiv:2602.19450, 2026.
- [14] Saini, Jiang & Liu. *Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise*. arXiv:2602.11088, 2026.
- [15] Habeeb et al. *Ringmaster: How to Juggle High-Throughput Host OS System Calls from TrustZone TEEs*. arXiv:2601.16448, 2026.
- [16] Condrey. *A TEE-Based Architecture for Confidential and Dependable Process Attestation in Authorship Verification*. arXiv:2603.00178, 2026.
- [17] Paju et al. *External Entropy Supply for IoT Devices Employing a RISC-V Trusted Execution Environment*. arXiv:2603.09311, 2026. (CRiSIS 2025)
