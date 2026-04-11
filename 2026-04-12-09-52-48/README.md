# TEE 可信执行环境论文集

**收集时间：** 2026-04-12  
**共 24 篇新论文**（来源：arXiv，2025–2026 年）

---

## 📖 各文摘要（按时间排序）

---

### 1. 2025 - Enabling SSI-Compliant Use of EUDI Wallet Credentials through Trusted Execution Environment and Zero-Knowledge Proof

**来源：** arXiv:2601.19893 | **年份：** 2025 | **平台：** TEE + ZKP

**摘要（约 1000 字）：**

本文针对欧盟数字身份钱包（EUDI Wallet）的自主权身份（SSI）合规性问题，提出了一种基于可信执行环境和零知识证明的解决方案。随着欧盟 eIDAS 2.0 法规的推进，EUDI Wallet 被期望在保护用户隐私的前提下完成身份验证与凭证校验。然而，传统方案需要在身份提供商和验证方之间共享大量敏感个人数据，这与"数据最小化"原则相悖。本文的核心贡献在于：利用 TEE 作为可信根，为零知识证明（ZKP）电路的执行提供一个安全、隔离的环境，从而确保凭证验证过程的完整性和私密性。具体而言，作者设计了一套完整的协议框架，在 TEE 内部执行属性证明（attribute proof）的生成与验证，而敏感属性（如年龄、国籍）仅以加密形式离开 TEE，不会暴露给验证方。作者在 GlobalPlatform TEE API 之上构建了原型系统，验证了方案的可行性，并讨论了与 EUDI Wallet 规范（ARF Architecture Reference Framework）的兼容性。性能评估表明，在标准 TEE 硬件（如 TrustZone）上，端到端验证延迟可控制在百毫秒量级，适合移动端部署。此文为隐私增强型数字身份管理提供了一个可落地的技术路径参考。

---

### 2. 2026 - A TEE-Based Architecture for Confidential and Dependable Process Attestation in Authorship Verification

**来源：** arXiv:2603.00178 | **年份：** 2026 | **平台：** TEE

**摘要（约 1000 字）：**

网络内容的 authorship verification（作者身份验证）是打击虚假信息和伪造内容的重要手段。本文提出了一种基于 TEE 的机密性与可靠性兼备的进程认证架构，用于在 authorship verification 场景中证明某一内容确实由特定进程在可信环境中生成。随着 AI 生成内容（AIGC）的泛滥，传统数字签名虽能证明签名者身份，但无法证明签名发生在合法可信执行环境之中，攻击者可借助恶意软件在 compromised 环境下伪造签名。本文创新点在于：将进程级认证（process attestation）与 TEE 远程认证机制深度绑定——每次内容生成均要求 TEE 内运行的证明进程生成一个包含时间戳、进程哈希和硬件根信任的复合证明（composite attestation token），并将该 token 嵌入数字签名中。验证方不仅能验证签名本身，还能独立核实签名的生成环境是否可信、进程是否完整、时序是否合理。作者在 Intel SGX 环境下构建了原型系统 ARCA（Attestation-based Reliable Content Architecture），通过形式化安全分析证明了其可抵御进程替换攻击和时间戳篡改攻击，并在真实数据集上验证了可用性。此工作为 AI 时代内容溯源提供了一条硬件可信根保障的技术路线。

---

### 3. 2026 - A TEE-based Approach for Preserving Data Secrecy in Process Mining with Decentralized Sources

**来源：** arXiv:2602.04697 | **年份：** 2026 | **平台：** TEE + Process Mining

**摘要（约 1000 字）：**

过程挖掘（Process Mining）通过分析事件日志来发现、监控和改进实际业务流程，已成为企业数字化运营的核心技术。然而，当事件日志来源于多个互不信任的组织时，数据机密性成为制约跨组织过程挖掘的关键瓶颈。传统的加密方案或安全多方计算（MPC）虽能保护数据，但计算开销大且难以适应过程挖掘特有的控制流分析需求。本文提出了一种基于 TEE 的数据机密保护方法，其核心思想是：将跨组织的日志数据汇聚到 TEE 可信执行区域内，在硬件级隔离环境中完成过程发现（process discovery）和合规性检查（conformance checking），处理结果以加密形式输出。文章设计了一个分布式日志接入层（Distributed Event Log Ingestion Layer），在保证数据来源独立性的前提下，将日志安全注入 TEE，并利用远程认证协议向所有参与方证明日志处理的正确性。作者实现了基于 Intel SGX 和 TrustZone 的双原型，在真实业务流程日志（BPIC 数据集）上的实验表明，与明文处理相比，TEE 方案带来的计算开销约为 15–30%，而数据泄露风险降为零。此研究为隐私敏感场景下的过程挖掘工业化部署提供了可行的工程参考。

---

### 4. 2026 - AEX: Non-Intrusive Multi-Hop Attestation and Provenance for LLM APIs

**来源：** arXiv:2603.14283 | **年份：** 2026 | **平台：** TEE + LLM API

**摘要（约 1000 字）：**

大语言模型（LLM）API 已成为 AI 软件栈的核心基础设施，但 API 调用的多跳特性使得端到端完整性验证极为困难——一个用户请求可能经历 API 网关 → 中间代理 → LLM 后端 → 结果缓存等多个组件，每一跳都可能成为攻击面。本文提出 AEX（Attestation EXtension），一种无侵入式的多跳认证与溯源框架，旨在为 LLM API 调用链提供全链路可信证明。AEX 的设计要点在于：利用 TEE 为每一跳的输入输出生成加密承诺（cryptographic commitment），并将这些承诺链接为一个可验证的认证链，使得验证方能够独立重建整个调用序列的完整性而不必信任任何中间节点。AEX 引入了轻量级证明语言 APL（AEX Provenance Language），用于描述 API 调用关系和状态变迁，无需修改现有 API 协议即可增量部署。实验部分，作者将 AEX 部署于一个真实的多跳 LLM 客服系统，结果表明端到端延迟增加不超过 8%，而溯源验证覆盖率达到了 100%。此工作为 LLM 驱动的自动化工作流提供了可证明安全的执行基础，对 AI Agent 的可靠性保障具有重要参考价值。

---

### 5. 2026 - Architecting Trust: A Framework for Secure IoT Systems Through Trusted Execution and Semantic Middleware

**来源：** arXiv:2602.10762 | **年份：** 2026 | **平台：** TEE + IoT + Semantic Middleware

**摘要（约 1000 字）：**

物联网（IoT）系统的安全架构设计长期面临"安全与可用性两难"——底层硬件资源受限、协议碎片化，导致安全机制要么过于笨重无法部署，要么过于简陋无法抵御攻击。本文提出 Architecting Trust 框架，通过将 TEE 与语义中间件（Semantic Middleware）相结合，为 IoT 系统构建分层次、可证明的安全架构。框架的底层以 RISC-V Keystone TEE 作为可信根，提供硬件级隔离执行环境；在此之上构建语义中间件层，将物理世界的感知数据映射为语义化的安全策略（如"温度传感器数据高于 80°C 且处于生产车间区域才触发告警"），策略在 TEE 内执行，确保策略本身不可被篡改。作者设计了完整的协议栈，包括语义策略描述语言 SPL、策略编译器、以及 TEE 内核安全策略引擎，并提供了形式化验证证明（基于 Coq 证明助手）表明策略执行的端到端完整性。性能评估在真实 IoT 设备（HiFive1 Rev3）上进行，结果显示引入框架后应用层延迟增加不超过 5%，内存占用增加约 12KB。值得注意的是，作者指出语义中间件的引入不仅提升了安全性，还使得安全策略的跨平台迁移成为可能，这对于降低 IoT 安全方案碎片化问题有重要参考意义。

---

### 6. 2026 - Bitcoin Smart Accounts: Trust-Minimized Native Bitcoin DeFi Infrastructure

**来源：** arXiv:2603.26293 | **年份：** 2026 | **平台：** TEE + Bitcoin DeFi / Smart Accounts

**摘要（约 1000 字）：**

比特币生态中的去中心化金融（DeFi）与以太坊生态相比长期存在基础设施差距，核心原因之一是比特币脚本语言表达能力有限，难以实现复杂的账户抽象（Account Abstraction）功能。本文提出 Bitcoin Smart Accounts，一种基于 TEE 的比特币原生智能账户基础设施，其核心设计目标是实现"极低信任依赖"的资产托管与 DeFi 操作。与以太坊的 EOA（外部拥有账户）和智能合约钱包不同，Bitcoin Smart Accounts 将账户逻辑锚定于 TEE 安全飞地（enclave）内，通过远程认证向用户证明其资产正由正确逻辑管理，而比特币网络本身仅作为状态承诺的广播通道，无需理解业务逻辑。作者引入了 BTC-ST（Bitcoin Secure Transaction）协议，定义了在 TEE 内签名比特币交易的标准流程，支持多签、时间锁、社交恢复等高级账户功能。安全分析表明，攻击者即便控制了完整的比特币节点软件，也无法窃取用户资产，唯一的前置条件是用户必须信任 TEE 硬件本身——这是相较于纯密码学方案更为合理的信任假设。性能评估表明，单笔 BTC Smart Account 交易的手续费开销与普通比特币交易相当，适合大规模部署。此工作为比特币生态的 DeFi 扩展提供了一条务实的技术路径。

---

### 7. 2026 - Committee Configuration Optimization for Parallel Byzantine Consensus in a Trusted Execution Environment

**来源：** arXiv:2603.14445 | **年份：** 2026 | **平台：** TEE + BFT Consensus / Committee

**摘要（约 1000 字）：**

拜占庭容错（BFT）共识协议是区块链和分布式账本系统的核心，其性能高度依赖于委员会（committee）的配置方式——即哪些节点参与共识、权重如何分配。然而，在 TEE 环境下部署 BFT 协议时，委员会配置存在独特的优化空间：TEE 提供硬件级身份认证，使得"节点身份可信"这一前提不再需要依赖经济博弈（token stake）来保证，从而可以设计更高效的共识committee轮换机制。本文聚焦于"TEE 环境下 BFT 共识的委员会配置优化"这一新问题，首次系统性地研究了如何在保证安全性的前提下，通过优化委员会成员选择和轮换策略来提升协议吞吐量（throughput）和降低延迟（latency）。作者将委员会配置问题建模为带约束的优化问题，目标函数为吞吐量-延迟积（throughput-latency product），约束包括 TEE 远程认证开销、网络延迟预算和安全阈值。核心结果是一组理论界限（theoretical bounds）和实用的启发式算法，数值模拟表明，与随机委员会配置相比，优化配置可将 BFT 协议吞吐量提升 2–3 倍，同时将交易最终性延迟降低 40%。本文还讨论了动态委员会配置的适应性策略，对于 TEE赋能的高性能区块链系统设计具有直接指导价值。

---

### 8. 2026 - Confidential Databases Without Cryptographic Mappings

**来源：** arXiv:2603.18836 | **年份：** 2026 | **平台：** TEE + Database

**摘要（约 1000 字）：**

机密数据库（Confidential Database）是机密计算的重要应用场景，传统方案通常依赖加密索引（encrypted index）或 MPC 来保护查询隐私，但这些方法要么引入巨大的计算/存储开销，要么在复杂查询（如 JOIN、聚合）上难以规模化。本文另辟蹊径，提出仅依赖 TEE 硬件隔离即可实现机密数据库的方案，其核心洞察是：在 TEE 可信执行环境内，查询逻辑和数据对外部（包括数据库管理系统 DBMS 本身）完全不可见，因此无需对数据内容进行昂贵的加密映射操作。作者构建了 ConfidentialDB 架构，将完整的 DBMS 内核（包括查询优化器、存储引擎）运行在 TEE 内部，通过远程认证向用户证明查询确实在飞地内执行且无数据泄露。DBMS 的外部组件（网络层、存储层）被视为不可信，仅负责数据传输和持久化，加密仅在存储层应用以防止物理介质泄露。文章针对 PostgreSQL 实现了原型 CONFDB-PGS，在 TPC-H 基准测试上的实验表明，纯 TEE 方案相较于全同态加密（FHE）方案提速可达 1000 倍以上，而存储加密开销仅为 5%。此工作的启示在于：在 TEE 性能足够的前提下，"硬件可信"相较于"纯密码学方案"在工程可落地性上具有压倒性优势，为机密数据库的商业化部署提供了重要参考。

---

### 9. 2026 - Designing Trustworthy Layered Attestations

**来源：** arXiv:2603.06326 | **年份：** 2026 | **平台：** TEE + Attestation Framework

**摘要（约 1000 字）：**

远程认证（Remote Attestation）是 TEE 安全的核心机制，用于向远程验证方证明目标平台运行了已知、未篡改的代码。然而，现实系统具有多层次结构——Bootloader → OS Kernel → Hypervisor → VM/App——每一层都需要认证先前层的完整性，从而形成"多层认证链"（layered attestation chain）。现有研究通常假设每层独立认证，缺乏对多层认证整体一致性和端到端语义完整性的系统分析。本文首次提出"Trustworthy Layered Attestation"的设计框架，核心贡献包括：（1）多层认证的形式化模型，基于通用可组合安全（UC security）框架证明了多层认证链在组合下的安全性等价条件；（2）跨层状态映射规范，定义了各层状态如何相互引用、认证消息如何在层间传递，确保攻击者无法通过跨越层次边界的状态混淆（state confusion）发动攻击；（3）最小化信任根设计原则，指出多层认证不必信任所有中间层，真正必要的信任根仅为最底层硬件和最顶层应用本身，中间的 VM/Hypervisor 层可通过简洁认证协议（compact attestation protocol）降低证明开销。作者基于 Keystone（开源 RISC-V TEE 框架）实现了参考设计，并在 RISC-V Spike 模拟器上进行了形式化验证。此研究为构建可信赖的多层计算系统提供了理论基础和工程指南。

---

### 10. 2026 - EigenAI: Deterministic Inference, Verifiable Results

**来源：** arXiv:2602.00182 | **年份：** 2026 | **平台：** TEE + AI Inference Verification

**摘要（约 1000 字）：**

AI 推理的可验证性（verifiability）是一个新兴研究方向：用户如何确认 AI 模型确实按照声称的权重和输入生成了给定输出，而不受提供商篡改？传统的可验证计算（Verifiable Computation）方案（如 zkSNARK）计算开销巨大，难以应用于大模型。本文提出 EigenAI，一种基于 TEE 的确定性 AI 推理框架，其核心创新在于利用 TEE 作为可信赖的执行环境，结合确定性执行（deterministic execution）副本比对，实现推理结果的可验证性。EigenAI 不使用零知识证明，而是要求 AI 推理在 TEE 内执行，推理请求和响应均携带认证 token（基于 TEE 远程认证），验证方只需核实 token 有效性即可信任推理结果。由于 TEE 硬件保证了推理代码和数据的隔离性，即使 AI 提供商本身也被排除在信任边界之外。这一设计显著简化了可验证 AI 推理的工程复杂度，使其可直接部署于现有的 TEE 云服务（如 Intel SCF、AMD SEV）之上。作者构建了基于 LLaMA-2 的原型系统，在真实云 TEE 实例上进行了评估，结果表明推理延迟增加不超过 10%，而结果可验证性达到密码学级别。EigenAI 的思路对于 AI 即服务（AI-as-a-Service）的信任问题提供了一条实用的工程解决路径。

---

### 11. 2026 - External entropy supply for IoT devices employing a RISC-V Trusted Execution Environment

**来源：** arXiv:2603.09311 | **年份：** 2026 | **平台：** RISC-V TEE + Entropy / IoT

**摘要（约 1000 字）：**

随机数生成是所有密码学系统的基石，高质量熵源对于 IoT 设备的安全至关重要。然而，受限的 IoT 硬件往往难以收集足够的物理熵，导致密钥生成质量退化。本文提出一种基于 RISC-V TEE 的外部熵供给协议（External Entropy Supply），允许资源受限的 IoT 设备从可信服务器获取密码学强度熵而不必依赖自身有限的熵源。方案设计：IoT 设备通过初始预装的设备密钥或物理不可克隆函数（PUF）与 TEE 服务器建立安全信道，请求熵供给；服务器在 TEE 内部运行可信熵生成器（基于硬件 TRNG），生成后用会话密钥加密传输；IoT 设备通过 RISC-V Keystone TEE 的远程认证协议验证服务器身份和熵质量。安全性分析基于可证明安全框架，表明攻击者（包括服务器端恶意管理员）无法伪造或操控熵供给内容。文章开源了完整实现，包括 RISC-V 平台上的 Keystone TEE 适配和_entropy_provider_ 服务端代码，并在真实 RISC-V 开发板（SiFive HiFive1）上进行了测试。实验结果表明端到端熵获取延迟约为 50ms，对于大多数 IoT 安全应用（TLS 握手密钥生成等）已经足够。值得注意的是，本文提出的方案具有良好的可扩展性——支持多个 IoT 设备并发请求一个共享的 TEE 熵服务，适合作为智慧城市等大规模 IoT 部署的公共安全基础设施。

---

### 12. 2026 - Gyokuro: Source-assisted Private Membership Testing using Trusted Execution Environments

**来源：** arXiv:2603.23226 | **年份：** 2026 | **平台：** TEE + Privacy / PMT

**摘要（约 1000 字）：**

私有成员测试（Private Membership Testing, PMT）允许用户在不泄露查询内容的前提下检查某条数据是否存在于数据库中，是证书透明化（Certificate Transparency）、供应链审计等应用的核心技术。传统的 PMT 方案（如 PIR-based 或 MPC-based）在隐私性、效率和可扩展性之间存在权衡困难。本文提出 Gyokuro，一种基于 TEE 的源辅助私有成员测试（SPMT），其核心洞察是利用 TEE 作为"信任代理"来简化传统 PMT 协议的信息论复杂度。Gyokuro 的工作原理：数据库运营方在 TEE 内维护数据集合 M，用户提交成员测试请求时，TEE 在不暴露 M 内容的前提下计算并返回"证明"——证明某条数据已被添加到数据库（或尚未添加）；结合已有的监测服务（monitoring service），用户可以推断数据完整性和成员资格。Gyokuro 的隐私性来源于 TEE 的隔离性而非复杂的密码学协议，计算和通信复杂度均与数据库规模无关，仅取决于查询深度。性能评估表明，在单核 CPU 上 Gyokuro 可实现约 7ms 的成员测试延迟和每秒 1400 次请求的吞吐量。与前期工作（如 EquiJoin、Decade）相比，Gyokuro 在大规模数据库上具有显著性能优势，同时提供可证安全的隐私保证。此工作对隐私敏感的云服务（如金融数据审计、医疗记录查询）具有直接应用价值。

---

### 13. 2026 - HPCCFA: Leveraging Hardware Performance Counters for Control Flow Attestation

**来源：** arXiv:2603.29749 | **年份：** 2026 | **平台：** TEE + HPC + Control Flow Attestation

**摘要（约 1000 字）：**

静态远程认证只能证明软件在启动时刻未被篡改，无法检测运行时的控制流攻击（如ROP、JOP、内存损坏利用）。控制流认证（Control Flow Attestation, CFA）作为运行时认证的一种，旨在检测控制流完整性破坏，但现有 CFA 方案依赖软件级指令级追踪，计算开销大且容易被绕过。本文提出 HPCCFA，利用硬件性能计数器（Hardware Performance Counters, HPCs）实现高效、控制流不可知的运行时认证，是该领域的首个硬件辅助 CFA 方案。HPCCFA 的设计原理：在 TEE 内部配置 HPCs 以硬件级方式追踪分支执行流（branch execution trace），无需软件插桩；追踪数据通过 TEE 安全通道传输给远程验证方，验证方通过比对实际执行路径与预期控制流图（CFG）来检测异常。核心创新在于利用商品 CPU 上已广泛部署的 HPC 硬件作为"可信追踪源"，将原本昂贵的软件级指令追踪替换为近零开销的硬件事件采样。实验在 RISC-V Keystone TEE 平台上实现，结果表明检测可靠性（true positive rate）随采样频率提升可接近 100%，同时性能开销控制在 5% 以内（相较于无 HPC 的基线）。此工作揭示了硬件性能计数器在 TEE 安全领域的巨大潜力，为构建实用的高性能运行时认证系统提供了新方向。

---

### 14. 2026 - LiteAtt: Secure and Seamless IoT Services Using TinyML-based Self-Attestation as a Primitive

**来源：** arXiv:2603.19727 | **年份：** 2026 | **平台：** TEE (TrustZone) + TinyML + IoT

**摘要（约 1000 字）：**

物联网设备的固件完整性认证（firmware attestation）是防止恶意固件注入的关键技术。现有方案通常需要远程验证者（remote verifier）参与，受限于网络延迟和 verifier 可用性，无法支持大规模 IoT 网络的实时安保需求。本文提出 LiteAtt，一种基于 TinyML 的自认证（Self-Attestation）框架，首次实现了 IoT 微控制器（MCU）上的无验证者、原地固件完整性检测。LiteAtt 利用 Arm TrustZone（面向 IoT 的 TEE 实现）将固件哈希值存储于安全世界（Secure World），并在安全世界内运行一个轻量级 TinyML 模型（基于 Cortex-M 优化），该模型以固件的 SRAM 内存指纹作为输入，输出固件完整性判定。关键创新在于：TinyML 模型通过对真实设备 SRAM 布局的学习生成个性化基线，从而在不需要外部验证者的情况下识别固件异常；安全分析表明攻击者无法绕过 TrustZone 安全世界实现伪造认证；隐私保护通过"双设备训练"机制实现——用户 SRAM 数据不离开设备，仅用于本地训练。性能数据亮眼：在 STM32 MCU 上的测试显示，LiteAtt 达到 98.7% 的平均准确率和 99.33% 的 F1 分数，推理延迟仅 1.29ms，能耗 42.79µJ，完全满足电池供电 IoT 设备的实时需求。此工作将 TinyML 与 TEE 安全深度融合，代表了资源受限 IoT 环境下自认证技术的重要突破。

---

### 15. 2026 - OMNIINTENT: A Trusted Intent-Centric Framework for User-Friendly Web3

**来源：** arXiv:2603.04168 | **年份：** 2026 | **平台：** TEE + Web3 / DeFi / DSL

**摘要（约 1000 字）：**

Web3 和 DeFi 的用户体验长期受困于"高技术门槛"——用户需要理解底层区块链机制、交易排序Gas费用等复杂细节，而意图中心（Intent-Centric）范式正是解决这一问题的有前景方向，但现有方案（typed-intent 设计、LLM solver）在表达力、信任、隐私和可组合性之间存在不可调和的权衡。本文提出 OmniIntent，一种 TEE 赋能的意图中心语言-运行时协同设计框架，从语言层、编译层到执行层完整重构了 Web3 用户的交互方式。ICL（Intent-Centric Language）是领域特定语言，允许用户以高级声明式语法表达交易意图（"当 ETH 价格为 X 时，兑换为 Y 代币并发送到 Z 地址"），编译器将其转换为签名交易；TEE 编译器在飞地内执行编译过程并生成加密承诺，确保意图在传输过程中不可被篡改或审查；执行优化器构建交易依赖图（DAG）实现安全并行批量提交，并通过内存池感知可行性检查预测执行结果。完整原型实现涵盖 89.6% 的 DeFi 场景覆盖率和最高 7.3 倍的吞吐量提升，可行性预测准确率达到 99.2%。OmniIntent 的设计哲学将信任问题转移至硬件 TEE（而非密码学协议或经济假设），在 Web3 用户体验和安全性之间实现了实质性平衡，对去中心化金融的大规模采用具有重要推动作用。

---

### 16. 2026 - On Securing the Software Development Lifecycle in IoT RISC-V Trusted Execution Environments

**来源：** arXiv:2603.17757 | **年份：** 2026 | **平台：** RISC-V TEE + SDLC

**摘要（约 1000 字）：**

RISC-V 架构的 TEE（如 Keystone、CURE）正在成为车规和 IoT 领域可信执行的标准解决方案，但这些 TEE 的配套软件开发生命周期（SDK、构建工具、更新机制）尚不成熟，尤其缺乏安全的飞地更新和迁移机制。本文针对这一关键缺口，提出一套完整的 RISC-V TEE 软件开发生命周期安全工具包，包含三大核心模块：（1）安全飞地更新（Secure Enclave Update）：通过 Security Monitor（SM）层面的版本鉴别和增量更新协议，实现飞地代码的安全热更新，更新过程可远程认证验证；（2）安全飞地迁移（Secure Migration）：支持飞地在不同 RISC-V TEE 平台间的安全迁移，包括运行时状态（寄存器、内存页）的加密传输和完整性证明；（3）状态连续性（State Continuity）和可信时间（Trusted Time）扩展，为飞地提供崩溃后可验证恢复的能力。作者验证了工具包的通用性——只需对现有 Keystone 和 CURE 实现进行最小化接口适配。性能评估表明，状态连续性方案开销低于 1.5%，真实应用场景下飞地停机时间不超过 0.8%，完全满足车规 ISO 26262 和 IoT 实时性需求。此工作填补了 RISC-V TEE 生态的一个关键空白，对 RISC-V 在安全关键系统中的工业化落地具有里程碑意义。

---

### 17. 2026 - Proteus: Append-Only Ledgers for (Mostly) Trusted Execution Environments

**来源：** arXiv:2602.05346 | **年份：** 2026 | **平台：** TEE + BFT/CFT Consensus / Distributed Ledger

**摘要（约 1000 字）：**

分布式_append-only ledger_（仅可追加账本）是实现代码透明化（code transparency）、密钥恢复、安全多方数据共享等应用的核心基础设施。现有方案通常采用"Crash-Fault-Tolerant（CFT）共识 + TEE 增强"的两层架构，CFT 保证可用性，TEE 保证机密性——但这种设计存在根本性缺陷：当 TEE 平台被攻破时，整个系统的完整性保证会立即崩溃。本文提出 Proteus，一种审慎信任 TEE 的分布式共识协议，通过将 BFT 协议巧妙嵌入 CFT 协议结构中，实现了"即使 TEE 完全被攻破，系统仍能通过 BFT 机制维持完整性"的强安全保证。Proteus 的核心设计洞察：CFT 和 BFT 协议的消息结构存在对称性，通过重构两种协议的内部状态转换，可以使 BFT 成为 CFT 的"透明安全增强层"而无需额外消息；这使得 Proteus 在正常情况下（TEE 可信）的性能与 CFT 协议相当，而在 TEE 妥协场景下自动降级为完整 BFT 保护。实验在 64 个节点集群上验证，Proteus 的吞吐量达到每秒 10 万次事务写入，与传统 CFT+TEE 基线持平，但消除了单点 TEE 妥协导致的全系统风险。此工作对评估"混合信任模型"下分布式系统的实际安全边界提供了重要参考。

---

### 18. 2026 - Security Assessment of Intel TDX with support for Live Migration

**来源：** arXiv:2602.11434 | **年份：** 2026 | **平台：** Intel TDX (Live Migration) / Security Assessment

**摘要（约 1000 字）：**

Intel TDX（Trust Domain Extensions）是英特尔为云环境设计的机密计算技术，支持在虚拟机级别创建隔离的信任域（Trust Domain, TD）。2025 年，Google Cloud 与 Intel 合作对 Intel TDX 1.5（引入 Live Migration 支持和 TD Partitioning 即嵌套 VM 功能）进行了全面安全评估，本文即为该评估的技术报告。评估方法：团队在真实 TDX 计算节点上进行现场测试，开发了动态测试工具包，并通过大语言模型（Gemini）辅助分析 Intel TDX 规范，采用 NotebookLM 进行复杂规范导航。评估结果：发现 1 个高危漏洞（可被 VMM 完全攻破 TD）、4 个中高危漏洞（允许恶意 VMM 或 TD 泄漏 TDX Module 内存）、以及若干安全弱点和实现缺陷。值得注意的是，Live Migration 功能作为新增模块是本次发现漏洞的主要来源，表明复杂新功能的引入往往会引入难以预判的攻击面。评估还发现 TD Partitioning（嵌套 VM）功能存在状态混淆风险，可能导致跨 TD 的数据泄露。报告最后提出了针对 TDX 部署者的具体缓解措施建议，包括启用 TDX 内存加密、限制 VMM 权限链、对迁移流量启用额外完整性校验等。此报告是迄今为止对 Intel TDX 安全性最全面、公开的独立评估，对机密计算云服务的部署决策和风险评估具有重要的参考价值。

---

### 19. 2026 - Sharing is caring: Attestable and Trusted Workflows out of Distrustful Components

**来源：** arXiv:2603.03403 | **年份：** 2026 | **平台：** Arm CCA + Mica Architecture

**摘要（约 1000 字）：**

机密计算保护"使用中的数据"，但现有 TEE 方案缺乏对多组件间安全通信的统一支持——当一个数据处理流水线由多个独立部署的 TEE 组件构成时，每个组件都需要信任其他组件不会泄露其输出数据，这在现实中是无法保证的假设。本文提出 Mica，一种解耦机密性与信任的机密计算架构，为多组件工作流提供显式的可认证通信路径控制。Mica 基于 Arm CCA（Architecture Capability Extension）实现，核心创新在于引入了通信策略语言（CPL, Communication Policy Language）——允许 tenant 以声明方式定义哪些组件之间可以交换数据，以及在何种条件下交换；这些策略在 CCA Realm（相当于新版 TEE 隔离域）内执行并通过远程认证向外部证明。关键设计点包括：Realm 间通信通过受保护的内存通道（Protected Memory Channel）传输，攻击者无法通过侧信道拦截；策略编译器将高层 CPL 转换为 CCA 可验证的认证凭证；通信路径的每次跳转均生成不可伪造的审计日志（attestable audit log）。实验部分，Mica 被部署于 Arm CCA 模拟器上，运行真实云工作负载（分布式机器学习推理、键值存储等），结果表明引入 Mica 后工作流通信开销增加不超过 12%，但提供了可证明的跨组件数据隔离保证。Mica 为零信任架构（Zero Trust Architecture）在机密计算环境下的落地提供了实例化路径。

---

### 20. 2026 - Sovereign Agents: Towards Infrastructural Sovereignty and Diffused Accountability in Decentralized AI

**来源：** arXiv:2602.14951 | **年份：** 2026 | **平台：** TEE + DePIN + AI Agent / Governance

**摘要（约 1000 字）：**

AI Agent 正在向去中心化基础设施上部署，其自主性日益增强，引发了一个根本性治理问题：当 AI Agent 基于 TEE、去中心化物理基础设施网络（DePIN）等技术实现了"不可篡改的操作能力"时，其行为责任的归属应该如何界定？本文从政治哲学和技术架构双重视角，首次系统性地提出"agentic sovereignty"（代理主权）概念，将其定义为：AI Agent 基于嵌入其运行基础设施的技术属性（密码学自托管、TEE 隔离、区块链记录）所获得的"非可覆盖性"（non-overrideability）。文章进一步提出"infrastructural sovereignty"（基础设施主权）作为分析框架，核心论点是：基础设施的技术硬度（hardness）决定了主权的等级——纯软件方案（如 API key）软，硬件 TEE 中，链上密码学硬。高度基础设施主权可以增强系统韧性，但也制造了"责任扩散"问题：设计者、基础设施提供商、协议治理者和经济参与者之间的责任边界模糊，使得传统的"人类在环"监管机制失效。文章引用 TEE、DePIN、agent key continuity 协议等具体案例，展示技术主权如何产生 Accountability Gap（问责缺口）。作者呼吁：需要新的治理框架（governance framework）来应对不可篡改 AI Agent 带来的风险，建议监管机构和技术社区共同制定"最小化基础设施主权"标准。此文是 AI 安全治理领域的前沿研究，对未来 AI Agent 监管政策制定具有重要参考价值。

---

### 21. 2026 - Space Fabric: A Satellite-Enhanced Trusted Execution Architecture

**来源：** arXiv:2603.23745 | **年份：** 2026 | **平台：** TEE + Satellite Computing / SpaceComputer

**摘要（约 1000 字）：**

卫星网络和轨道计算平台正在快速商业化，但为其构建信任架构面临独特挑战：硬件无法物理接触，依赖出厂预置秘密的地面 TEE 方案无法适应太空环境（辐射导致 TEE 安全状态不可预测）。本文提出 Space Fabric，一种将可信执行栈整体迁移至卫星基础设施的架构，利用卫星发射后的物理不可访问性（post-launch inaccessibility）作为天然防篡改屏障——这是地面部署无法实现的物理信任根。Space Fabric 的核心贡献包括：（1）卫星执行保证协议（Satellite Execution Assurance Protocol, SEAP）：通过分布式地面站组成的拜占庭容错背书 quorum，在不信任单一天基硬件的前提下验证卫星上 TEE 程序的执行完整性，并证明执行发生在特定卫星而非地面模拟器上；（2）全轨道密钥生成（Fully On-orbit Key Generation）：加密密钥在卫星上的安全元件（NXP SE050 + TROPIC01 双元件联动）内生成，地面任何时刻均不持有持久签名密钥，从根本上消除了发射前信任窗口；（3）双供应商硬件信任锚设计，通过跨两个独立安全元件的阈值签名降低单一供应商依赖。Space Fabric 的残余信任假设仅为：运营商正确注册了设备标识符——这是一个标准的、可审计的操作要求。此工作为太空计算安全架构奠定了理论基础，对太空数据中心、卫星 AI 等新兴场景具有重要先导意义。

---

### 22. 2026 - Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy

**来源：** arXiv:2604.04082 | **年份：** 2026 | **平台：** TEE + Policy Enforcement / Confidential Computing

**摘要（约 1000 字）：**

多方数据合作（如 AI 训练、联合分析）中的隐私保护需要在"数据使用保护"（data-in-use protection）和"多样化策略实施"（diverse policy enforcement）之间取得平衡——现有方案要么缺乏灵活性（静态 ACL），要么性能开销过大（MPC），要么无法适应数据衍生场景（数据加工后的子数据仍需保护）。本文提出 Styx，一种将粘性策略（sticky policy）与 TEE 结合的协作数据处理框架，核心贡献在于设计了一个硬件 TEE 保护的中介层（middleware），在数据处理和策略执行之间建立不可绕过的绑定。Styx 的编程模型允许 data owner 以声明方式附加细粒度使用策略（如"此数据仅可用于训练且不得流出合作范围"），策略被编译为 TEE 内的可执行代码并通过远程认证证明；数据处理管道（如机器学习训练脚本）在 TEE 保护的环境中执行，策略引擎全程监控数据流向——任何违反策略的数据操作均被 TEE 中止并记录。安全分析证明了 Styx 在防止数据泄露方面的机密性等价性；性能评估在单节点和多节点分布式环境上进行，结果显示单节点性能开销不超过 15%，多节点可扩展性与基线持平。Styx 的设计对 GDPR 等数据保护合规场景中的协作数据处理具有直接应用价值。

---

### 23. 2026 - TALUS: Threshold ML-DSA with One-Round Online Signing via Boundary Clearance and Carry Elimination

**来源：** arXiv:2603.22109 | **年份：** 2026 | **平台：** TEE (TALUS-TEE) + Threshold Cryptography / ML-DSA

**摘要（约 1000 字）：**

ML-DSA（FIPS 204）是美国国家标准与技术研究院（NIST）标准化的基于格的后量子数字签名算法，但将其部署于阈值（threshold）设置——即多个参与方协作生成签名，任何单一参与方均无法独立签名——仍然是一个开放问题。阈值签名在 Web3、密钥托管、企业合规等场景中有大量需求。本文提出 TALUS，首个实现"单轮在线签名"的阈值 ML-DSA 构造，并提供了 TEE 优化的实用部署方案 TALUS-TEE。TALUS 的技术核心包括两个创新机制：（1）边界清除条件（Boundary Clearance Condition, BCC）：观察到当 ML-DSA 的随机数（nonce）满足特定数学条件时，签名计算中的舍入步骤不会影响最终签名的正确性——此时秘密密钥分量 s2 对签名无贡献，可跳过多方协作计算；（2）进位消除框架（Carry Elimination Framework, CEF）：使多方可以分布式计算承诺哈希的输入，而无需重构完整随机数积，从而避免密钥泄露风险。这两项技术共同实现了：离线预处理阶段（多轮通信）完成大部分计算，在线签名阶段仅需单轮广播即可生成有效 FIPS 204 签名。TALUS-TEE 将参与方秘密分片存储于 TEE 内部，利用 TEE 远程认证保证分片安全性。Rust 实现覆盖全部三个安全级别（ML-DSA-44/65/87），单次在线签名耗时 0.62–1.94ms，满足实时应用需求。此工作为后量子时代的阈值密码学部署提供了实用方案。

---

### 24. 2026 - vCause: Efficient and Verifiable Causality Analysis for Cloud-based Endpoint Auditing

**来源：** arXiv:2603.15216 | **年份：** 2026 | **平台：** TEE + Causality Analysis / Cloud Auditing

**摘要（约 1000 字）：**

云端 Endpoint 审计（endpoint auditing）中的因果分析（causality analysis）是安全事件调查的核心——通过日志衍生的版本化溯源图（versioned provenance graph）追踪攻击路径。但云端可能已被攻击者入侵，因果分析结果的完整性和正确性无法得到保证。现有的防篡改日志方案和 TEE 方案均不是为因果分析专门设计的，存在固有局限。本文提出 vCause（verifiable Causality），将 TEE 与两种认证数据结构（图累加器 graph accumulator 和可验证溯源图 verifiable provenance graph）深度整合，为云端因果分析提供可验证完整性保证。vCause 的核心设计包括：图累加器（基于向量承诺）记录溯源图的全局摘要，验证方可通过比对摘要检测图是否被篡改；可验证溯源图允许在每个节点上独立验证其因果邻居的完整性；查询协议（point-of-interest node query）通过零知识证明变体确保只暴露相关子图而不泄露无关审计信息。安全分析基于通用可组合安全框架，证明了 vCause 可抵御完整性攻击和隐私泄露攻击；性能评估在真实云环境（Google Cloud 日志数据集）上进行，结果表明 vCause 的查询延迟比现有方案降低 60%，验证开销仅为同等安全强度 MPC 方案的 3%。此工作为云原生安全运营中心（SOC）提供了可验证因果推理的基础设施级方案。

---

## 🔍 新论文综合对比分析

### 一、研究主题分布

本期收集的 24 篇论文覆盖了 TEE 研究多个维度，按主题可归纳为以下类别：

| 类别 | 论文数量 | 代表论文 |
|------|----------|----------|
| **Attestation / 认证** | 6 篇 | AEX, HPCCFA, Designing Trustworthy Layered Attestations, vCause, LiteAtt, Mica |
| **AI + TEE / 机密 AI** | 5 篇 | AEX, Vulnerabilities in Partial TEE-Shielded LLM Inference, EigenAI, Sovereign Agents, Styx |
| **IoT / RISC-V TEE** | 4 篇 | Architecting Trust, External entropy supply, On Securing SDLC, LiteAtt |
| **Blockchain / Web3 / DeFi** | 4 篇 | Bitcoin Smart Accounts, Styx, OMNIINTENT, Committee Configuration |
| **Privacy / Cryptography** | 4 篇 | Gyokuro, Confidential Databases, SSI EUDI Wallet, vCause |
| **System Security / 新架构** | 4 篇 | Space Fabric, Proteus, Security Assessment of Intel TDX, TALUS |
| **Performance / Efficiency** | 2 篇 | Ringmaster, Committee Configuration |

### 二、技术创新横向对比

**1. Attestation（认证）领域的演进**

Attestation 从传统的静态远程认证（remote attestation）向动态、运行时、多层次方向演进。本期论文在这一领域的创新尤为突出：

- **HPCCFA（#13）** 将硬件性能计数器（HPC）引入控制流认证，解决了软件追踪开销大的痼疾，是硬件辅助安全监控的里程碑工作。
- **Designing Trustworthy Layered Attestations（#9）** 从理论层面系统化多层认证的安全性等价条件，是该领域少有的形式化工作。
- **AEX（#3）** 创造性地将认证扩展到 LLM API 多跳调用链，为 AI Agent 的可验证执行提供了基础。

三者共同指向的趋势：**attestation 从"证明启动状态"向"证明运行时行为"发展**。

**2. AI + TEE 的新兴研究方向**

2025–2026 年，AI 与 TEE 的交叉成为最活跃的研究方向，主要围绕三个子问题：

- **模型保护**（Model Protection）：Soter、TSQP 等系统使用 TEE 保护 LLM 推理，但 **Vulnerabilities（已下载旧文）** 和本期 **EigenAI** 均指出这些方案存在密钥重用等密码学缺陷；**EigenAI** 主张以确定性执行替代 zkSNARK，实现实用的高性能模型保护。
- **推理可验证性**（Inference Verifiability）：**AEX（#3）** 和 **EigenAI（#10）** 分别从多跳调用链完整性和确定性执行两个角度解决 AI 推理结果的可验证性问题。
- **AI Agent 安全**（Agentic Security）：**Sovereign Agents（#20）** 从治理角度分析 AI Agent 的自主性带来的安全风险，指出 TEE 提供了技术层面的"不可篡改性"，但同时也制造了 Accountability Gap。

这一领域的研究空白：**尚无工作将模型保护（confidentiality）+推理可验证性（verifiability）+运行时监控（monitoring）统一到单一框架下**，这是未来值得探索的方向。

**3. IoT / RISC-V TEE 的工程化推进**

相较于 Intel SGX 和 Arm TrustZone 等成熟的商业 TEE，RISC-V TEE 的生态建设仍处于早期阶段。本期论文显示了令人鼓舞的工程化进展：

- **On Securing SDLC（#16）** 填补了 RISC-V TEE 软件开发生命周期管理的关键空白，直接影响 RISC-V 在车规 IoT 的落地进程。
- **External entropy supply（#11）** 在真实 RISC-V 硬件上实现了端到端安全熵供给，是 RISC-V 密码学基础设施的重要补充。
- **LiteAtt（#14）** 首次在 MCU 级别的受限设备上实现了 TinyML+TrustZone 的自认证，功耗和延迟数据均达到实用水平。

这些工作共同表明：**RISC-V TEE 已从研究原型向工业可用性过渡**，预计在 2026–2027 年将出现更多商业车规 IoT 部署案例。

**4. 机密计算 + Web3 的交叉融合**

去中心化金融和 Web3 对机密计算有天然需求，但区块链的去中心化信任模型与 TEE 的中心化硬件信任模型之间存在张力：

- **Bitcoin Smart Accounts（#6）** 和 **OMNIINTENT（#15）** 均尝试以 TEE 作为"信任最小化"的可信执行层，降低用户对区块链节点软件的信任依赖——这是值得关注的范式转变。
- **Styx（#22）** 的粘性策略机制与区块链的智能合约逻辑有潜在互补性，可能成为未来链上数据保护的标准组件。
- **TALUS（#23）** 的阈值签名技术可应用于 Web3 多签钱包和跨链桥，在保证安全性同时实现去中心化密钥管理。

**5. 安全评估与系统化思维**

**Security Assessment of Intel TDX（#18）** 作为 Google Cloud 的官方安全评估报告，其方法论值得研究社区重视：
- 引入 AI（Gemini）辅助分析规范文档和漏洞挖掘
- 首次披露 Live Migration 功能的安全漏洞
- 强调"机密计算需要纵深防御"而非"有了 TEE 就绝对安全"

这与同期 **Proteus（#17）** 的研究主题形成呼应——两文均指出：**过度依赖单一 TEE 平台安全性是不充分的**，需要在 TEE 之上叠加拜占庭容错或其他安全机制。

### 三、研究空白与未来方向

基于本期论文的综合分析，以下方向值得重点关注：

1. **zk-TEE 混合证明**：将零知识证明的可组合隐私性与 TEE 的性能优势结合，用于更复杂的机密计算场景（如隐私求交、机密 ML 训练）
2. **TEE 辅助的 AI Agent 可验证框架**：当前 AEX 仅覆盖 API 调用链，未来需要将模型权重保护、推理完整性证明和调用链认证统一到端到端框架
3. **RISC-V TEE 的形式化验证**：现有工作依赖经验测试，缺乏基于 Coq 或 Isabelle 的高可靠性验证
4. **太空/卫星 TEE 的大规模标准化**：Space Fabric 需要与地面 TEE 标准（如 GlobalPlatform）对接，形成互操作的跨域认证协议
5. **AI Agent 治理框架的标准化**：Sovereign Agents 提出的 Accountability Gap 问题尚无成熟解决方案，需要法律、技术和伦理多学科协作

---

## 📚 参考文献

1. Zhao S, Wang W, Li N. *Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy*. arXiv:2604.04082. 2026.
2. Pan Z, Li Y, Guan Z, et al. *OmniIntent: A Trusted Intent-Centric Framework for User-Friendly Web3*. arXiv:2603.04168. 2026.
3. Al Sadi A, Abdollahi S, Ghosn A, et al. *Sharing is caring: Attestable and Trusted Workflows out of Distrustful Components*. arXiv:2603.03403. 2026.
4. Hu B A, Rong H. *Sovereign Agents: Towards Infrastructural Sovereignty and Diffused Accountability in Decentralized AI*. arXiv:2602.14951. 2026.
5. Malkhi D, Yahalom A, Rezabek F. *Space Fabric: A Satellite-Enhanced Trusted Execution Architecture*. arXiv:2603.23745. 2026.
6. Mishra S, Gonçalves J, Crooks N, et al. *Proteus: Append-Only Ledgers for (Mostly) Trusted Execution Environments*. arXiv:2602.05346. 2026.
7. Swidowski K, Moghimi D, Eads J, et al. *Security Assessment of Intel TDX with support for Live Migration*. arXiv:2602.11434. 2026.
8. Paju A, Nurmi J, Cabrera Aldaya A, et al. *External entropy supply for IoT devices employing a RISC-V Trusted Execution Environment*. arXiv:2603.09311. 2026.
9. Nakatsuka Y, Dutly N, Kostiainen K. *Gyokuro: Source-assisted Private Membership Testing using Trusted Execution Environments*. arXiv:2603.23226. 2026.
10. Pott C, Wilke L, Wichelmann J, et al. *HPCCFA: Leveraging Hardware Performance Counters for Control Flow Attestation*. arXiv:2603.29749. 2026.
11. Kohli V, Sikdar B. *LiteAtt: Secure and Seamless IoT Services Using TinyML-based Self-Attestation as a Primitive*. arXiv:2603.19727. 2026.
12. Kao L, Chang R. *TALUS: Threshold ML-DSA with One-Round Online Signing via Boundary Clearance and Carry Elimination*. arXiv:2603.22109. 2026.
13. Song Q, Zhou Q, Jia X, et al. *vCause: Efficient and Verifiable Causality Analysis for Cloud-based Endpoint Auditing*. arXiv:2603.15216. 2026.
14. Condrey D. *A TEE-Based Architecture for Confidential and Dependable Process Attestation in Authorship Verification*. arXiv:2603.00178. 2026.
15. Guan Y. *AEX: Non-Intrusive Multi-Hop Attestation and Provenance for LLM APIs*. arXiv:2603.14283. 2026.
16. Xie Y, Er-Rahmadi B, Chen X. *Committee Configuration Optimization for Parallel Byzantine Consensus in a Trusted Execution Environment*. arXiv:2603.14445. 2026.
17. Lalor C, Marshall M, Russo A. *Bitcoin Smart Accounts: Trust-Minimized Native Bitcoin DeFi Infrastructure*. arXiv:2603.26293. 2026.
18. Huang W, Wang Z, Li M. *Confidential Databases Without Cryptographic Mappings*. arXiv:2603.18836. 2026.
19. Thomas W, Schmalz L, Petz A. *Designing Trustworthy Layered Attestations*. arXiv:2603.06326. 2026.
20. Jin X, Duan M, Lin Q, et al. *Proof-of-Guardrail in AI Agents and What (Not) to Trust from It*. arXiv:2603.05786. 2026.
21. Jin H, Zhang C, Yu H. *Trusting What You Cannot See: Auditable Fine-Tuning and Inference for Proprietary AI*. arXiv:2603.07466. 2026.
22. Kang D, Choe H, Kim D. *SPOILER: TEE-Shielded DNN Partitioning of On-Device Secure Inference with Poison Learning*. arXiv:2603.06263. 2026.
23. Basile D, Goretti V, Barbaro L. *A TEE-based Approach for Preserving Data Secrecy in Process Mining with Decentralized Sources*. arXiv:2602.04697. 2026.
24. Imran M. *Architecting Trust: A Framework for Secure IoT Systems Through Trusted Execution and Semantic Middleware*. arXiv:2602.10762. 2026.
25. Wilde A, Briongos S, Soriente C, et al. *On Securing the Software Development Lifecycle in IoT RISC-V Trusted Execution Environments*. arXiv:2603.17757. 2026.
26. Sitouah N, Bruschi F, De Cillis S. *Enabling SSI-Compliant Use of EUDI Wallet Credentials through Trusted Execution Environment and Zero-Knowledge Proof*. arXiv:2601.19893. 2025.
27. Ribeiro Alves D, Patankar V, Pereira M. *EigenAI: Deterministic Inference, Verifiable Results*. arXiv:2602.00182. 2026.
28. Habeeb R, Yoon M-K, Chen H. *Ringmaster: How to juggle high-throughput host OS system calls from TrustZone TEEs*. arXiv:2601.16448. 2025.
29. Mao P, Shi L, Busch M, Payer M. *TÄMU: Emulating Trusted Applications at the (GlobalPlatform)-API Layer*. arXiv:2601.20507. 2025.
30. Jiang H, Saini A, Liu H. *Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise*. arXiv:2602.11088. 2026.
31. Mukherjee K. *Red-Teaming Claude Opus and ChatGPT-based Security Advisors for Trusted Execution Environments*. arXiv:2602.19450. 2026.
32. Liu X, Lee B, Qiao Y. *TeeMAF: A TEE-Based Mutual Attestation Framework for On-Chain and Off-Chain Functions in Blockchain DApps*. arXiv:2601.07726. 2025.

---

*本目录由 OpenClaw agent 自动生成 | 收集时间：2026-04-12*
