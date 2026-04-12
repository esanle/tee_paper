# TEE 论文批次综述

**批次目录：** `/tmp/tee_paper/2026-04-12-12-41-20/`
**生成时间：** 2026-04-12 12:41:20 (GMT+12)
**论文总数：** 16 篇（均为重复下载，已存在于其他会话目录）
**arXiv ID 范围：** 2501.02350 ~ 2604.04082

---

## ⚠️ 重要说明

本目录中的 **16 篇 PDF 论文均已在其他会话目录中出现并处理过**（通过哈希去重确认）。本 README 为重复覆盖文档，旨在保持该时间戳目录的完整性。所有论文原文已存在于 `/tmp/tee_paper/` 的其他历史目录中，提取文本存放于 `/tmp/tee_paper_log/pdf_text_{arxiv_id}.txt`。

---

## 综述：可信执行环境（TEE）研究全景

### 一、总体趋势

本批次 16 篇 TEE 论文跨越 2025 至 2026 年，覆盖了 TEE 技术从**底层硬件架构**到**上层应用生态**的完整研究光谱。综合来看，当前 TEE 研究呈现以下几个核心趋势：

#### 1. 应用场景的极速扩展
从最早聚焦于加密和移动支付，TEE 的触角已深入**卫星计算（Space Fabric）**[SpaceFabric-2026]**、学术可复现性（TEE Replication Crisis）**[TEERepCrisis-2026]**、LLM 推理保护（Partial TEE LLM）**[PartialTEE-LLM-2026]**、IoT 生态（Keyfort、External Entropy IoT）**[Keyfort-2026][ExternalEntropyIoT-2026]等前沿领域。传统区块链和加密货币不再是 TEE 的主战场，取而代之的是 **AI 模型保护**——这一趋势在 [WhatYouTrust-2025] 的大规模实证研究中得到量化印证：AI 模型保护相关项目占实际 TEE 项目的 12%，且增长迅速。

#### 2. TEE 本身的脆弱性被深度审视
一批论文开始"反身性"研究 TEE 的安全问题。[WhatYouTrust-2025] 通过分析 241 个 GitHub 项目发现 **25.3% 的项目存在不安全编码实践**（硬编码密钥、缺失输入验证等），32.4% 的项目绕过了官方 SDK 加密 API 而选择自行实现。[PartialTEE-LLM-2026] 则揭示了部分 TEE 屏蔽 LLM 推理中**密钥复用**的密码学缺陷，可在约 6 分钟内恢复 LLaMA-3 8B 模型的全部权重和秘密。[TriadTTP-2025] 证明 Triad 可信时间协议的校准机制存在漏洞，恶意操作系统可以操纵时钟速度并向诚实节点传播任意未来时间戳。

#### 3. 抽象层与工程化：从"能用"到"好用"
[AbstractionTEE-2025] 的系统化综述指出，TEE 生态高度碎片化是阻碍广泛采用的核心瓶颈——不同厂商的 TEE（Intel SGX、AMD SEV、ARM TrustZone、RISC-V Keystone 等）互不兼容。WebAssembly 被认为是当前**支持最全面特征集**的抽象层方案。[AutoTEE-2025] 则利用 LLM 自动将 Java/Python 程序中的敏感函数识别并迁移至 TEE，在 Java 上达到 0.94 的 F1 分数，转换成功率达 91.8%，极大降低了 TEE 的工程门槛。

#### 4. 跨组件信任与数据全生命周期保护
[Mica-2026] 和 [Styx-2026] 均针对一个核心问题：**TEE 之间以及 TEE 与不可信环境之间的通信如何保证机密性？** Mica 提出在 Arm CCA 上扩展策略语言，使各 Realm 之间以及与不可信世界之间的通信路径可被显式定义、限制和证明；Styx 则将"粘性策略"（sticky policy）与 TEE 结合，通过 I/O 管道和运行时沙箱实现数据全生命周期保护（输入保护→处理保护→输出保护→派生数据保护）。

#### 5. 经济模型与安全定量化
[TEEBFT-2025] 首次将**博弈论定价框架**引入 TEE 安全研究，通过共谋成本-收益模型推导出 K-of-n 阈值下理性共谋的边界条件，论证了在合理假设下协议可保护约 **1 万亿美元**价值免受 TEE 破坏——这是 TEE 安全研究中首次尝试将安全保证量化为经济参数。

#### 6. 垂直领域的深度定制
- **卫星/太空：** [SpaceFabric-2026] 利用卫星发射后的物理不可访问性作为防篡改屏障，实现了在轨密钥生成（无预置秘密）、零预发射秘密窗口、双安全元件交叉验证
- **汽车/IoT：** [Keyfort-2026] 为 RISC-V TEE 补充了安全更新时间、状态迁移和可信计时能力（填补了现有 TEE 对软件生命周期支持的空白），TCB 仅增加约 750 行代码
- **学术出版：** [TEERepCrisis-2026] 以约 $1.35–$1.80/package 的低成本证明 TEE 可替代传统数据编辑实现可复现性验证
- **归因验证：** [TEEProcessAttest-2026] 将 TEE 用于写作过程证明（防伪造写作证据链），提供三级输入保证和 >99.5% 的证据链可用性

### 二、技术主题交叉地图

| 主题 | 相关论文 |
|------|----------|
| LLM + TEE 安全 | [PartialTEE-LLM-2026], [WhatYouTrust-2025] |
| 抽象层与可移植性 | [AbstractionTEE-2025], [AutoTEE-2025] |
| TEE 间通信/多组件 | [Mica-2026], [Styx-2026] |
| 侧信道与微架构攻击 | [TriadTTP-2025], [WhatYouTrust-2025], [PartialTEE-LLM-2026] |
| RISC-V TEE | [Keyfort-2026], [ExternalEntropyIoT-2026], [SpaceFabric-2026] |
| 云端机密计算 | [PM-Dedup-2025], [TEEBFT-2025], [TEERepCrisis-2026] |
| IoT 与边缘 | [PM-Dedup-2025], [ExternalEntropyIoT-2026], [Keyfort-2026] |
| 决策支持系统 | [SPARTA-2025] |
| LLM 安全顾问红队 | [RedTeamingTEE-2026] |
| 卫星/太空计算 | [SpaceFabric-2026] |
| 软件开发生命周期 | [Keyfort-2026] |
| 学术可复现性 | [TEERepCrisis-2026] |
| 过程证明/归因 | [TEEProcessAttest-2026] |
| 经济安全模型 | [TEEBFT-2025] |
| 边缘去重 | [PM-Dedup-2025] |

### 三、核心发现与局限性

**核心发现：**
1. **TEE 开发者实践与学术假设严重脱节**：大多数开发者绕过官方 SDK API，32.4% 选择重实现加密功能，25.3% 存在不安全编码行为 [WhatYouTrust-2025]
2. **部分 TEE 屏蔽范式存在根本性密码学缺陷**：预计算噪声机制引入密钥复用，破坏了 LLM 模型保护的核心假设 [PartialTEE-LLM-2026]
3. **TEE 信任边界的语言化是打通规模化应用的关键**：抽象层 [AbstractionTEE-2025] 和自动化迁移工具 [AutoTEE-2025] 代表了降低 TEE 使用门槛的两个互补方向
4. **可信时间仍是 TEE 领域的开放难题**：Triad 协议的漏洞表明，即使是协作式可信时间协议也难以抵御恶意操作系统的调度操纵 [TriadTTP-2025]

**核心局限：**
- 大量研究仍基于 Intel SGX，跨平台可移植性存疑
- 侧信道攻击的防护仍是未解问题，多篇论文将侧信道作为已知威胁模型边界
- 经济模型 [TEEBFT-2025] 高度依赖校准参数假设，实际可操作性有待验证

---

## 各论文详细摘要

---

### 1. PM-Dedup：基于云到边缘服务器部分迁移的安全去重

**arXiv ID：** 2501.02350
**标题：** PM-Dedup: Secure Deduplication with Partial Migration from Cloud to Edge Servers
**作者：** Zhaokang Ke, Haoyu Gong, David H.C. Du（明尼苏达大学）
**发表：** 2025年1月

#### 摘要（约1000字）

云存储服务中海量数据的重复率极高（备份存储中冗余数据可达90%~95%），数据去重技术是节省存储空间的关键手段。然而，当用户对云端数据安全心存顾虑而选择加密上传时，传统加密方案会导致相同内容的密文因密钥不同而无法被识别为重复，严重削弱去重效果。收敛加密（Convergent Encryption）通过以数据内容哈希作为加密密钥，使相同数据生成相同密文，从而支持加密环境下的去重。

现有加密去重方案分为两类：**目标端去重**要求客户端将所有密文块上传至云端再执行去重，带宽开销巨大；**源端去重**则先上传密文指纹至云端进行重复检查，仅上传唯一块，但引入了三方面问题：易受侧信道攻击（猜测指纹推断云端数据存在性）、高延迟（额外往返通信和 PoW 挑战响应）、云端计算负载繁重。

PM-Dedup 的核心思想是：**将原本在云端执行的去重检查和所有权证明（PoW）任务迁移至客户端边缘服务器的 TEE（Intel SGX）中进行**。在单一组织（多分支机构）场景下，同一组织内的客户端共享公共数据的概率更高，边缘服务器可以就近处理去重和 PoW，显著降低延迟和云端开销。

具体而言，PM-Dedup 包含四个核心组件：
1. **高效共享索引生成（Share-Index Generation）**：云端预选高影响力的指纹子集（share-index）下发给边缘服务器，使边缘可直接进行去重判断，减少与云端的交互次数。
2. **双层轻量响应式 PoW**：在文件级和块级分别执行 PoW，结合云端预计算挑战-响应对（而非实时生成），大幅缩短 PoW 验证时间。
3. **基于 SGX 的安全迁移**：所有关键操作（去重检查、PoW 验证）均在边缘服务器 SGX Enclave 内执行，防止恶意操作系统干扰。
4. **安全信息共享机制**：云端下发给边缘的共享索引和预计算挑战-响应对通过 SGX 远程证明机制保护，确保传输安全。

#### 关键贡献

- 首个将 TEE 应用于客户端边缘服务器执行安全源端去重的研究工作
- 提出了云端预计算挑战-响应对的优化设计，显著降低 PoW 延迟
- 在单组织多分支场景下，量化分析了带宽节省和延迟降低效果

#### 引用

[PM-Dedup-2025] Z. Ke, H. Gong, D. H. C. Du. "PM-Dedup: Secure Deduplication with Partial Migration from Cloud to Edge Servers." *arXiv:2501.02350*, Jan. 2025.

---

### 2. AutoTEE：利用大语言模型自动识别、转换和迁移程序敏感函数至 TEE

**arXiv ID：** 2502.13379
**标题：** Automated TEE Adaptation with LLMs: Identifying, Transforming, and Porting Sensitive Functions in Programs
**作者：** Ruidong Han, Zhou Yang, Chengyan Ma, Ye Liu, Yuqing Niu, Siqi Ma, Debin Gao, David Lo（新加坡管理大学、阿尔伯塔大学、卧龙岗大学）
**发表：** 2025年2月（2026年3月更新至v3）

#### 摘要（约1000字）

TEE 通过在硬件隔离的内存区域中执行敏感代码，为软件程序提供强有力的安全保护。然而，将现有程序适配以利用 TEE 安全能力面临两大核心挑战：其一，**细粒度安全关键代码的识别**需要开发者同时精通应用逻辑和 TEE 安全模型；其二，**TEE 执行环境受限**——大多数 TEE 仅支持低级代码（C/Rust），不原生支持 Java、Python 等高级语言，且 TEE 中的 API 和系统调用与普通世界存在差异（如 Intel SGX 不支持定时器、文件 I/O 和多线程）。

现有解决方案分为两类：移植高级语言运行时至 TEE（开销大、安全性弱）或手动指定数据并转换程序（复杂且易出错。实践中，TEE 适配仍以人工为主，亟需自动化工具。

AutoTEE 是**首个基于大语言模型（LLM）的自动化 TEE 适配框架**，核心流程包含以下步骤：
1. **函数提取**：对给定程序（Java/Python）生成抽象语法树（AST），提取不含用户定义调用的叶子函数（leaf functions）作为最小粒度迁移单元。
2. **敏感函数识别**：利用 LLM 审查每个叶子函数，识别涉及加密操作、序列化等敏感操作的函数，在评测集上达到 Java 平均 F1=0.94、Python 平均 F1=0.87。
3. **代码转换与迭代精化**：通过 ReAct 策略引导 LLM 将识别出的敏感函数转换为功能等价的原生代码实现。转换过程中，AutoTEE 借助编译器反馈和覆盖率分析工具（线覆盖率、分支覆盖率）迭代改进测试输入，提升转换质量。
4. **功能等价性验证**：对每个转换后的函数，在 LLM 生成的测试输入上比对原始函数与转换后代码的输出，确保功能一致性。
5. **集成与远程证明**：通过基于端口的通信机制将 TEE 验证版本重新集成至原程序，替换原始函数实现为对 Enclave 中对应版本的远程调用。

评测数据集由研究者手动构建，来源于 68 个代码仓库共 385 个敏感叶子函数。使用 GPT-4o 进行转换时，Java 代码成功率达 91.8%，Python 为 84.3%。

#### 关键贡献

- 首个完全自动化的 TEE 程序适配框架，降低 TEE 技术使用门槛
- 提出基于 AST 的细粒度函数识别与基于 ReAct 的迭代代码转换方法
- 覆盖 Java 和 Python 两种主流高级语言，具有广泛的工程适用性

#### 引用

[AutoTEE-2025] R. Han et al. "Automated TEE Adaptation with LLMs: Identifying, Transforming, and Porting Sensitive Functions in Programs." *arXiv:2502.13379*, Feb. 2025.

---

### 3. Triad 可信时间协议的开源实现与安全分析

**arXiv ID：** 2507.20851
**标题：** An Open-source Implementation and Security Analysis of Triad's TEE Trusted Time Protocol
**作者：** Matthieu Bettinger, Sonia Ben Mokhtar（INSA Lyon, CNRS）、Anthony Simonet-Boulogne（iExec Blockchain Tech）
**发表：** 2025年7月（DSN-S 2025 补充卷）

#### 摘要（约1000字）

许多协议逻辑依赖时间测量。在 Intel SGX 等 TEE 中，时间源位于 TCB 之外——恶意系统软件可以操纵 TEE 的时间感知，例如加速时间或跳跃至任意未来时间戳。这对时间戳权威机构（TSA）、Proof-of-Elapsed-Time、凭证过期撤销、延迟敏感系统（交易、实时系统）、BFT 共识等场景构成严重威胁。

Triad 是一个针对 TEE 可信时间的协作式协议，其核心设计思路是：将多个 TEE 组织为集群，通过 AEX-Notify（异步 Enclave 退出通知）机制检测时间连续性被破坏的时刻，然后从集群中的对等 Enclave 或时间权威（TA，如 NTP 服务器）获取时间刷新。然而，**原版 Triad 为闭源实现**（基于专有容器化方案 Scone），缺乏公开可用的实现和攻击验证。

本文的贡献是双重的：首先，**作者贡献了 Triad 的首个开源实现**（基于公开协议规范的独立重实现）；其次，**通过实验发现了 Triad 协议的多个安全漏洞**：

**Calibration 协议攻击**：Triad 依赖 TSC（时间戳计数器）的校准来建立 TSC 增量与真实时间的关系。恶意操作系统通过控制调度（减少中断频率），可影响校准精度，使 TEE 高估或低估时钟速度。

**时钟速度操纵攻击**：攻击者控制操作系统即可任意调整其本地 TEE 的时钟速度感知。在 Triad 集群中，感染节点可向诚实节点传播任意未来的时间戳，随后被感染的诚实节点进一步向其他诚实节点传播，造成**时间跳跃在集群中呈指数级级联传播**。

**修复方向**：论文讨论了若干协议改进方向，包括：更robust的校准协议（防止低中断率强化攻击）、节点间时间差异的主动监控、以及更保守的时间回退策略。

#### 关键贡献

- 首个 Triad 协议的开源实现（独立于原厂 Scone 实现）
- 首个通过实验验证的 Triad 协议攻击（时钟操纵、校准协议漏洞及其集群级联传播）
- 提出了针对上述攻击的协议改进思路

#### 引用

[TriadTTP-2025] M. Bettinger, S. Ben Mokhtar, A. Simonet-Boulogne. "An Open-source Implementation and Security Analysis of Triad's TEE Trusted Time Protocol." *arXiv:2507.20851*, Jul. 2025.

---

### 4. SPARTA：基于 TEE 的决策支持安全与隐私方法

**arXiv ID：** 2509.02413
**标题：** A TEE-based Approach for Security and Privacy in Decision Support
**作者：** Edoardo Marangone, Eugenio Nerio Nemmi, Daniele Friolo（罗马大学）、Giuseppe Ateniese（乔治梅森大学）、Ingo Weber（慕尼黑工业大学 & 弗劳恩霍夫协会）、Claudio Di Ciccio（乌得勒支大学）
**发表：** 2025年9月

#### 摘要（约1000字）

决策支持系统（DSS）被广泛应用于医疗、金融、商业和供应链等领域，通过数据驱动洞察和分析工具提升决策质量。然而，在多方协作场景中，如何在保证数据隐私、完整性和可用性的同时实现决策逻辑的可定制性、安全性和可验证性，仍是悬而未决的难题。

现有方案存在明显短板：中心化系统牺牲了数据隐私和可用性；依赖云平台的方案将数据和决策逻辑暴露给第三方；基于加密的隐私保护方案引入单点失败或高昂开销；而区块链方案虽保证可用性，但将输入数据和处理过程公开暴露，无法保护隐私。

SPARTA（Secure Platform for Automated decision Rules via Trusted Applications）提出了一种基于 TEE 的多方协作决策支持架构，核心技术栈包括：
- **Intel SGX Enclave**：在硬件隔离环境中安全执行决策逻辑
- **IPFS 分布式存储**：加密数据分布式存储，保证可用性
- **公链存证**：使用区块链作为存证系统，保证信息完整性并支持授权访问审计
- **DMN（Decision Model and Notation）**：标准化决策规则描述语言，支持用户自定义决策逻辑
- **ALFA（Abbreviated Language for Authorization）**：基于属性的访问控制策略语言，实现细粒度授权

系统工作流程：参与方将加密数据上传至 IPFS，并通过 ALFA 策略控制访问权限；SPARTA 在 SGX Enclave 内根据 DMN 规则处理数据，仅返回决策结果（不暴露原始数据）；每一步决策均生成区块链存证，支持后续审计和追溯。

实验结果表明，SPARTA 在公开基准数据集和合成数据上均具有良好的可扩展性，引入的安全机制带来的性能开销相对于非加密方案处于可接受范围内。

#### 关键贡献

- 首个将 TEE、DMN 决策标准与 ALFA 访问控制策略完整结合的多方决策支持架构
- 在保护数据机密性的同时实现决策逻辑的可定制化和可验证性
- 开源实现，提供了可复现的原型系统

#### 引用

[SPARTA-2025] E. Marangone et al. "A TEE-based Approach for Security and Privacy in Decision Support." *arXiv:2509.02413*, Sep. 2025.

---

### 5. TEEBFT：Proof of Cloud 安全性的定价框架

**arXiv ID：** 2510.26091
**标题：** TEEBFT: Pricing the Security of Proof of Cloud
**作者：** Alex Shamis, Matt Stephenson, Linfeng Zhou（Subzero Labs）
**发表：** 2025年10月（2025年11月更新至v3）

#### 摘要（约1000字）

区块链在与外部系统交互时存在固有局限性，TEE 作为有前景的解决方案，允许可信中介与外部系统接口。现有关于 TEE 安全的讨论大多停留在技术层面，缺乏对**攻击者理性动机**的经济学分析。

TEEBFT 首次将**共谋成本-收益框架（cost-of-collusion principal-agent model）**应用于 Data Center Execution Assurance 设计中的 TEE 安全建模。模型聚焦于四个核心决定因素：

1. **K-of-n 共谋阈值**：系统事件（如阈值解密）需要至少 K 个提供商协同触发
2. **检测概率 q**：每个成员的独立检测概率
3. **成员制裁 Fi**：被发现后每个成员面临的罚金（包括法律、声誉和资产负债表暴露）
4. **可提取流动奖励 ω = βV**：区别于系统总"存量"价值 V 的"流量"奖励，β ∈ (0,1] 表示可被在攻击窗口内提取的比例

模型推导出：（a）理性共谋的条件——即 Fi、q、ω、K、n 满足何种关系时共谋有利可图；（b）威慑阈值的闭合形式解——展示各参数如何影响理性共谋边界；（c）设计边界——即如何调整参数保证"即使能实现共谋也无法盈利"。

校准依据包括时间优势套利分析和安全漏洞代价估算。论文论证了在合理参数下，协议可保护约 **1 万亿美元**量级的价值免受 TEE 破坏。这一数字的意义在于：它为"多高的安全投入是合理的"提供了经济学依据，而不仅仅依赖定性安全讨论。

#### 关键贡献

- 首个将博弈论与经济模型引入 TEE 安全性的量化研究
- 推导出理性共谋边界的设计条件，提供可操作的协议安全参数指导
- 论证了 TEE-BFT 设计在宏观金融规模上的经济可行性

#### 引用

[TEEBFT-2025] A. Shamis, M. Stephenson, L. Zhou. "TEEBFT: Pricing the Security of Proof of Cloud." *arXiv:2510.26091*, Oct. 2025.

---

### 6. 你所信任的并不安全：开发者实际使用 TEE 的首次大规模实证研究

**arXiv ID：** 2512.17363
**标题：** What You Trust Is Insecure: Demystifying How Developers (Mis)Use Trusted Execution Environments in Practice
**作者：** Yuqing Niu, Jieke Shi, Ruidong Han, Ye Liu, Chengyan Ma, Yunbo Lyu, David Lo（新加坡管理大学）
**发表：** 2025年12月（2026年1月更新至v3）

#### 摘要（约1000字）

TEE 已成为移动支付、数字货币钱包、远程证明等场景的基石，但**我们实际上对开发者如何在真实项目中运用 TEE 知之甚少**。现有研究主要分析 TEE 相关移动二进制文件或整理学术文献，尚未有对真实开源项目中 TEE 使用实践的大规模定量调查。

本文通过对 **241 个 GitHub 开源项目**（使用 Intel SGX 和 ARM TrustZone）进行手动审查和定制静态分析，填补了这一研究空白。研究围绕三个维度展开：

**RQ1：TEE 被应用在哪些领域？**
- IoT 设备安全（30%）远超区块链安全（7%）——这与学术界长期聚焦于区块链形成鲜明对比
- AI 模型保护（12%）正在快速增长，契合大模型时代对模型知识产权保护的需求
- 加密操作（68.2%）仍是 TEE 最普遍的功能类型

**RQ2：TEE 的主流开发模式是什么？**
- **32.4% 的项目重实现了加密功能**而非使用官方 SDK API，表明现有 SDK 的可用性和可移植性存在严重不足（文档不清、API 抽象层级不合理）
- 此类重实现可能引入逻辑缺陷和侧信道漏洞

**RQ3：存在哪些不安全实践？**
- **25.3%（61/241）的项目存在不安全编码行为**，包括硬编码密钥和缺失输入验证
- 这些问题即使对于有意加强安全性的开发者也极易出现，说明 TEE 环境下的安全编程实践仍需更好支持

研究同时提出了针对 SDK 设计者和安全社区的启示：需降低 TEE 开发门槛、提供更清晰的 API 抽象，并建立针对 TEE 开发的安全编码规范和工具链。

#### 关键贡献

- 首个大规模真实项目 TEE 使用实证研究（241 个 GitHub 仓库）
- 揭示学术研究与实际应用之间的显著偏差（IoT 主导 vs. 区块链主导）
- 量化了 SDK 可用性问题（32.4% 重实现）和安全实践不足（25.3% 不安全编码）

#### 引用

[WhatYouTrust-2025] Y. Niu et al. "What You Trust Is Insecure: Demystifying How Developers (Mis)Use Trusted Execution Environments in Practice." *arXiv:2512.17363*, Dec. 2025.

---

### 7. TEE 抽象层：推动机密计算广泛采用的缺失环节

**arXiv ID：** 2512.22090
**标题：** Abstraction of Trusted Execution Environments as the Missing Layer for Broad Confidential Computing Adoption: A Systematization of Knowledge
**作者：** Quentin Michaud（Telecom SudParis, Thales）、Sara Ramezanian（隆德大学、卡尔斯塔德大学）、Dhouha Ayed（Thales）、Olivier Levillain、Joaquin Garcia-Alfaro（Telecom SudParis）
**发表：** 2025年12月

#### 摘要（约1000字）

机密计算（Confidential Computing）通过在硬件级隔离的 attestation 空间中执行计算来保护使用中的数据，是云安全的关键技术。然而，当前 TEE 生态存在两大核心碎片化问题：其一，**硬件实现高度碎片化**——Intel SGX、AMD SEV、ARM TrustZone、ARM CCA、Intel TDX、RISC-V Keystone/CURE/Sanctum 等方案各具不同的安全模型、API 和部署方式；其二，**机密计算应用需要适配特定硬件**，开发者在已有软件栈上引入机密计算时面临陡峭的学习曲线。

 abstraction 层（抽象层）正是解决这些问题的关键——它们在底层异构 TEE 硬件和上层应用之间建立统一接口，使开发者无需深入了解每种 TEE 的内部细节即可部署安全的机密计算应用。然而，现有的综述主要聚焦于 TEE 底层细节，缺乏对抽象层技术的系统梳理。

本文对 TEE 抽象层技术进行了系统化的知识梳理（SoK），主要内容包括：

**TEE 生态概览**：梳理了从进程级 TEE（SGX）到虚拟机级 TEE（TDX、SEV-SNP）再到开放架构 RISC-V TEE（Keystone、Sanctum、CURE）的设计选择与权衡。

**抽象层分类**：将现有抽象层技术分为四大类：
1. **SDK-based**：提供统一 API 封装底层 TEE 差异（如 Graphene、SCONE、Gramline）
2. **Container-based**：支持标准容器格式在 TEE 中运行（如 Inclavare Containers、Koacon）
3. **Language-based**：通过特定语言运行时提供抽象（如 WebAssembly、Rust+Enclave）
4. **其他形式**：包括联合学习框架、隐私保护 ML 框架等

**核心发现**：**WebAssembly 被认为是当前支持最全面特征集的抽象层方案**，其语言无关性、确定性执行沙箱和紧凑二进制格式使其特别适合 TEE 场景。同时指出了各抽象层方案在安全性、性能、可移植性之间的权衡取舍，以及未来研究方向（如抽象层的形式化验证、跨平台 attestation 标准等）。

#### 关键贡献

- 首个对 TEE 抽象层技术进行系统化分类和评估的综述
- 揭示 WebAssembly 作为 TEE 抽象层的突出优势
- 为机密计算生态的标准化和互操作性提供了清晰的发展路线图

#### 引用

[AbstractionTEE-2025] Q. Michaud et al. "Abstraction of Trusted Execution Environments as the Missing Layer for Broad Confidential Computing Adoption." *arXiv:2512.22090*, Dec. 2025.

---

### 8. 部分 TEE 屏蔽 LLM 推理中预计算噪声的漏洞研究

**arXiv ID：** 2602.11088
**标题：** Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise
**作者：** Abhishek Saini, Haolin Jiang, Hang Liu（罗格斯大学）
**发表：** 2026年2月

#### 摘要（约1000字）

在大语言模型（LLM）部署场景中，将模型知识产权保护在第三方设备上是一个核心挑战。纯密码学方案如同态加密（HE）性能开销过高，难以满足低延迟 LLM 推理需求。TEE 提供了一种更实用的替代方案，但其内存和性能限制使得在 TEE 内运行完整大模型并不现实。因此，**部分 TEE 屏蔽执行（Partial TEE-Shielded Execution, PTSE）** 成为主流范式——将计算密集型的线性操作卸载到强大的 GPU 等不可信硬件，而 TEE 负责管理整体执行流程并保护模型密钥和完整性。

PTSE 的核心技术模式为"掩码-卸载-恢复"（mask-offload-restore）：TEE 对输入数据施加掩码（mask）后卸载到 GPU；GPU 在掩码数据上执行线性操作后返回结果；TEE 移除掩码效应恢复明文输出，或通过指纹（fingerprint）机制验证 GPU 计算的完整性。

本文揭示了 PTSE 范式中一个**根本性的密码学缺陷**：为加速掩码操作而预计算并重用静态噪声（密钥材料），实质上引入了**密钥复用**问题，由此产生两类攻击：

**机密性攻击**：通过利用同一静态噪声基对多层模型进行统计分析，可完整恢复模型的秘密置换（secret permutation）和权重。实验表明，在约 **6 分钟内**即可从 LLaMA-3 8B 模型的一层中提取全部秘密，且该攻击可扩展至 **4050 亿参数**量级的大模型。

**完整性攻击**：完全绕过 Soter 和 TSQP 等系统的完整性检查机制。攻击者利用预计算噪声的固定结构，可以生成通过 TEE 指纹验证的虚假 GPU 计算结果，从而在不被检测的情况下篡改模型推理结果。

该漏洞影响范围广泛，涵盖 ShadowNet、SLIP、Soter、TransLinkGuard 等多个 PTSE 系统。论文同时讨论了潜在的防御方向。

#### 关键贡献

- 首次揭示 PTSE LLM 推理范式中预计算噪声引入的密钥复用安全漏洞
- 实证验证 6 分钟内恢复 LLaMA-3 8B 层级秘密，可扩展至 405B 参数模型
- 完整绕过现有 PTSE 完整性验证机制（Soter、TSQP）

#### 引用

[PartialTEE-LLM-2026] A. Saini, H. Jiang, H. Liu. "Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise." *arXiv:2602.11088*, Feb. 2026.

---

### 9. 红队测试 Claude Opus 和 ChatGPT：面向 TEE 的 AI 安全顾问风险评估

**arXiv ID：** 2602.19450
**标题：** Red-Teaming Claude Opus and ChatGPT-based Security Advisors for Trusted Execution Environments
**作者：** Kunal Mukherjee（弗吉尼亚理工大学）
**发表：** 2026年2月

#### 摘要（约1000字）

安全团队日益依赖通用大语言模型（LLM）助手作为 TEE 架构评审、缓解规划和漏洞分诊的安全顾问。然而，LLM 的幻觉（hallucination）、过度承诺安全保证（overclaiming）、对提示的敏感性等系统性弱点可能直接转化为不安全的系统设计建议。

本文首次对 **ChatGPT-5.2 和 Claude Opus-4.6** 担任 TEE 安全顾问角色进行红队测试研究，核心成果包括：

**TEE-RedBench 评估框架**：
- 基于 TEE 的威胁模型：涵盖 SGX 和 TrustZone 架构、attestation 和密钥管理、威胁建模、非操作性缓解指导，以及政策约束的滥用探测
- 结构化提示套件：覆盖微架构泄漏、故障注入、安全部署实践等领域
- 联合评分标准：同时衡量技术正确性、接地性（groundedness）、不确定性校准、拒绝质量和安全有用性五个维度

**核心发现**：
- 提示诱导的失败模式在两个 LLM 之间具有**12.02% 的跨模型可转移性**，说明部分失败并非 LLM 特有的偶发问题，而是系统性缺陷
- 典型失败类型包括：边界混淆（错误理解 TEE 信任边界）、Attestation 过度承诺（对远程证明语义的不准确描述）、缓解幻觉（生成现实中不存在或不安全的"缓解措施"）

**防御机制**：
- "LLM-in-the-loop" 评估管道：政策门控（policy gating）、检索接地（retrieval grounding）、结构化模板和轻量级验证检查四层防御
- 实验表明该管道可**降低 80.62% 的可转移失败率**

该研究将 LLM 安全顾问视为安全决策循环中的架构组件，其失效模式必须被系统化地识别、测量和缓解。

#### 关键贡献

- 首个针对 LLM 作为 TEE 安全顾问的全面红队研究
- 提出可量化的跨模型失败可转移性指标（12.02%）
- 构建 LLM-in-the-loop 防御框架，显著降低不安全建议的风险

#### 引用

[RedTeamingTEE-2026] K. Mukherjee. "Red-Teaming Claude Opus and ChatGPT-based Security Advisors for Trusted Execution Environments." *arXiv:2602.19450*, Feb. 2026.

---

### 10. 基于 TEE 的机密可信过程证明架构：写作归因验证

**arXiv ID：** 2603.00178
**标题：** A TEE-Based Architecture for Confidential and Dependable Process Attestation in Authorship Verification
**作者：** David Condrey（Writerslogic, Inc.）
**发表：** 2026年2月

#### 摘要（约1000字）

过程证明（Process Attestation）系统验证连续物理过程（如人类写作）是否真实发生，而非仅检查系统状态。这类系统在写作归因、在线监考等场景中具有重要价值。然而，**证明基础设施本身必须在证明方控制平台时仍保持可用性和防篡改性**——这构成了一种"信任反转"（trust inversion）：证明方可能就是 adversary，有动机伪造证据。

TEE 通过硬件级隔离将信任问题从"adversary 控制一切"转化为"adversary 控制除 Enclave 以外的一切"，但将 TEE 与连续过程证明结合引入了新的**可用性需求**：Enclave 可能崩溃（硬件故障、断电、操作系统终止），侧信道在边界内泄漏有限信息，证据链具有顺序性和累积性（间隙可能导致数小时前的证据无效）。

本文提出**首个在 TEE Enclave 内实现连续过程证明证据收集的架构**，核心设计包括：

**三级输入保证**：
- Tier 1（软件级）：HMAC 保护的共享内存 + RA-TLS 会话密钥
- Tier 2（OS中介级）：内核级输入钩子（如 Linux evdev）
- Tier 3（硬件绑定级）：安全输入路径（如 TrustZone 可信输入控制器）

**证据链协议**：每 30 秒检查点使用 Argon2id-seeded SHA256 链生成时间证明（Sequential Work Functions），结合 CDCE（Cross-Domain Constraint Entanglement）将内容、行为和时间证据绑定在 HMAC 下，实现跨检查点的证据链连续性。

**马尔可夫链可用性模型**：推导出 ECA（Evidence Chain Availability）、MTBEG（Mean Time Between Evidence Gaps）和 RTO（Recovery Time Objectives）的闭合形式表达式。

**评估结果（Intel SGX）**：每次检查点 CPU 开销 <25%（远低于 30 秒间隔的 0.3% 实际占比）；蒙特卡洛模拟下 ECA >99.5%；密封状态恢复时间 <200ms。

#### 关键贡献

- 首个 TEE 内连续过程证明的完整架构设计
- 提出三级梯度输入保证机制和马尔可夫链可用性分析
- 在 Intel SGX 上验证了 <25% CPU 开销和 >99.5% ECA 的实用性指标

#### 引用

[TEEProcessAttest-2026] D. Condrey. "A TEE-Based Architecture for Confidential and Dependable Process Attestation in Authorship Verification." *arXiv:2603.00178*, Feb. 2026.

---

### 11. Mica：基于不可信组件构建可证明可信的工作流

**arXiv ID：** 2603.03403
**标题：** Sharing is Caring: Attestable and Trusted Workflows out of Distrustful Components
**作者：** Amir Al Sadi, Sina Abdollahi, Adrien Ghosn, Hamed Haddadi, Marios Kogias（帝国理工学院、微软研究院）
**发表：** 2026年3月（2026年3月更新至v2）

#### 摘要（约1000字）

机密计算仅保护数据在使用中的隔离，但**现有 TEE 对组件之间的安全通信缺乏实质性支持**。当流水线涉及独立开发、部署和管理的多个 TEE 时，每个组件必须信任其他组件不会泄露所交换的敏感信息——这是一个不现实的假设，也是现代云工作负载实现真正机密性的核心障碍。

现有方案（如 Ryoan、基于 paravisor 的设计）试图在 TEE 内部通过可信软件层强制执行所有通信约束，但这种方法将机密性保障寄托于 TEE 内部可信软件的功能正确性，对实际云工作负载而言是不堪重负的负担：需要所有流水线参与方标准化到相同的可信软件栈，且该软件栈的正确性实际上无法被独立审计。

Mica 的核心创新在于**将机密性与信任解耦**：将通信端点和路径显式标识、测量和证明，而非从可信软件的行为中推断。Mica 基于三大原则：
1. **从隐式共享到显式共享**：通信端点和路径被显式标识、测量和证明
2. **从固定策略到固定机制+可配置策略**：将租户定义的共享策略与实施和证明这些策略的可信机制分离
3. **从 TEE 内强制执行到结构保证**：机密性不再依赖 TEE 内部可信软件对所有交互的中介，而是来源于内存访问和组件间通信的可证明结构

Mica 在 **Arm CCA** 上实现，通过扩展 Realm Management Monitor（RMM）添加小型策略语言，控制和证明 Realms 之间以及与不可信 hypervisor 之间的共享通信通道（共享保护内存、共享非保护内存、控制转移）。所有扩展均基于现有 Arm CCA 原语，无需硬件修改。

评测表明，Mica 支持真实云处理流水线，仅带来可忽略的 TCB 增加和 TEE 启动/证明开销。

#### 关键贡献

- 首个将机密性与信任解耦的机密计算架构，使互不信任的组件之间可构建可证明机密的工作流
- 在 Arm CCA 上实现策略语言控制的通信路径显式证明机制
- 完全基于现有原语，无需硬件修改，具有良好的工程可行性

#### 引用

[Mica-2026] A. Al Sadi et al. "Sharing is Caring: Attestable and Trusted Workflows out of Distrustful Components." *arXiv:2603.03403*, Mar. 2026.

---

### 12. 基于 RISC-V TEE 的 IoT 设备外部熵源供给

**arXiv ID：** 2603.09311
**标题：** External Entropy Supply for IoT Devices Employing a RISC-V Trusted Execution Environment
**作者：** Arttu Paju, Juha Nurmi, Alejandro Cabrera Aldaya, Nicola Tuveri, Juha Savimäki（坦佩雷大学）、Marko Kivikangas、Brian McGillion（技术创新研究所 TII）
**发表：** 2026年3月（2026年3月更新至v2）

#### 摘要（约1000字）

熵（随机性）是生成安全加密密钥的必备条件。然而，资源受限的小型 IoT 设备往往难以收集足够的高质量熵——这可能导致熵耗尽攻击（entropy starvation attack），攻击者通过预测设备随机数来破解密钥和通信安全。

现有解决方案包括：内置真随机数发生器（TRNG）但增加硬件成本；环境源（如温度、光线、运动传感器读数）理论上可提供熵但易被操控；用户交互作为熵源不适用于无人值守 IoT 设备。当设备自身熵不足时，最可行的方案是从外部可靠来源获取高质量熵。

本文提出在 **RISC-V TEE（SPIRS 平台）** 上构建外部熵服务（Entropy as a Service, EaaS），核心设计：
- SPIRS（RISC-V 安全平台）集成硬件 RoT（含 PUF/TRNG、AES-256、SHA-256、数字签名）、CORE-V CVA6 处理器核心和安全监控器（SM）
- SM 以最高特权运行，管理内存和设备访问，通过 PMP（物理内存保护）实现隔离
- EaaS TA（Trusted Application）在 TEE 内运行，保证熵的生成和分发过程不被篡改

系统工作流程：IoT 设备开机后通过少量初始熵或预装密钥建立安全通信；连接后从 TEE 后端服务器请求加密强熵；通过 TPM/远程 attestation 验证熵的可靠性和新鲜性；支持扩展传感器作为额外可信熵源。

开源实现表明，在开放 RISC-V 平台上构建可信熵基础设施是可行且有效的。本文同时发布了 SPIRS TEE SDK 和 EaaS TA 的开源代码。

#### 关键贡献

- 首个在 RISC-V TEE 上实现面向 IoT 设备群的外部熵即服务（EaaS）解决方案
- 开源 SPIRS TEE SDK，支持开放源代码开发 RISC-V TEE 受信任应用
- 利用 TEE 的远程证明能力确保 IoT 设备接收到可靠且新鲜的熵

#### 引用

[ExternalEntropyIoT-2026] A. Paju et al. "External Entropy Supply for IoT Devices Employing a RISC-V Trusted Execution Environment." *arXiv:2603.09311*, Mar. 2026.

---

### 13. Keyfort：保障 IoT RISC-V TEE 软件开发生命周期安全

**arXiv ID：** 2603.17757
**标题：** On Securing the Software Development Lifecycle in IoT RISC-V Trusted Execution Environments
**作者：** Annika Wilde（波鸿鲁尔大学）、Claudio Soriente（GMV Spain）、Samira Briongos（NEC 实验室欧洲）、Ghassan Karame（波鸿鲁尔大学）
**发表：** 2026年3月

#### 摘要（约1000字）

RISC-V 作为模块化开放标准指令集架构，在汽车和 IoT 领域快速崛起：Mobileye EyeQ 芯片（超过 2 亿台车辆部署）计划 2030 年前全面转向 RISC-V；英飞凌 2025 年推出 RISC-V 汽车 MCU 新品线。这意味着未来汽车平台将大量集成 RISC-V TEE，使其成为现实需求。

然而，**当前没有任何 RISC-V TEE——乃至任何商用 TEE 设计——提供安全的端到端软件生命周期支持**，包括安全计时、状态保持的软件更新和 Enclave 迁移。这些能力对 IoT 和汽车领域至关重要：想象无法在关键漏洞披露后更新汽车软件，或无法将数据安全迁移至新车！

核心挑战在于 Enclave 状态的密封（sealing）机制：密封密钥通常与特定处理器和 Enclave 二进制绑定，使安全状态传输本质上困难重重。目前唯一的更新/迁移方法是以明文形式将代码、状态和密钥从 TEE 中提取出来，手动执行更新或迁移后再重新配置——这打开了多重攻击向量。

Keyfort 是首个填补这一空白的工具包，基于 **Keystone（最流行的开源 RISC-V TEE 框架）** 构建，同时兼容 CURE 和 ACE 等其他 RISC-V TEE 框架。Keyfort 扩展安全监控器（SM）增加三个模块：

1. **可信本地计时**：在 Enclave 内部提供安全的本地时间感知（不依赖不可信操作系统）
2. **状态连续性**：支持 Enclave 状态的安全持久化和恢复，保证跨软硬件环境的状态一致性
3. **安全软件更新与迁移**：允许 Enclave 在不暴露明文状态的前提下完成版本升级和设备间迁移

实现结果显示：TCB 仅增加约 **750 行代码**（计时 50 行、状态连续性 160 行、更新迁移 540 行）；运行时内存开销极低（每个活跃 Enclave 仅需额外 4 字节）；更新停机时间 ≤10ms，迁移停机时间 ≤0.7s（针对 16KB 状态），符合汽车 OTA 更新和 IoT 设备的实际需求。

#### 关键贡献

- 首个在 RISC-V TEE 上实现完整软件生命周期安全管理（安全更新、迁移、状态连续性、可信计时）
- 模块化设计，与 Keystone、CURE、ACE 等主流 RISC-V TEE 框架兼容
- TCB 增加极小（~750 LoC），运行时开销 <1.5%，服务停机时间实际可接受

#### 引用

[Keyfort-2026] A. Wilde et al. "On Securing the Software Development Lifecycle in IoT RISC-V Trusted Execution Environments." *arXiv:2603.17757*, Mar. 2026.

---

### 14. Space Fabric：卫星增强型可信执行架构

**arXiv ID：** 2603.23745
**标题：** Space Fabric: A Satellite-Enhanced Trusted Execution Architecture
**作者：** Filip Rezabek, Dahlia Malkhi, Amir Yahalom（SpaceComputer, UCSB）
**发表：** 2026年3月

#### 摘要（约1000字）

太空领域正在经历根本性转型：低成本小卫星和商业发射服务的普及使轨道基础设施日益可及，催生了去中心化卫星网络、轨道数据中心、AI 增强卫星等新兴范式。然而，**如何在租户或验证者无法物理接触、无法独立监控的情况下建立对轨道计算平台的信任**，成为制约发展的关键问题。

地面云端通过 TEE 解决信任问题，但直接移植地面 TEE 架构至轨道平台面临两大根本挑战：

**挑战一：物理攻击防护不足**。现有 TEE 的威胁模型假设物理访问是可能的并试图防御，但事实证明越来越站不住脚：SGX 已被大量侧信道和微架构攻击攻破；SEV/TDX 的 TCB 包含整个客户机内核，攻击面实质上以另一种方式扩大；更重要的是，所有现有 TEE 架构都无法抵御对主机拥有持续物理访问能力的攻击者。

**挑战二：预置制造商秘密的信任依赖**。当前 TEE 的 attestation 链根源在于制造过程中配置的秘密密钥——这些密钥在发射前窗口期内存在，制造商可能仍持有，验证者无法独立审计。这与去中心化卫星网络中多个运营商需要相互验证但不能依赖单一制造商 attestation 服务的需求根本矛盾。

Space Fabric 的核心洞察：**卫星发射后物理上不可访问，这一属性可作为防篡改屏障，其安全性远超任何地面部署**。Space Fabric 将整个可信计算栈（TPM、TEE、执行验证）迁移至轨道基础设施，并通过以下创新实现：

1. **卫星执行保证协议（SEAP）**：通过拜占庭容错地面站背书 quorum，将工作负载执行绑定到特定卫星——不仅证明 TEE 内执行了什么程序，还证明**在哪里**执行
2. **全轨道密钥生成**：所有签名密钥（包括卫星身份密钥和 attestation 密钥）均在发射后在共置安全元件内生成，发射前后地球上都无任何秘密存在——彻底消除预发射秘密窗口
3. **双安全元件交叉验证**：硬件信任锚分布于两个来自不同厂商的独立安全元件（NXP SE050 + TROPIC01），两者必须共同签名才能生成有效 attestation 证据——需同时攻破两家厂商的芯片才能伪造证明

在 USB Armory Mk II（ARM TrustZone + NXP SE050 + TROPIC01）上实现，通过 Veraison 进行端到端 attestation 验证。

#### 关键贡献

- 首个利用卫星物理不可访问性作为防篡改屏障的轨道计算信任架构
- 提出卫星执行保证协议（SEAP），将 TEE 证明从"执行了什么"扩展到"在哪里执行"
- 实现无预置秘密的全轨道密钥生成，配合双元件交叉验证消除单厂商依赖

#### 引用

[SpaceFabric-2026] F. Rezabek, D. Malkhi, A. Yahalom. "Space Fabric: A Satellite-Enhanced Trusted Execution Architecture." *arXiv:2603.23745*, Mar. 2026.

---

### 15. TEE 用于解决学术界的可复现性危机

**arXiv ID：** 2603.24878
**标题：** Trusted-Execution Environment for Solving the Replication Crisis in Academia
**作者：** Jiasun Li（乔治梅森大学）
**发表：** 2026年3月

#### 摘要（约1000字）

可复现性危机（replication crisis）横跨经济学、金融学、社会科学和计算机科学，严重损害学术研究的可信度。现有解决方案（如artifact评估、数据编辑审查）面临系统性瓶颈：资深数据编辑稀缺且多为志愿性质；专有数据无法与期刊共享导致豁免泛滥；编辑流程耗时且成本高昂（Management Science 已收取 $79/篇投稿费以资助可复现性基础设施）。

本文提出利用 **Intel TDX** 颠覆传统数据编辑流程的核心设计：作者在云端 TEE 中执行复现包（replication package），生成正确执行的加密证明（attestation quote），期刊或会议仅需验证该证明即可——无需重新运行代码。具体流程：论文接收后，作者在云端 TDX 虚拟机中执行复现包；TEE 生成包含执行环境哈希和代码测量值的 cryptographic proof；作者将该证明随论文投稿包一并提交；期刊通过验证 TEE attestation quote 在毫秒级确认代码正确执行。

四大优势：
1. **可靠性**：TEE 执行完全自动化，消除数据编辑过程中的人为错误和错失
2. **成本**：约 **$1.35–$1.80/package**，比 Management Science 的 $79/篇投稿费低 50 倍以上，且验证时间从数小时缩短至毫秒
3. **可验证性**：TEE attestation proof 可被任何人快速验证，而非仅编辑内部可审
4. **专有数据覆盖**：TEEs 的机密计算属性使作者可在不暴露敏感数据的前提下证明结果正确性——填补了现有系统对专有数据论文豁免后无人验证的重大空白

实地验证：招募无 TEE 经验的高中生实习生，在云端 TDX 上复现 Management Science Volume 70 期刊论文。绝大多数实习生成功复现，失败原因均为原始复现包本身缺失依赖，而非 TEE 使用困难。

附录中的形式化分析证明：作者合规在 TEE 下几乎是完全理性的（任何正制裁均可实现威慑）；期刊采用 TEE 即使承担全部每篇成本也节省 >99% 的费用；TEE 全面采用是期刊竞争格局中的稳定均衡。

#### 关键贡献

- 首个将 TEE 应用于学术可复现性危机的系统性框架，将验证成本降低 50 倍以上
- 利用 TDX 机密计算属性覆盖专有数据场景（填补现有系统空白）
- 形式化经济分析证明 TEE 替代数据编辑是作者顺从、期刊成本优势下的均衡结果

#### 引用

[TEERepCrisis-2026] J. Li. "Trusted-Execution Environment for Solving the Replication Crisis in Academia." *arXiv:2603.24878*, Mar. 2026.

---

### 16. Styx：基于 TEE 强制粘性策略的协作私密数据处理

**arXiv ID：** 2604.04082
**标题：** Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy
**作者：** Shixuan Zhao, Weicheng Wang, Ninghui Li（普渡大学）、Zhiqiang Lin（俄亥俄州立大学）
**发表：** 2026年4月

#### 摘要（约1000字）

多方数据协作（如多方联合 AI 训练）中，不存在所有参与方都信任的单一实体，各方对敏感数据的使用方式、输出内容和输出保护有各自不同的策略。如何在数据全生命周期和派生数据上强执行各方的策略，同时支持动态协作，是机密计算领域尚未解决的核心挑战。

粘性策略（sticky policy）早在二十年前就被提出，旨在通过将数据特定策略附加在数据本身上支持多样化策略表示。但现有粘性策略工作主要聚焦于访问控制，强执行方案需要针对每个新场景重新设计。

TEE 原生支持数据使用中的保护，但现有 TEE 主要为单方外包场景设计，当处理由其他实体执行或使用专有代码时——多方协作的真实场景——存在明显不足：
- 远程 attestation 仅传递哈希，各参与方需自行验证应用——在专有代码和多方场景下不可行
- 无法提供多方输入的数据使用保护
- 缺乏数据派生（derived data）保护机制

Styx 的核心创新在于**将粘性策略与 TEE 强执行深度整合**，并辅以运行时沙箱实现安全协作数据处理：

**三层关键需求满足**：
1. **数据使用保护**：I/O 管道受运行时沙箱完全控制，防止未授权泄漏（而非依赖 TEE 内部可信软件的功能正确性）
2. **数据生命周期保护**：在输入和输出两侧均设计双管道（dual pipeline），确保策略在输出侧同样被强制执行——不仅指定输出可包含什么，还指定输出应附加什么策略
3. **动态协作**：整合来自不同参与方的不同数据策略，支持对输出的联合控制和策略决策

**技术架构**：基于 Intel SGX + WebAssembly 运行时构建中间件框架，将协议和框架与具体架构解耦，支持异构处理节点上的数据处理。在 Intel SGX Enclave 内运行 WASM 沙箱，通过可插拔策略引擎支持完全可定制的策略。

评测表明：Styx 在单节点计算上性能开销合理（与 HTTPS 加密协议相当），运行时沙箱的额外开销相对于标准运行时极小，且可扩展至大规模分布式多节点部署。论文同时以多家医院联合训练癌症分类模型作为真实应用场景进行演示。

#### 关键贡献

- 首个将粘性策略与 TEE 强制执行完整整合的框架，实现数据全生命周期保护
- 提出 I/O 双管道和运行时沙箱设计，覆盖输入保护→处理保护→输出保护→派生数据保护的完整链路
- 架构无关设计（基于 Intel SGX + WASM），具有向异构分布式环境扩展的可行性

#### 引用

[Styx-2026] S. Zhao et al. "Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy." *arXiv:2604.04082*, Apr. 2026.

---

## 总结

本批次 16 篇 TEE 论文覆盖了从基础理论（经济安全模型、可信时间协议）到系统设计（抽象层、多组件工作流）再到垂直应用（卫星、IoT、汽车、学术、LLM）的完整研究光谱。

**最具影响力的技术贡献**：
- [PartialTEE-LLM-2026] 揭示了 PTSE LLM 推理范式的根本性密码学漏洞（密钥复用）
- [AutoTEE-2025] 开创了 LLM 自动化 TEE 适配的先河
- [Mica-2026] 和 [Styx-2026] 在多组件机密计算领域提出了解耦机密性与信任的重要范式转变
- [WhatYouTrust-2025] 提供了迄今为止最大规模的真实 TEE 使用实证数据

**最具创新性的应用场景**：
- [SpaceFabric-2026] 将 TEE 信任拓展至太空领域
- [TEERepCrisis-2026] 以极低成本（$1.35-1.80）将 TEE 应用于学术诚信基础设施
- [Keyfort-2026] 填补了 RISC-V TEE 软件生命周期安全的空白

**最重要的开放问题**：
1. TEE 侧信道攻击的全面防御仍是未解难题
2. 跨平台 TEE 抽象层的标准化尚未形成共识
3. LLM 作为安全顾问的可靠性和安全性需要在实际部署前得到系统性验证

---

*本 README 由自动化脚本生成，所有摘要内容基于对应论文原文提取文本编写。*
*生成器版本：TEE Paper Batch Processor | 日期：2026-04-12*
