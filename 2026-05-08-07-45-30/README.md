# TEE 论文综述 — 2026-05-08 下载批次

**会话目录**: `/tmp/tee_paper/2026-05-08-07-45-30/`
**下载时间**: 2026-05-08 07:45 (NZST)
**论文数量**: 12 篇（去重后）

本目录收录 2025-2026 年 arXiv 上与**可信执行环境（Trusted Execution Environment, TEE）**相关的最新研究，涵盖 AI 安全、区块链、隐私计算、IoT 等多个方向。

---

## 论文索引

| # | 文件名 | arXiv ID |
|---|--------|----------|
| 1 | [2026 - A TEE-based Approach for Preserving Data Secrecy in Process Mining.pdf](#1-confine) | 2602.04697 |
| 2 | [2026 - Agentic Witnessing: Pragmatic and Scalable TEE-Enabled Privacy-Preserving Auditing.pdf](#2-agentic-witnessing) | 2604.24203 |
| 3 | [2026 - Gyokuro: Source-assisted Private Membership Testing using Trusted Execution Environments.pdf](#3-gyokuro) | 2603.23226 |
| 4 | [2026 - KingsGuard: Enclave Data Protection Under Real-World TEE Vulnerabilities.pdf](#4-kingsguard) | 2605.00613 |
| 5 | [2026 - Privacy-Preserving Product-Quantized Approximate Nearest Neighbor Search via A Hybrid of FHE and TEE.pdf](#5-pppq-ann) | 2604.17816 |
| 6 | [2026 - Proteus: Append-Only Ledgers for (Mostly) Trusted Execution Environments.pdf](#6-proteus) | 2602.05346 |
| 7 | [2026 - SPOILER: TEE-Shielded DNN Partitioning of On-Device Secure Inference with Poison Learning.pdf](#7-spoiler) | 2603.06263 |
| 8 | [2026 - Space Fabric: A Satellite-Enhanced Trusted Execution Architecture.pdf](#8-space-fabric) | 2603.23745 |
| 9 | [2026 - Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy.pdf](#9-styx) | 2604.04082 |
| 10 | [2026 - T-RBFT: A Scalable and Efficient Byzantine Consensus Based on Trusted Execution Environment.pdf](#10-t-rbft) | 2604.16053 |
| 11 | [2026 - Trusted-Execution Environment for Solving the Replication Crisis in Academia.pdf](#11-tee-replication) | 2603.24878 |
| 12 | [2026 - When Agents Handle Secrets: A Survey of Confidential Computing for Agentic AI.pdf](#12-agentic-survey) | 2605.03213 |

---

## 各篇论文摘要

### 1. CONFINE: 流程挖掘中的 TEE 数据保密方法 {#1-confine}

**文件**: `2026 - A TEE-based Approach for Preserving Data Secrecy in Process Mining.pdf`
**作者**: Basile, Goretti, Barbaro, Reijers, Di Ciccio (Sapienza University 等)
**arXiv**: 2602.04697v1

**核心贡献**:  
本文提出 **CONFINE**，一种用于**跨组织流程挖掘**的保密方案。传统流程挖掘依赖中心化服务器分析多方事件日志，这会暴露各参与方的商业敏感数据。CONFINE 利用 TEE（Intel SGX/AMD SEV 等）构建可信执行环境，使多方可以在不暴露原始数据的前提下联合分析日志。

**技术方案**:
- 采用**四阶段协议**：数据加密传输 → TEE 内批量处理 → 安全聚合 → 结果返回
- 针对 TEE 内存有限的问题，设计了**基于分割的策略**（segmentation-based strategy），将大型事件日志分批送入 TEE 处理，避免 OOM
- 提供形式化验证和安全性分析，证明 TEE 核心能够保证数据不泄露

**意义**: 为敏感业务流程（如供应链、跨行金融）提供了"数据可用不可见"的分析范式，有望推动跨组织流程挖掘在合规要求严格领域的落地。

---

### 2. Agentic Witnessing: TEE 赋能隐私保护审计 {#2-agentic-witnessing}

**文件**: `2026 - Agentic Witnessing: Pragmatic and Scalable TEE-Enabled Privacy-Preserving Auditing.pdf`
**作者**: ARIA 研究团队
**arXiv**: 2604.24203v1

**核心贡献**:  
针对**可复现性危机**，提出 **Agentic Witnessing** 框架——将 LLM 审核员运行在 TEE 内，作为"代理见证人"审查私有代码/数据集。审核方（Verifier）可以通过布尔问答（Yes/No）获取关于被审核方私有数据的断言，而无需暴露原始数据。

**技术方案**:
- 引入**加密日志链**（transcript hash chain）：将审核过程中的每一步推理绑定到密码学哈希链，保证不可篡改和不可否认性
- LLM 审核员在 TEE 内使用 Chain-of-Thought 推理，生成经硬件签名的断言
- 三方架构：Verifier（审核方）、Prover（数据持有方）、Enclaved Auditor（TEE 内 LLM）

**意义**: 将隐私保护的静态验证转变为动态对抗性查询，为代码审核、数据合规、学术同行评审提供了一种无需数据出境的可行路径。

---

### 3. Gyokuro: 源辅助的 TEE 私密成员测试 {#3-gyokuro}

**文件**: `2026 - Gyokuro: Source-assisted Private Membership Testing using Trusted Execution Environments.pdf`
**作者**: Srdjan Čapkun 团队（ETH Zurich）
**arXiv**: 2603.23226v1

**核心贡献**:  
提出 **Source-assisted PMT (SPMT)** ——一种客户端利用数据源提供的辅助信息进行成员测试的协议。与传统 PIR/PSI 相比，Gyokuro 的查询不包含任何关于用户隐私的信息（零查询泄露），且通信和计算复杂度与数据库大小无关。

**技术方案**:
- 利用 TEE 生成**进度证明**（proof of progress）而非传统 presence proof：服务器证明"已处理到足够深度可以包含该数据项"，客户借此推断成员资格
- 结合监控服务（如 Certificate Transparency log）确保数据未被动过
- 性能：7ms 查询延迟，约 1400 req/sec/core 吞吐量

**应用场景**: 药品供应链审计（扫码验证药品是否在合法日志中）、证书透明度审计、文档公开审计

**意义**: 开创性地将 TEE 用于隐私成员测试，以"证明处理进度"代替"证明包含性"，避免了传统方案的查询泄露问题。

---

### 4. KingsGuard: 真实世界 TEE 漏洞下的飞地数据保护 {#4-kingsguard}

**文件**: `2026 - KingsGuard: Enclave Data Protection Under Real-World TEE Vulnerabilities.pdf`
**作者**: Firdous Allaqband 等
**arXiv**: 2605.00613v2
**会议**: CCS 2026

**核心贡献**:  
指出当前 TEE 的两大安全威胁：**（1）飞地代码漏洞**（侧信道、内存错误）和**（2）硬件设计缺陷**，均可导致敏感数据即使在强隔离下依然泄露。提出 **KINGSGUARD**，通过硬件级**动态信息流跟踪（DIFT）**实时监控飞地内敏感数据的传播。

**技术方案**:
- 在 RISC-V 处理器上实现硬件级数据流追踪：对所有飞地内的数据移动进行标记追踪
- 引入**受控去分类**（controlled declassification）机制：在边界允许受控的数据释放，平衡安全性与实用性
- 实现开销：FPGA 综合后硬件面积增加 10.8%，性能开销 5.69%

**意义**: 首次系统性地从数据流追踪角度解决 TEE 的实际漏洞问题，为未来 TEE 安全设计提供了可证明的硬件级防御框架。

---

### 5. PPPQ-ANN: FHE+TEE 混合的隐私保护近似最近邻搜索 {#5-pppq-ann}

**文件**: `2026 - Privacy-Preserving Product-Quantized Approximate Nearest Neighbor Search via A Hybrid of FHE and TEE.pdf`
**arXiv**: 2604.17816v1

**核心贡献**:  
针对 LLM/VLM 时代的**向量嵌入泄露问题**（成员推断、属性推断、嵌入反转攻击），提出 **PPPQ-ANN**：结合全同态加密（FHE）与 TEE 的多层安全最近邻搜索框架。

**技术方案**:
- 在 TEE 内执行搜索过程，数据在内存中加密存储
- 对可能泄露完整数据的查询和 codebook 使用 CKKS-based FHE 在 TEE 内加密
- 结合乘积量化（PQ）优化数据打包，最小化 FHE 密文计算量
- 性能：百万级数据集数据库生成 < 2 小时，搜索吞吐 > 50 QPS

**意义**: 在安全性和性能之间取得了迄今最优的平衡，为高机密向量数据库（医学、知识产权、LLM RAG）提供了可直接部署的方案。

---

### 6. Proteus: 面向（Mostly）TEE 的只增账本 {#6-proteus}

**文件**: `2026 - Proteus: Append-Only Ledgers for (Mostly) Trusted Execution Environments.pdf`
**作者**: Mishra, Gonçalves 等
**arXiv**: 2602.05346v1

**核心贡献**:  
分析当前分布式账本（append-only ledgers）依赖 TEE 的安全假设的问题：虽然 TEE 大幅提升安全性，但所有主流 TEE 均已被实际攻击破解（如 SGX 侧信道、TrustZone 漏洞），"信任 TEE" 存在单点故障风险。提出 **Proteus**，将 BFT 协议**巧妙嵌入** CFT 协议的结构中，无需额外消息即可在 TEE 妥协时提供完整性保证。

**技术方案**:
- 重新设计 CFT 和 BFT 协议结构，使其对齐，使 BFT 层可以在不增加额外消息的情况下激活
- TEE 正常时性能与普通 TEE 共识协议相当（高吞吐低延迟）
- TEE 被攻破时自动切换到 BFT 保护模式

**意义**: 优雅地解决了"完全信任 TEE"与"完全不用 TEE"之间的两难，为实用分布式系统设计提供了新的安全范式。

---

### 7. SPOILER: 带毒学习的 TEE 屏蔽 DNN 分割 {#7-spoiler}

**文件**: `2026 - SPOILER: TEE-Shielded DNN Partitioning of On-Device Secure Inference with Poison Learning.pdf`
**arXiv**: 2603.06263v1

**核心贡献**:  
当前 TEE 屏蔽 DNN 分割（TSDP）方案面临两难：训练后再分割存在隐私泄露，分割后再训练则因结构依赖导致高延迟。**SPOILER** 通过"搜索后训练"范式从根本上解决这一矛盾，使用硬件感知 NAS 找到轻量级 TEE 子网，再通过**自毒学习**（self-poisoning learning）强制逻辑隔离。

**技术方案**:
- 硬件感知神经架构搜索（NAS）：找到严格适配硬件约束的轻量 TEE 子网，最大化并行效率
- 自毒学习：在公开子网上注入特殊噪声，使其在缺少 TEE 组件时功能失调，从而实现"逻辑隔离"而非"物理隔离"
- 支持 CNN 和 Transformer，在安全/延迟/精度三方面均达到 SOTA

**意义**: 突破了 TEE 推理中的隐私-效率二元困境，为边缘 AI 模型保护提供了新的设计范式。

---

### 8. Space Fabric: 卫星增强的可信执行架构 {#8-space-fabric}

**文件**: `2026 - Space Fabric: A Satellite-Enhanced Trusted Execution Architecture.pdf`
**arXiv**: 2603.23745v1

**核心贡献**:  
针对**近地轨道卫星网络**（LEO satellite computing）提出新型 TEE 信任模型。现有地面 TEE 的两大缺陷：物理攻击脆弱、信任链依赖厂商预置密钥（存在预发射窗口和单厂商依赖）。**Space Fabric** 将可信计算栈移至卫星，利用发射后的物理不可访问性作为防篡改屏障。

**技术方案**:
- **卫星执行保证协议**（SEAP）：通过分布式地面站的拜占庭容错背书仲裁，对 TEE 内执行的程序进行"在哪里"的绑定认证
- **全轨道密钥生成**：加密密钥在发射后由共置的安全元件（NXP SE050 + TROPIC01 双签）生成，地球上任何时点均无持久签名密钥
- 信任锚分散到两个独立安全元件，必须联合签名才能提供证明

**意义**: 首次将 TEE 扩展到太空计算环境，为未来卫星托管计算、星际区块链提供安全基础。

---

### 9. Styx: TEE 强制粘性策略的协作私密数据处理 {#9-styx}

**文件**: `2026 - Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy.pdf`
**arXiv**: 2604.04082v1

**核心贡献**:  
解决多方协作 AI 训练中的数据保护问题：当多方数据需要联合训练时，现有方案无法同时满足"数据生命周期保护"和"灵活协作"的需求。**Styx** 将粘性策略（sticky policy）与 TEE 结合，构建软硬件协同的沙箱环境。

**技术方案**:
- 硬件 TEE 保护的中间件 + 编程语言运行时：为数据处理和策略执行同时提供保护
- 全生命周期策略执行：从数据使用、传输到派生数据的每个环节均强制执行访问策略
- 数据在用保护（data-in-use protection）+ 动态协作支持

**意义**: 为医疗联合训练、跨机构金融建模等场景提供了可证明安全的策略执行框架。

---

### 10. T-RBFT: 基于 TEE 的联盟链高效拜占庭共识 {#10-t-rbft}

**文件**: `2026 - T-RBFT: A Scalable and Efficient Byzantine Consensus Based on Trusted Execution Environment.pdf`
**arXiv**: 2604.16053v1

**核心贡献**:  
联盟链中传统 BFT 协议（如 PBFT）为最坏情况设计，消息开销过大。**T-RBFT** 利用 TEE 构建两层共识：节点先根据运行时特征动态分组，组间通过 TEE 辅助的 BFT 达成一致，组内使用改进的 Raft 协议。

**技术方案**:
- 动态分组机制：根据节点运行时特征（性能、在线时长等）动态调整委员会配置
- TEE 辅助的组间 BFT：利用 TEE 的可信性降低组间共识的协议复杂度
- 评估结果：正常操作下吞吐量提升 15%，TEE 故障回退时提升 21%

**意义**: 为高性能联盟链提供了切实可行的 TEE 加速共识方案，在安全性和性能之间取得了良好平衡。

---

### 11. TEE 用于解决学术可复现性危机 {#11-tee-replication}

**文件**: `2026 - Trusted-Execution Environment for Solving the Replication Crisis in Academia.pdf`
**arXiv**: 2603.24878v1

**核心贡献**:  
学术可复现性危机源于：缺乏合格的编辑、专有数据集难处理、流程效率低、依赖志愿者劳动。本文提出利用 **Intel TDX** 在云端 TEE 内执行复现包，生成可密码学验证的执行证明，期刊/会议无需重新运行代码即可高效验证。

**技术方案**:
- 作者在 TDX 云虚拟机内执行复现包，生成加密执行证明
- 期刊/会议通过验证证明确认代码正确性，无需访问原始数据
- 试点实验：平均成本 $1.35–$1.80/package，计算开销可忽略，新手用户高成功率

**意义**: 为科研诚信提供了技术可行的市场化解决方案，有望大幅降低学术出版的人工核查成本。

---

### 12. 代理 AI 时代的机密计算综述 {#12-agentic-survey}

**文件**: `2026 - When Agents Handle Secrets: A Survey of Confidential Computing for Agentic AI.pdf`
**arXiv**: 2605.03213v1

**核心贡献**:  
首个系统性分析 **Agentic AI**（使用 MCP/A2A 等协议规划、调用工具、维护持久记忆、委托任务的 LLM 驱动代理）与**机密计算**（CC/TEE）交叉领域的综述。指出当前 Agentic AI 的安全威胁面与独立模型推理有本质差异——代理累积敏感上下文、持有凭证、跨流水线操作，面临上下文泄露、凭证盗窃、提示注入等新威胁。

**技术方案**:
- 统一分类法：覆盖 Intel SGX、Intel TDX、AMD SEV-SNP、ARM TrustZone、ARM CCA、NVIDIA H100 CC 六种 TEE 平台
- 以代理为中心的威胁模型：映射感知→规划→记忆→行动→协作各层的九大安全目标
- 对比 CC 防御在单次调用推理与新型代理设计的有效性差异
- 提出六大开放挑战：多跳代理链的复合证明、GPU-TEE 在 LLM 规模的性能问题

**意义**: 为 Agentic AI 时代的安全架构提供了系统性参考框架，指明了机密计算在该领域的实际成熟度与关键差距。

---

## 综合对比分析

### 各论文主题分布

| 方向 | 论文 |
|------|------|
| AI/ML + TEE | #5 PPPQ-ANN, #7 SPOILER, #12 Agentic Survey |
| 隐私保护协议 | #2 Agentic Witnessing, #3 Gyokuro, #9 Styx |
| 区块链/共识 | #6 Proteus, #10 T-RBFT |
| 系统安全 | #4 KingsGuard, #1 CONFINE |
| 硬件/架构 | #8 Space Fabric |
| 应用 | #11 学术复现 |

### 关键技术趋势

**1. TEE 与 AI 的深度融合（最热方向）**

2026 年的 TEE 研究中，AI 相关议题占据最大比例。核心矛盾是：
- **模型IP保护**：LLM/DNN 部署在第三方设备时，白盒环境下的模型窃取攻击威胁巨大（#7 SPOILER）
- **向量隐私**：嵌入向量包含丰富语义信息，泄露风险突出（#5 PPPQ-ANN）
- **Agentic AI 安全**：随着 LLM 代理（MCP/A2A 协议）兴起，安全边界从模型延伸到整个协作流水线（#12 Survey）

关键创新点：从"全量在 TEE 内运行"转向**分割式 TEE**（partitioning），通过 NAS 搜索找到最小可信子网，结合密码学或噪声学习实现逻辑隔离而非物理隔离。

**2. TEE 辅助的隐私保护协议**

传统隐私计算方案（PIR、PSI、ORAM）各有权衡：TEE 方案性能好但依赖硬件安全，密码学方案安全强但开销大。2026 年新趋势是**混合方案**：
- #5 结合 FHE+TEE：TEE 内搜索、FHE 加密敏感数据
- #3 Gyokuro 用 TEE 生成"进度证明"而非 presence proof，规避查询泄露
- #2 Agentic Witnessing 将 LLM 审核员放入 TEE，提供可验证的隐私保护推理

**3. 区块链共识中的 TEE 应用**

#6 Proteus 和 #10 T-RBFT 均研究如何在 BFT/CFT 共识中利用 TEE，但侧重点不同：
- Proteus 关注 TEE 被攻破时的安全降级——通过巧妙的协议结构嵌入使 BFT 可在零额外消息下激活
- T-RBFT 利用 TEE 降低组间共识复杂度，提升性能

两者都承认"TEE 可被攻破"这一现实，但处理方式截然不同：Proteus 设计了后备机制，T-RBFT 则通过分层简化正常路径。

**4. TEE 实际安全性的再审视**

#4 KingsGuard 和 #12 Survey 均指出当前 TEE 在实际部署中的脆弱性：
- 硬件漏洞（侧信道、内存错误）
- SDK/API 使用不当（开发者误用）
- SGX/TrustZone 均已被实际攻击破解

这推动了两个方向：（1）从代码层面增加防御（KingsGuard 的 DIFT）；（2）将 TEE 视为"提升攻击难度"而非"绝对安全"的组件（Proteus 的混合设计）。

**5. 新应用场景的开拓**

- **太空计算**（#8 Space Fabric）：TEE 首次扩展到卫星平台，利用轨道物理特性解决传统地面 TEE 的信任链问题
- **学术复现**（#11）：将机密计算应用于科研诚信，开创了全新应用方向
- **跨组织流程挖掘**（#1 CONFINE）：数据可用不可见的业务流程分析

### 主要技术手段对比

| 论文 | TEE 平台 | 核心机制 | 性能开销 |
|------|---------|---------|---------|
| KingsGuard | RISC-V | 硬件 DIFT | 10.8% 面积, 5.69% 性能 |
| PPPQ-ANN | 通用 TEE | FHE+TEE 混合 | <2h DB生成, 50+QPS |
| Styx | 通用 TEE | 策略执行中间件 | 单节点可接受 |
| T-RBFT | 通用 TEE | 两层共识 | 延迟显著降低 |
| Proteus | 通用 TEE | CFT+BFT 结构对齐 | 与纯 CFT 相当 |
| SPOILER | 通用 TEE | NAS+毒学习 | SOTA 安全/延迟/精度 |
| Space Fabric | ARM TrustZone | 卫星 SEAP | 需地面站协同 |
| CONFINE | SGX/SEV | 分段处理 | 避免 OOM |

---

## 开放挑战与未来方向

1. **GPU-TEE 性能瓶颈**：大模型在 TEE 内执行时 GPU 加速受限，如何在 LLM 规模下实用化仍是难题（#12 明确指出）
2. **复合证明**：多跳 Agent 链的端到端 TEE 证明尚未成熟，各飞地之间的信任传递缺乏标准框架
3. **TEE 漏洞响应**：从漏洞发现到补丁部署之间的攻击窗口仍是实际威胁（#4 尝试但未完全解决）
4. **机密 AI 的标准化**：Agentic AI + CC 的安全目标尚未形成行业共识，评测基准缺失

---

## 下载元数据

```json
{
  "session": "2026-05-08-07-45-30",
  "download_time": "2026-05-08 07:45 NZST",
  "papers_count": 12,
  "papers": [
    {"arXiv": "2602.04697", "title": "CONFINE: TEE-based Approach for Preserving Data Secrecy in Process Mining"},
    {"arXiv": "2604.24203", "title": "Agentic Witnessing: TEE-Enabled Privacy-Preserving Auditing"},
    {"arXiv": "2603.23226", "title": "Gyokuro: Source-assisted Private Membership Testing using TEE"},
    {"arXiv": "2605.00613", "title": "KingsGuard: Enclave Data Protection Under Real-World TEE Vulnerabilities"},
    {"arXiv": "2604.17816", "title": "PPPQ-ANN: Privacy-Preserving Approximate Nearest Neighbor via FHE+TEE"},
    {"arXiv": "2602.05346", "title": "Proteus: Append-Only Ledgers for (Mostly) TEEs"},
    {"arXiv": "2603.06263", "title": "SPOILER: TEE-Shielded DNN Partitioning with Poison Learning"},
    {"arXiv": "2603.23745", "title": "Space Fabric: Satellite-Enhanced Trusted Execution Architecture"},
    {"arXiv": "2604.04082", "title": "Styx: TEE-Enforced Sticky Policy for Collaborative Data Processing"},
    {"arXiv": "2604.16053", "title": "T-RBFT: Byzantine Consensus Based on TEE for Consortium Blockchain"},
    {"arXiv": "2603.24878", "title": "TEE for Solving the Replication Crisis in Academia"},
    {"arXiv": "2605.03213", "title": "When Agents Handle Secrets: Survey of Confidential Computing for Agentic AI"}
  ]
}
```

---

*生成时间: 2026-05-08 07:50 NZST | 模型: MiniMax-M2.7*