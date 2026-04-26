# TEE 论文综述 — 2026-04-26 批次

## 本批次收录论文

本批次共收录 10 篇与可信执行环境（TEE）相关的学术论文，涵盖区块链共识、机器学习安全推理、联邦学习隐私保护、数据库系统、分布式存储可靠性等多个方向。

---

## 1. TEE-based Key-Value Stores: a Survey (2025)

**作者：** Aghiles Ait Messaoud, Sonia Ben Mokhtar, Anthony Simonet-Boulogne

**来源：** arXiv:2501.03118, 2025年1月

### 概述

本文是一篇关于基于 TEE（特别是 Intel SGX）的键值存储系统（Key-Value Stores, KVS）的全面综述。键值存储作为 NoSQL 数据库的重要类型，因其简洁性、可扩展性和快速检索能力而在云计算中广受欢迎。然而，存储敏感数据需要强安全属性来防止数据泄露和未授权篡改。

论文系统梳理了 TEE-based KVS 的通用架构，将其划分为五个核心模块：(1) **数据结构模块**，涵盖哈希表、跳表和日志结构合并树（LSMT）三种主要结构及其在 SGX 有限安全内存下的适配策略；(2) **磁盘访问优化模块**，包括异步系统调用和 SPDK 用户态驱动，通过绕过内核存储栈减少上下文切换开销；(3) **网络优化模块**，采用 DPDK 和 RDMA 技术实现高性能网络通信；(4) **同步模块**，分析 Raft、ABD 和两阶段提交三种共识协议在 TEE 环境下的应用；(5) **安全模块**，涵盖远程证明、安全通道建立、数据机密性/完整性/新鲜性保护以及可用性保障机制。

论文对 10 个代表性系统（ShieldStore、Speicher、Avocado、Treaty 等）进行了多维度分类比较，并深入讨论了侧信道攻击（SCA）对 SGX 系统的持续威胁及现有缓解方案。核心发现包括：所有被调研系统均选择 Client SGX 而非 Scalable SGX，因其提供物理完整性保护；SGX 安全内存限制（128MB）是主要性能瓶颈；侧信道攻击缓解方案虽有效但代价高昂，导致实际系统中均未部署。论文最后指出 Client SGX 的持续支持不确定性和侧信道攻击防御的实际挑战是未来关键研究方向。

---

## 2. Jodes: Efficient Oblivious Join in the Distributed Setting (2025)

**作者：** Yilei Wang, Xiangdong Zeng, Sheng Wang, Feifei Li (Alibaba Cloud)

**来源：** arXiv:2501.09334, 2025年1月

### 概述

本文针对基于 TEE 的加密数据分析系统中的等值连接（equi-join）操作，提出了高效的分布式遗忘连接算法 Jodes。在 TEE enclave 内执行计算虽然提供了隔离的安全环境，但仍面临侧信道攻击导致的访问模式泄露问题。遗忘计算（oblivious computation）要求内存访问模式独立于输入，但引入显著开销。

Jodes 的核心创新在于同时在网络层面和 enclave 层面实现遗忘性。在网络侧，通信模式（各服务器间传输的数据量）独立于输入数据分布，防御网络窃听者；在 enclave 侧，内存访问模式独立于输入，防御内存观察者。算法仅公开输入大小和输出大小这一最弱信息泄露。在分布式 16 服务器环境中的实验表明，Jodes 相比最先进的连接算法实现了最高 6 倍的性能提升，同时在通信开销和计算开销上均实现了渐近意义上的优势。

论文详细分析了先前工作（Opaque 和 SODA）在连接操作支持上的不足——要么效率低下，要么功能受限，要么安全假设较弱。Jodes 通过精心设计的分布式 oblivious sort 和 oblivious shuffle 原语，结合高效的 join 实现，填补了这一空白。这项工作为构建实用的分布式加密数据分析系统提供了关键基础组件。

---

## 3. Characterization of GPU TEE Overheads in Distributed Data Parallel ML Training (2025)

**作者：** Jonghyun Lee, Yongqin Wang, Rachit Rajat, Mengyuan Li, Murali Annavaram (USC)

**来源：** arXiv:2501.11771, 2025年1月（v3: 2025年8月）

### 概述

本文是对 GPU TEE 在分布式数据并行（DDP）机器学习训练中性能开销的深入实证研究。随着 NVIDIA H100、B200 等服务器级 GPU 原生支持 TEE（NVIDIA Confidential Computing），在云端安全训练 ML 模型成为可能。然而，GPU TEE 对分布式训练的具体影响此前未被充分探索。

研究揭示了 GPU TEE 在 DDP 训练中的核心瓶颈：在反向传播阶段，DDP 执行环形全归约（ring all-reduce），由于只有 CPU 和 GPU 封装受信，跨越封装边界的每条消息都需要加密和认证。随着 GPU 数量增加，子步骤数及其 TEE 开销线性增长。实验测得在 4 块 GPU 上，各基准测试平均每次迭代时间增加 8.68 倍，GPT-2-XL 模型的减速高达 41.6 倍。异步梯度交换（本应将通信与计算重叠）在 GPU TEE 中收益甚微，因为保护多次小传输的安全开销占主导地位。

论文提出的缓解方案是增大 DDP 的 bucket_cap_mb 参数以批量传输更多梯度，减少往返次数。这一调优将差距缩小，但 GPT-2-XL 在 4-GPU TEE 环境下仍比非 TEE 基线慢 3.03 倍。研究结论强调需要超越参数调优的 TEE 感知通信设计，为未来 GPU TEE 在大规模 ML 训练中的应用提供了重要的基准数据。

---

## 4. LATTEO: A Framework to Support Learning Asynchronously Tempered with Trusted Execution and Obfuscation (2025)

**作者：** Abhinav Kumar 等 (Saint Louis University, New Mexico State University, Intel Labs)

**来源：** arXiv:2502.04601, 2025年2月

### 概述

LATTEO 是一个面向异步联邦学习（FL）的隐私保护框架，结合了梯度混淆机制和 TEE 实现网络边缘的安全聚合。论文首先揭示了一个此前被忽视的问题：异步联邦学习存在严重的隐私漏洞。作者提出了一种新颖的数据重构攻击，利用梯度更新恢复敏感客户端数据。

为解决这一漏洞，LATTEO 提出三重防御机制：(1) **梯度混淆机制**，将结构相似性指数（SSIM）降低 85%，重构误差增加 400%；(2) **基于 TEE 的安全聚合**，在边缘设备的安全 enclave 中执行聚合操作；(3) **基于多授权机构属性基加密（MA-ABE）的新型数据中心化证明机制**，替代传统 enclave 远程证明。这一创新使客户端能够隐式验证 TEE 聚合服务、灵活处理按需客户端参与，并随异步连接数增加无缝扩展。

相比传统的 RA-TLS 远程证明，LATTEO 的证明机制将平均延迟降低多达 1500%。论文填补了异步联邦学习隐私保护的重要空白——此前大多数防御方案仅针对同步 FL 设计和评估，而异步场景缺乏协调更新、客户端参与变化更大、隐私风险更严重。这项工作由学术界与 Intel Labs 合作完成，展现了工业界对 TEE 在边缘 AI 中应用的关注。

---

## 5. TEE Is Not a Healer: Rollback-Resistant Reliable Storage (2026)

**作者：** Sadegh Keshavarzi, Gregory Chockler (University of Surrey), Alexey Gotsman (IMDEA Software Institute)

**来源：** DISC 2025 (39th International Symposium on Distributed Computing), arXiv:2505.18648

### 概述

本文从理论基础层面研究了 TEE 系统中的回滚攻击问题。虽然 TEE（如 Intel SGX、ARM TrustZone）可以显著降低拜占庭容错成本，但其保护仅在程序执行期间有效。一旦断电，非易失性存储中的程序状态面临回滚攻击——被不可检测地替换为旧版本。

论文引入了崩溃-重启-回滚（Crash-Restart-Rollback, CRR）统一故障模型，形式化了 TEE 系统中可能发生的多种故障类型。在此模型下，研究者研究了在异步消息传递系统中由 n 个 CRR 故障副本实现可靠读写寄存器的问题，考虑了静态（故障阈值先验固定）和动态（任意多副本可回滚，但频率受限）两种情况，并建立了紧密的容错边界。

核心算法 TEE-Rex 是首个正确实现分布式状态恢复的过程，既不需要持久存储也不需要可信单调计数器等专用硬件。这一成果具有理论意义——它证明了在动态故障模型下，仅通过消息传递和 TEE 的基本属性即可实现可靠存储，无需额外硬件信任根。论文发表于分布式计算顶级会议 DISC 2025，代表了 TEE 系统可靠性研究的理论前沿。

---

## 6. DistilLock: Safeguarding LLMs from Unauthorized Knowledge Distillation on the Edge (2025)

**作者：** Asmita Mohanty, Gezheng Kang, Lei Gao, Murali Annavaram (USC, UC Davis)

**来源：** NeurIPS 2025 Workshop: Lock-LLM, arXiv:2510.16716

### 概述

DistilLock 解决了大语言模型（LLM）在边缘设备上安全微调时的知识产权保护问题。传统方案面临两难：云端微调需要上传敏感数据引发隐私担忧；边缘微调则需将专有模型传输到不可信设备，面临模型窃取风险。

DistilLock 采用 TEE 辅助的知识蒸馏框架：(1) 专有基础模型在数据所有者设备的 TEE enclave 内作为黑盒教师执行，同时保护数据隐私和模型 IP；(2) 模型混淆机制将混淆后的权重卸载到不可信加速器（如 GPU）进行高效计算，避免 TEE 内完整模型前向传播的巨大开销；(3) TEE 仅用于轻量授权，混淆后的权重虽功能可用但无法逆向工程。蒸馏完成后，混淆教师被销毁，仅保留针对用户任务定制的蒸馏学生模型。

评估表明 DistilLock 能有效防止未授权知识蒸馏和模型窃取攻击，即使对手尝试在混淆模型上进行替代训练。框架引入的计算开销极小，通过轻量 TEE 授权和混淆模型卸载实现实用性能。这项工作发表于 NeurIPS 2025 Lock-LLM Workshop，代表了 TEE 在 LLM 安全部署领域的前沿应用。

---

## 7. SecureInfer: Heterogeneous TEE-GPU Architecture for Privacy-Critical Tensors for Large Language Model Deployment (2025)

**作者：** Tushar Nayan, Ziqi Zhang, Ruimin Sun (Florida International University, UIUC)

**来源：** arXiv:2510.19979, 2025年10月

### 概述

SecureInfer 提出了一种异构 TEE-GPU 混合架构，用于在边缘平台安全部署 LLM 推理。随着 LLM 在移动和边缘设备上的部署增加，模型提取攻击成为紧迫威胁——对手可通过块级表示、注意力分数、KV 缓存或完整 logits 泄露模型信息。

SecureInfer 的核心是信息论和威胁驱动的模型分区策略：安全敏感组件（非线性层、注意力头投影、FFN 变换、LoRA 适配器）在 Intel SGX enclave 内执行；计算密集的线性操作（矩阵乘法）在加密后卸载到 GPU，结果在 enclave 内安全还原。这种分区基于对 Transformer 各层信息泄露风险的细粒度分析，而非简单的启发式隔离。

基于 LLaMA-2 模型的原型实现和评估显示，SecureInfer 在提供强安全保证的同时保持了合理性能。与 DistilLock 不同，SecureInfer 专注于推理阶段而非训练/微调，两者互补地覆盖了 LLM 生命周期的安全需求。论文首次系统研究了 LLM 推理中的模型分区安全问题，超越了此前针对 CNN/DNN 的防御方法。

---

## 8. Proof of Trusted Execution: A Consensus Paradigm for Deterministic Blockchain Finality (2025)

**作者：** Kyle Habib, Vladislav Kapitsyn, Giovanni Mazzeo, Faisal Mehrban (Trillion.xyz, University of Naples)

**来源：** arXiv:2512.09409, 2025年12月

### 概述

本文提出了可信执行证明（Proof of Trusted Execution, PoTE），一种基于 TEE 的区块链共识新范式。现有共识协议存在结构性局限：PoW 能耗高且确认延迟大；PoS 存在权益集中、长程攻击和"无利害关系"漏洞，且受限于 slot 时间和多轮委员会投票的性能天花板。

PoTE 的核心思想是将共识从"复制重执行"转变为"验证已执行"。验证者在异构基于 VM 的 TEE 中运行，执行相同的规范程序（measurement 公开记录），并生成供应商支持的证明将 enclave 代码哈希绑定到区块内容。由于执行确定性和提议者从公共随机性唯一推导，PoTE 避免了分叉、消除了 slot 时间瓶颈，并在单轮验证中提交区块。

论文描述了 PoTE 共识客户端的设计和参考实现，并针对 Trillion 去中心化交易所的高吞吐需求进行了性能评估。PoTE 的理论贡献在于证明 TEE 可用于简化共识协议到近乎确定性的单轮确认，这对 DeFi 等对延迟敏感的应用具有重要意义。该工作体现了区块链与 TEE 技术深度融合的趋势，为高吞吐去中心化系统提供了新范式。

---

## 9. OmniIntent: A Trusted Intent-Centric Framework for User-Friendly Web3 (2026)

**作者：** Zhuoran Pan, Yue Li, Zhi Guan, Jianbin Hu, Zhong Chen (Peking University, Taiyuan University of Technology)

**来源：** WWW 2026 (The Web Conference 2026), arXiv:2603.04168

### 概述

OmniIntent 是一个语言-运行时协同设计框架，通过 TEE 实现 Web3/DeFi 的意图驱动交互。现有方案在表达性、信任、隐私和可组合性之间存在权衡：类型化意图设计表达能力有限，LLM 驱动的求解器存在信任和隐私问题。

OmniIntent 包含三个核心组件：(1) **ICL（Intent-Centric Language）**，一种领域特定语言，用于精确灵活地指定触发条件、动作和运行时约束；(2) **基于 TEE 的编译器**，在 enclave 内将意图编译为签名的、状态绑定的交易；(3) **执行优化器**，构建交易依赖图实现安全并行批量提交，并提供 mempool 感知的可行性检查器预测执行结果。

全栈原型在多种 DeFi 场景下实现 89.6% 的意图覆盖率，通过并行执行获得最高 7.3 倍的吞吐量加速，可行性预测准确率高达 99.2% 且延迟低。TEE 在此框架中承担关键角色：确保意图编译的完整性、防止求解器篡改用户意图、保护用户交易隐私。论文发表于 Web 领域顶级会议 WWW 2026，代表了 TEE 在 Web3 用户交互层面的创新应用。

---

## 10. Privacy-Preserving AI-Enabled Decentralized Learning and Employment Records System (2026)

**作者：** Yuqiao Xu, Mina Namazi, Sahith Reddy Jalapally, Osama Zafar, Youngjin Yoo, Erman Ayday (Case Western Reserve University, LSE)

**来源：** arXiv:2601.02720, 2026年1月

### 概述

本文提出了一个基于 TEE 和区块链的去中心化学历与就业记录（LER）系统。现有基于区块链的可验证凭证平台缺乏自动技能凭证生成和非结构化学习证据整合能力。

系统的核心创新在于 TEE 与 NLP 的深度结合：(1) 教育机构的数字签名成绩单被接受后，在 TEE enclave 内通过 NLP 管线分析正式记录（成绩单、教学大纲）和非正式学习成果，自动生成可验证的自我签发技能凭证；(2) 所有验证和职位-技能匹配在 enclave 内执行，支持选择性披露，原始凭证和私钥始终不离开 enclave；(3) 职位匹配仅依赖经证明的技能向量，不受简历中非技能字段影响，从而减少筛选偏见。

NLP 组件在样本学习者数据上的评估显示，多次运行的顶级技能排名方差低于 5%。论文提供了形式化安全声明和证明概要，证明派生凭证不可伪造且敏感信息保持机密。这项工作展示了 TEE 在去中心化身份和教育凭证领域的实际应用价值，将硬件信任根与 AI 技术结合以解决真实世界问题。

---

## 综合对比分析

### 研究主题分布

本批次论文反映了 TEE 研究的几个主要趋势：

1. **TEE + 机器学习安全**（DistilLock、SecureInfer、GPU TEE Overheads、LATTEO）是最大热点，涵盖推理、训练、联邦学习等场景。核心挑战在于 TEE 的性能开销（尤其是 GPU TEE 的加密通信开销）与 ML 计算密集需求之间的张力。DistilLock 和 SecureInfer 均采用 TEE-加速器混合架构，将安全敏感操作置于 enclave 而将计算密集操作卸载，体现了"最小化 TEE 内计算"的设计哲学。

2. **TEE + 区块链/Web3**（PoTE、OmniIntent）展现了 TEE 在去中心化系统中的双重角色：既作为共识加速器（PoTE 将 BFT 简化为单轮确认），又作为可信执行中间件（OmniIntent 在 enclave 内编译用户意图）。这反映了行业对 TEE 在 DeFi 高吞吐场景中实用价值的认可。

3. **TEE 基础设施与理论**（TEE-based KVS Survey、Jodes、TEE Is Not a Healer）则从数据库系统和分布式计算理论角度推进 TEE 研究。KVS Survey 系统总结了 TEE 存储系统的设计空间；Jodes 解决了分布式遗忘计算的关键操作符；TEE Is Not a Healer 从形式化模型出发建立 TEE 系统容错的理论边界。

4. **TEE + AI 应用落地**（Privacy-Preserving LER）展示了 TEE 与 NLP 结合在教育凭证领域的创新应用。

### 技术共性

- **分区策略**是 TEE 系统设计的核心：几乎每篇论文都涉及如何将计算/数据分为 TEE 内和 TEE 外两部分（SecureInfer 的模型分区、DistilLock 的教师-学生分离、KVS 的索引-数据分离）。
- **证明机制创新**是活跃研究方向：LATTEO 用 MA-ABE 替代传统远程证明，OmniIntent 用 TEE 编译实现意图完整性，PoTE 用供应商证明绑定区块内容。
- **性能与安全的权衡**始终是核心张力：GPU TEE Overheads 量化了这一开销（最高 41.6× 减速），而各系统通过混合架构、批量传输、异步操作等策略缓解。

### 交叉引用

- SecureInfer 和 DistilLock 均面向 LLM 的 TEE 保护，前者关注推理 [7]，后者关注训练/蒸馏 [6]，可视为互补方案。两者都采用了 TEE-GPU 混合卸载策略，区别在于分区粒度——SecureInfer 基于信息论分析各层泄露风险，DistilLock 则专注于教师模型的黑盒保护。
- GPU TEE Overheads [3] 的实证数据为 SecureInfer [7] 和 DistilLock [6] 的混合架构设计提供了动机依据：纯 TEE 执行 ML 任务的不可行性驱动了卸载方案的研究。
- PoTE [8] 和 OmniIntent [9] 均利用 TEE 的确定性执行属性服务 Web3 场景。PoTE 聚焦共识层，将验证者置于 TEE 实现单轮确认；OmniIntent 聚焦应用层，在 TEE 内编译意图保证完整性。
- Jodes [2] 和 KVS Survey [1] 同属 TEE 数据库基础设施。Jodes 解决的遗忘等值连接是 TEE 数据库的关键操作符，而 KVS Survey 中讨论的侧信道攻击缓解（如 ORAM）正是 Jodes 所应对的威胁。
- LATTEO [4] 和 TEE Is Not a Healer [5] 从不同角度处理 TEE 的"非完美性"：LATTEO 应对异步 FL 的梯度泄露（侧信道问题），TEE Is Not a Healer 应对持久状态的回滚攻击（离线攻击问题）。

---

*本综述由自动化流程生成于 2026-04-26，涵盖 2025-2026 年发表的 TEE 相关论文。*
