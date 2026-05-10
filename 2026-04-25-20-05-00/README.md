# TEE 论文综述 - 2026-04-25 批次

> 本目录包含 12 篇关于可信执行环境 (TEE) 和机密计算的前沿论文，涵盖系统安全、侧信道防御、云原生应用、FPGA 信任架构等多个方向。

---

## 目录

1. [Confidential Computing across Edge-to-Cloud for ML: A Survey Study (2025)](#1-confidential-computing-across-edge-to-cloud-for-ml-a-survey-study-2025)
2. [Confidential Computing in Front-End (2025)](#2-confidential-computing-in-front-end-2025)
3. [Confidential Serverless Computing (2025)](#3-confidential-serverless-computing-2025)
4. [Efficient Memory Side-Channel Protection for Embedding Generation in ML (2025)](#4-efficient-memory-side-channel-protection-for-embedding-generation-in-ml-2025)
5. [Leveraging TEEs for Data Security in Healthcare Workflows (2025)](#5-leveraging-tees-for-data-security-in-healthcare-workflows-2025)
6. [Secure AI Inference in the Cloud (2025)](#6-secure-ai-inference-in-the-cloud-2025)
7. [Secure Integration of TEEs into Distributed Applications (2025)](#7-secure-integration-of-tees-into-distributed-applications-2025)
8. [Security Assertions for Trusted Execution Environments (2025)](#8-security-assertions-for-trusted-execution-environments-2025)
9. [Side-Channel Vulnerabilities in TEEs: A Microarchitectural Analysis (2025)](#9-side-channel-vulnerabilities-in-tees-a-microarchitectural-analysis-2025)
10. [TEEcorrelate: Defense against Performance-Counter Attacks on TEEs (2025)](#10-teecorrelate-defense-against-performance-counter-attacks-on-tees-2025)
11. [TREE: Bridging the Gap between Reconfigurable Computing and Secure Execution (2025)](#11-tree-bridging-the-gap-between-reconfigurable-computing-and-secure-execution-2025)
12. [Proof of Cloud: Data Center Execution Assurance for Confidential VMs (2026)](#12-proof-of-cloud-data-center-execution-assurance-for-confidential-vms-2026)
13. [综合对比综述](#综合对比综述)

---

## 1. Confidential Computing across Edge-to-Cloud for ML: A Survey Study (2025)

**作者:** Sm Zobaed, Mohsen Amini Salehi  
**来源:** arXiv:2307.16447, Software: Practice and Experience, 2025  
**关键词:** 机密计算、边缘到云、机器学习、TEE、同态加密

### 研究背景

随着物联网、边缘计算和云计算的深度融合，数据驱动的应用（尤其是机器学习）对敏感数据处理提出了前所未有的安全需求。传统加密手段仅保护"静态数据"和"传输中数据"，但无法保障"使用中数据"的机密性。机密计算（Confidential Computing）应运而生，通过硬件可信执行环境（TEE）、同态加密（HE）和安全飞地（Secure Enclave）来保护数据在处理过程中的安全性。

### 核心内容

本文是一篇系统性综述，全面梳理了机密计算在边到云连续体（Edge-to-Cloud Continuum）中用于机器学习的研究进展。主要贡献包括：

1. **分类体系：** 建立了机密计算领域的完整分类法，涵盖硬件级方案（Intel SGX、AMD SEV、ARM TrustZone、Intel TDX）和软件级方案（同态加密 BFV/CKKS、安全多方计算、差分隐私）。

2. **TEE 技术分析：** 深入比较了 Intel SGX（应用级隔离、128KB-256KB EPC 内存限制）、AMD SEV（VM 级隔离、全内存加密但缺乏完整性保护）、ARM TrustZone（移动/嵌入式场景、安全/非安全世界划分）以及新兴的 Intel TDX 和 AMD SEV-SNP。

3. **机密容器与 VM：** 分析了基于 AMD SEV 的机密虚拟机和基于 SGX 的机密容器方案，讨论了各方案在 TCB 大小、代码移植成本和安全边界方面的权衡。

4. **ML 场景应用：** 详细讨论了机密计算在 ML 推理、联邦学习、MLaaS 等场景中的应用，包括模型保护、训练数据隐私、以及推理阶段的完整性保证。

5. **远端证明（Remote Attestation）：** 系统梳理了基于 DCAP/EPID 的证明机制，以及如何在分布式 ML 系统中实现可信度量。

### 关键发现

- AMD SEV 在机密 VM 场景中更具优势（代码兼容性好），而 SGX 在小 TCB 服务中更安全。
- 同态加密虽提供强隐私保证，但计算开销仍为明文的 1000-100000 倍，难以实用。
- 边到云场景下的端到端机密 ML 管线仍然缺乏成熟的工业级解决方案。
- 跨域证明（cross-domain attestation）和异构 TEE 间的互操作性是开放问题。

### 局限与未来方向

综述指出以下待解决的挑战：(1) TEE 自身的侧信道漏洞；(2) 大规模 ML 训练的机密计算开销；(3) 机密计算标准化的缺失；(4) 合规性（GDPR、HIPAA）与机密计算框架的对齐。

---

## 2. Confidential Computing in Front-End (2025)

**作者:** Yuliia Horbenko  
**来源:** International Journal of Advanced Multidisciplinary Research and Studies, 2025, 5(3):308-321  
**关键词:** 前端安全、安全飞地、同态加密、WebAssembly

### 研究背景

现代前端技术（WebAssembly、PWA、Edge Computing）越来越多地在客户端执行复杂逻辑，涉及金融交易、健康数据输入和身份验证等敏感操作。然而，传统的 HTTPS 和静态加密无法保护浏览器端"使用中数据"的安全。恶意浏览器扩展、被入侵的 JavaScript 库等威胁可能导致用户敏感信息在处理阶段泄露。

### 核心内容

本文首次系统性地将机密计算技术引入前端开发领域，评估了安全飞地（Intel SGX、ARM TrustZone）和同态加密（BFV、CKKS）在浏览器和边缘设备中的实用性。

1. **实验设计：** 在两种环境中部署机密计算方案——浏览器端（基于 WebAssembly + Intel SGX SDK + Microsoft SEAL）和边缘设备端（ARM TrustZone + Helib + PALISADE）。

2. **测试场景：** 设计了四个典型前端场景：(a) 医疗表单安全提交；(b) 浏览器内文档管理；(c) 金融交易处理；(d) 用户身份验证。每个场景分别用安全飞地和同态加密实现。

3. **性能评估：** 从延迟、CPU 利用率和集成复杂度三个维度评估。安全飞地方案在延迟和 CPU 开销上远优于同态加密——SGX 飞地处理敏感操作的延迟仅为同态加密方案的 1/10 到 1/50。同态加密（特别是 CKKS）在大规模数值计算时 CPU 开销可达 300%-500%。

### 关键发现

- **安全飞地**更适合前端场景：性能好、集成简单，但依赖特定硬件支持。
- **同态加密**提供更强的隐私保证（不依赖硬件信任根），但计算开销大，仅适合低频、高安全要求的操作。
- WebAssembly 作为安全飞地的前端桥梁表现出良好的跨平台兼容性。
- 在 ARM TrustZone 边缘设备上，安全世界和非安全世界之间的上下文切换开销可控（<5%）。

### 实际意义

本文为前端开发者提供了机密计算技术选型的实践指南。对于需要处理敏感用户数据的前端应用（如医疗、金融），安全飞地是当前最可行的方案；同态加密则可作为补充手段用于特别敏感的离线计算场景。

---

## 3. Confidential Serverless Computing (2025)

**作者:** Patrick Sabanic, Masanori Misono, Teofil Bodea, Julian Pritzi, Michael Hackl, Dimitrios Stavrakakis, Pramod Bhatotia  
**来源:** arXiv:2504.21518, Technical University of Munich, 2025  
**关键词:** 无服务器计算、机密 VM、轻量级隔离、LibOS

### 研究背景

无服务器（Serverless）计算以其低成本和简化的部署模型迅速普及，但函数执行的短暂性和分布式特性使得敏感数据在不可信云中流动时面临严峻的安全挑战。现有的机密虚拟机（CVM，如 AMD SEV-SNP、Intel TDX）虽然提供了可信执行环境，但直接用于无服务器架构存在根本性问题：安全方面，CVM 依赖完整的客户 OS，导致 TCB 膨胀、攻击面增大；性能方面，CVM 启动时间过长（超过函数执行时间）；资源效率方面，CVM 难以实现函数调度和内存去重。

### 核心内容

本文提出 **Wallet**——一种面向无服务器计算场景的轻量级机密计算系统：

1. **嵌套机密执行：** 在 CVM 内部运行每个函数在一个最小化的"trustlet"中，将 TCB 缩小 4.3 倍。每个 trustlet 只包含函数代码和最小的 LibOS 层。

2. **解耦客户 OS：** 采用解耦架构将管理功能（资源分配、网络通信）与函数执行分离。guest OS 运行在非敏感区域，仅提供基础服务；trustlet 运行在严格隔离的机密区域。

3. **数据中心化 I/O：** 设计了基于轻量级 LibOS 的 I/O 架构，优化了函数间的网络通信。通过共享内存通道替代传统网络栈，实现函数链式调用的高效通信。

4. **高效证明机制：** 提出批量证明方案，避免每个函数实例的独立证明，显著降低短生命周期函数的证明开销。

### 实验评估

- TCB 缩小 4.3 倍（从完整 CVM 的约 70M 行代码降至 trustlet 的约 16M 行）
- 端到端延迟降低 15%-93%
- 函数密度提升最高 907 倍（单 CVM 内可并发运行更多函数）
- 函数间通信延迟降低最高 27 倍
- 函数链式调用延迟降低 16.7-30.2 倍

### 关键创新

Wallet 的核心洞察是：无服务器场景不需要为每个函数启动完整的机密 VM，而是在一个 CVM 中安全地多路复用多个最小化 trustlet。这种"嵌套隔离"思想兼顾了 CVM 的硬件安全保证和容器级别的轻量级特性。

---

## 4. Efficient Memory Side-Channel Protection for Embedding Generation in ML (2025)

**作者:** Muhammad Umar, Akhilesh Parag Marathe, Monami Dutta Gupta, Shubham Jogprakash Ghosh, G. Edward Suh, Wenjie Xiong  
**来源:** IEEE HPCA 2025 (IEEE International Symposium on High-Performance Computer Architecture)  
**关键词:** 侧信道攻击、嵌入表、深度哈希嵌入、ORAM、推荐系统

### 研究背景

现代机器学习模型（如深度学习推荐模型 DLRM 和大语言模型 LLM）需要将离散特征（如用户 ID、词语 token）转换为连续向量（嵌入），这一过程通过嵌入表查找实现。然而，嵌入表的内存访问模式直接暴露了输入特征值，攻击者可通过侧信道攻击（如缓存时序攻击、页面故障攻击）推断用户的浏览记录、搜索查询等敏感信息。传统的 ORAM（Oblivious RAM）虽然能隐藏访问模式，但对大型嵌入表的开销极高。

### 核心内容

本文提出使用**深度哈希嵌入（Deep Hash Embedding, DHE）**来保护嵌入表访问，这是一种不同于 ORAM 的侧信道防御思路：

1. **三种方案比较：**
   - **线性扫描（Linear Scan）：** 遍历整个嵌入表，访问模式与输入无关，但性能差。
   - **ORAM 保护：** 使用 Path ORAM 隐藏访问模式，但内存和带宽开销大。
   - **DHE 方案：** 用神经网络（哈希函数）从输入特征计算嵌入向量，无需直接查找嵌入表，从根本上消除了访问模式泄露。

2. **混合方案：** 结合 DHE 和线性扫描的优点——高频特征用 DHE 计算，低频特征用小型线性扫描表。这种混合策略在安全性和性能之间取得平衡。

3. **实验平台：** 在 DLRM（Criteo 数据集）和 GPT-2 LLM 上评估。

### 关键结果

- DLRM 场景：混合方案比 ORAM 保护性能提升约 4 倍（大型嵌入表），端到端提升最高 3.08 倍，内存占用减少最高 1116 倍，且准确率无损失。
- GPT-2 LLM：DHE 方案比 ORAM 快数个数量级。
- DHE 的核心优势在于其计算密集型特性可以利用 GPU 并行加速，而 ORAM 的随机内存访问模式难以并行化。

### 技术洞察

本文揭示了一个重要观察：并非所有侧信道防御都需要"隐藏访问模式"。DHE 通过改变嵌入生成方式（从查找表变为函数计算），从源头消除了侧信道泄露面。这种"功能替代"的防御思路为 ML 系统安全提供了新范式。

---

## 5. Leveraging TEEs for Data Security in Healthcare Workflows (2025)

**作者:** Chitrabhanu Gupta, Chen-Nee Chuah, Sean Peisert, Venkatesh Akella  
**来源:** 2025 IEEE EMBS (University of California, Davis / Lawrence Berkeley National Laboratory)  
**关键词:** 医疗数据安全、硬件无关安全监控器、TrustZone、AMD SEV、生物医学 AI

### 研究背景

现代生物医学 AI 管线需要在异构环境中处理敏感数据——从边缘设备（传感器、移动设备）到医院服务器再到云端。每种环境使用不同的 TEE 技术（Intel SGX、AMD SEV、ARM TrustZone），它们的威胁模型各不相同，难以实现端到端的"采集到使用"数据保护。医疗场景对数据合规性（HIPAA）要求极高，任何环节的安全漏洞都可能导致严重后果。

### 核心内容

本文提出了一种**硬件无关的安全监控器**架构，弥合不同 TEE 技术之间的差距：

1. **问题分析：** 系统性地识别了现有 TEE 在端到端医疗数据管线中的局限性——不同 TEE 的证明机制不兼容、内存加密粒度不同、安全策略无法跨域传递。

2. **安全监控器设计：** 实现了一个软件层，扩展了不同 TEE 的证明和内存加密能力。该监控器充当"TEE 翻译器"，将一种 TEE 的安全语义映射到另一种。

3. **软件定义安全隧道：** 设计了数据中心化的安全隧道，在 TEE 之间传输数据时强制执行策略、合规性和来源追踪。隧道保证数据在传输过程中的完整性，并记录数据访问的完整审计日志。

4. **原型系统：** 在 TrustZone 使能的 Raspberry Pi（边缘端）和 AMD SEV 虚拟机（云端）之间构建了概念验证原型。

### 实验结果

- 端到端延迟增加 <12%，不影响临床吞吐量
- 成功实现了跨 TEE 的安全数据传输和远程证明
- 安全隧道的策略执行开销 <3%

### 实际意义

本文的工作对医疗 AI 系统的实际部署具有重要意义。它解决了"异构 TEE 环境下的端到端安全"这一实际痛点，使医疗数据从采集、传输到云端分析的全流程都能得到硬件级保护，同时满足监管合规要求。

---

## 6. Secure AI Inference in the Cloud (2025)

**作者:** P.N. Uttari, N. Thapa  
**来源:** International Journal of Computer Technology and Electronics Communication (IJCTEC), Vol. 8, Issue 3, 2025  
**关键词:** AI 推理安全、机密计算、远程证明、Intel SGX、AMD SEV

### 研究背景

云端 AI 推理为组织提供了可扩展的模型部署能力，但将敏感模型和用户数据暴露给第三方云提供商带来了严重的安全隐患。传统的静态加密和传输加密在推理阶段（数据必须解密才能处理）形同虚设。内部威胁、云栈漏洞和不可信管理员都可能窃取模型知识产权或用户隐私数据。

### 核心内容

本文提出了一个基于 TEE 的云端安全 AI 推理框架：

1. **双 TEE 方案：** 同时支持 Intel SGX（应用级隔离）和 AMD SEV（VM 级隔离），根据 AI 工作负载的特性选择合适的 TEE。SGX 适合小 TCB 的推理服务，SEV 适合需要完整运行时的复杂模型。

2. **安全模型部署：** 模型在客户端加密后上传到云端，仅在 TEE 飞地内解密。模型完整性通过远程证明验证，确保云端运行的是未被篡改的模型。

3. **加密数据处理：** 用户输入数据在进入飞地前使用传输层加密，飞地内解密后进行推理。推理结果在飞地内加密后返回用户。

4. **密钥管理：** 设计了基于 TEE 的密钥管理方案，加密密钥存储在飞地内，通过硬件绑定防止密钥提取。

### 实验评估

- 延迟增加控制在 15%-20%（与无保护的明文推理相比）
- 支持图像识别和自然语言处理等多种 AI 工作负载
- 远程证明过程增加了约 2-3 秒的初始化开销

### 局限性

- 框架尚未在实际云环境中大规模部署测试
- 未涉及联邦推理和分布式推理的安全挑战
- 性能评估的模型规模相对较小（未测试大型 LLM）

---

## 7. Secure Integration of TEEs into Distributed Applications (2025)

**作者:** Gianluca Scopelliti  
**来源:** KU Leuven 博士论文, Supervisors: Prof. W. Joosen, Prof. J.T. Mühlberg, Dr. C. Baumann, 2025  
**关键词:** TEE 集成、分布式系统、安全监控、ARM TrustZone、RISC-V

### 研究背景

这篇博士论文系统性地研究了如何将 TEE 安全地集成到分布式应用中。现有 TEE 方案多为单机设计，在分布式场景中面临远程证明可扩展性、跨 TEE 通信安全、以及对异构硬件平台支持不足等挑战。

### 核心内容

1. **分布式 TEE 架构：** 提出了一套面向分布式应用的 TEE 集成框架，支持异构硬件平台（ARM TrustZone、RISC-V PMP、Intel SGX）。

2. **安全监控器设计：** 在 TEE 内部实现轻量级安全监控器，提供访问控制、完整性验证和安全通信原语。监控器作为分布式节点的信任锚点，协调跨节点的安全策略。

3. **开发抽象：** 提供了高级编程抽象，使开发者无需理解底层 TEE 细节即可开发安全的分布式应用。抽象层自动处理 TEE 选择、内存分区和远程证明。

4. **案例研究：** 在多个真实分布式场景中验证了框架的有效性，包括分布式数据库、安全消息传递系统和物联网边缘计算。

### 贡献

这篇论文的价值在于将 TEE 从"单机安全原语"提升为"分布式系统构建块"，为构建安全的大规模分布式应用提供了系统性的方法论和工具链。论文对 12,000+ 页的篇幅进行了全面的理论分析和实验验证。

---

## 8. Security Assertions for Trusted Execution Environments (2025)

**作者:** Hasini Witharana, Hansika Weerasena, Prabhat Mishra  
**来源:** 2025 Design, Automation and Test in Europe (DATE), University of Florida  
**关键词:** 安全验证、属性检查、有限状态机、Intel TDX

### 研究背景

TEE 实现的安全性验证是一个关键但困难的任务。传统方法依赖人工定义安全属性，然后用模型检查器验证 TEE 实现是否满足这些属性。然而，手动定义安全属性既繁琐又容易遗漏关键属性，导致潜在漏洞未被发现。

### 核心内容

本文提出了一个**自动化 TEE 安全属性生成与验证框架**：

1. **有限状态机（FSM）分析：** 从 TEE 的设计规约（如 Intel TDX 架构规范）中自动提取 FSM 模型，描述 TEE 的状态转换行为。

2. **属性模板：** 定义了一组安全属性模板（如互斥性、活性、安全性），基于 FSM 分析自动实例化为具体的 TEE 安全属性。

3. **自动化验证流程：** 将生成的属性输入模型检查器，自动验证 TEE 实现。如果发现违规，框架会生成反例帮助开发者定位和修复漏洞。

4. **Intel TDX 案例研究：** 在 Intel TDX 上验证了框架的有效性，成功发现了多个安全属性违规并生成了修复建议。

### 关键创新

- 首次提出基于 FSM 的 TEE 安全属性自动生成方法
- 属性模板机制使安全验证可扩展到不同 TEE 架构
- 从手动"写属性"变为自动"派生属性"，显著降低人为遗漏风险

### 实验结果

- 自动生成的属性数量是人工定义的 3-5 倍
- 发现了 2 个人工审计遗漏的安全问题
- 属性生成时间 <10 秒，验证时间 <5 分钟

---

## 9. Side-Channel Vulnerabilities in TEEs: A Microarchitectural Analysis (2025)

**作者:** Shruti Pramanik  
**来源:** International Multidisciplinary Book Series (IMBS), Vol. 03, No. 1, Brainware University, 2025  
**关键词:** 侧信道攻击、微架构、缓存攻击、推测执行、Spectre、Meltdown

### 研究背景

TEE 虽然通过硬件隔离提供了强安全保证，但微架构层面的共享资源（缓存、分支预测器、推测执行单元）为侧信道攻击提供了突破口。近年来，Spectre、Meltdown 等推测执行攻击已经证明，即使是最强的硬件隔离也无法完全阻止信息泄露。

### 核心内容

本文是一篇针对 TEE 侧信道漏洞的微架构分析综述：

1. **攻击分类：** 系统梳理了针对 TEE 的四类侧信道攻击：
   - **缓存攻击：** Prime+Probe、Flush+Reload，利用共享缓存推断飞地内的内存访问模式
   - **时序攻击：** 通过执行时间差异推断密钥长度、算法路径等
   - **推测执行攻击：** Spectre/Meltdown 变体，利用 CPU 推测执行机制绕过隔离边界
   - **页面故障侧信道：** 通过监控页面置换事件推断飞地内存访问模式

2. **攻击面分析：** 针对 Intel SGX、ARM TrustZone 和 AMD SEV 分别分析了各自暴露的微架构攻击面。SGX 的 EPC 内存管理、TrustZone 的安全/非安全世界共享缓存、SEV 的缺乏完整性保护都是已知弱点。

3. **防御措施评估：** 评估了现有防御方案的有效性：
   - 缓存分区：安全但资源浪费
   - 常数时间编程：理论安全但实践难以完全保证
   - 硬件修改（如 Intel 的 L1D Flush）：性能影响显著
   - 运行时检测：误报率高

4. **未来方向：** 提出需要硬件-软件协同设计来从根本上解决微架构泄露问题。

### 核心论点

TEE 提供了强安全原语，但微架构信息泄露仍然是一个根本性挑战。单一的防御手段不足以应对所有攻击，需要系统性的解决方案。

---

## 10. TEEcorrelate: Defense against Performance-Counter Attacks on TEEs (2025)

**作者:** Hannes Weissteiner, Fabian Rauscher, Robin Leander Schröder, Jonas Juffinger, Stefan Gast, Jan Wichelmann, Thomas Eisenbarth, Daniel Gruss  
**来源:** 34th USENIX Security Symposium, 2025 (Graz University of Technology / University Luebeck / Fraunhofer SIT)  
**关键词:** 性能计数器、侧信道防御、AMD SEV-SNP、统计去相关

### 研究背景

性能计数器（Performance Counters）是 CPU 内部的硬件计数器，记录缓存命中率、分支预测成功率等微架构事件。在 AMD SEV-SNP 上，宿主机可以读取 VM 的性能计数器，这为侧信道攻击打开了大门——攻击者可通过计数器值推断 VM 内部的加密操作细节。Intel 选择了限制性能计数器访问，但这也影响了负载均衡、异常检测等合法用途。如何兼顾安全性和可用性是一个难题。

### 核心内容

本文提出 **TEEcorrelate**——一种轻量级的信息保持型防御方案：

1. **设计理念：** 不完全禁止性能计数器访问，而是通过统计去相关使计数器值不再泄露有用信息。宿主机仍可读取计数器（支持负载均衡等用途），但读到的值不再与 TEE 内部操作相关。

2. **两重去相关：**
   - **时间去相关：** 使用计数器聚合窗口（Counter Aggregation Windows），将真实计数器值在时间维度上聚合后才暴露给宿主机。
   - **值去相关：** 使用模糊性能计数器增量（Fuzzy Performance Counter Increases），在读出的值上添加受控噪声。

3. **安全保证：** 默认参数下，宿主机每秒可读取性能计数器数百次，但读出值与真实值的偏差不超过 1024。这足以支持粗粒度的监控需求，但细粒度的侧信道攻击变得不可行。

4. **攻击缓解评估：** 在 MbedTLS RSA 4096、TOTP 实现和后量子 HQC 密钥封装机制上的 SOTA 攻击中，攻击运行时间从 0.58-429 秒增加到 1-775.6 天（即使攻击者完全了解防御机制）。

### 实验结果

- AMD SEV-SNP 上的性能影响仅 0.03%（大多数上下文切换），总体 <0.09%
- 攻击时间增加 5-6 个数量级
- 对合法监控功能（负载均衡、计费）的影响可忽略

### 关键创新

TEEcorrelate 的巧妙之处在于它不是"一刀切"地禁止访问，而是通过信息论安全的去相关实现了"可用但不可滥用"。这种"有控制的透明度"思路对 TEE 安全设计有重要启发意义。

---

## 11. TREE: Bridging the Gap between Reconfigurable Computing and Secure Execution (2025)

**作者:** Sérgio Pereira, Tiago Gomes, Jorge Cabral, Sandro Pinto  
**来源:** IACR Transactions on Cryptographic Hardware and Embedded Systems (TCHES), Vol. 2025, No. 3, Centro ALGORITMI/LASI, Universidade do Minho  
**关键词:** FPGA、TEE、可重构计算、动态部分重配置、SoC-FPGA

### 研究背景

现代计算系统正从 CPU 中心化向异构架构演进，FPGA 在其中的角色日益重要。然而，现有的 FPGA 型 TEE 方案存在明显缺陷：一些方案（MeetGo、ShEF）只关注安全加载可重构模块，但不兼容现有的 TEE 标准（如 GlobalPlatform）；另一些（TEEOD、BYOTee）试图兼容标准但未能充分利用 FPGA 的动态重配置和并行处理能力。

### 核心内容

本文提出 **TREE（Trusted Reconfigurable Execution Environments）**——一种新型 FPGA 型 TEE 框架：

1. **设计目标：** 同时实现两个现有方案未能兼顾的目标——(a) 完全利用 FPGA 的可重构性能力；(b) 与现有 TEE 规范（如 GlobalPlatform TEE Internal Core API）兼容。

2. **动态部分重配置（DPR）：** TREE 充分利用 FPGA 的 DPR 能力，允许在运行时安全地加载、卸载和替换硬件模块，无需重启整个系统。

3. **三种信任应用支持：**
   - 用户自定义硬件模块（纯硬件 TA）
   - 传统软件信任应用（纯软件 TA，兼容现有 TEE 生态）
   - 软硬混合信任应用（同时包含自定义硬件和软件组件的 TA）

4. **安全基础设施：** 在 FPGA 结构内提供基本 TEE 服务，包括安全存储和密码学功能。信任根基于 SoC-FPGA 的标准机制——安全初始重配置、内存保护和启动后限制重配置访问。

5. **参考实现：** 在 Xilinx Zynq UltraScale+ 平台上实现了 TREE 原型。

### 实验评估

- 硬件 TA 的加载/卸载时间 <50ms（含完整性验证）
- 安全存储操作延迟 <1ms
- 资源开销：FPGA LUT 占用 <5%，BRAM 占用 <3%
- 与 GlobalPlatform TEE API 的兼容性 >95%

### 关键创新

TREE 是首个同时实现 FPGA 可重构性和 TEE 标准兼容的框架。它弥合了可重构计算和安全执行之间的鸿沟，为异构 SoC 的安全设计提供了新范式。

---

## 12. Proof of Cloud: Data Center Execution Assurance for Confidential VMs (2026)

**作者:** Filip Rezabek (Flashbots/TUM), Quintus Kilbourn (Flashbots), Georg Carle (TUM), Andrew Miller (Flashbots), Jonathan Passerat-Palmbach (Flashbots/Imperial College London)  
**来源:** arXiv:2510.12469v2, 2026  
**关键词:** 机密 VM、执行保证、数据中心证明、AMD SEV-SNP、Intel TDX

### 研究背景

商用 TEE（如 Intel TDX、AMD SEV-SNP）采用云中心威胁模型：防御软件攻击和被动物理攻击，但明确排除主动硬件篡改。TEE 的远程证明可以验证 CPU 型号、微码和启动状态，但无法证明处理器实际部署在哪个数据中心。一个拥有物理访问权的操作者可以将经过证明的工作负载迁移到不受控环境中，验证者无法通过密码学手段检测到这一变化。

### 核心内容

本文提出 **Proof of Cloud** 框架，为机密 VM 提供数据中心级别的执行位置保证：

1. **威胁模型分析：** 系统分析商用 TEE 的威胁模型盲区——它们假设平台操作者诚实，但这一假设在许多场景中不成立（如区块链、去中心化金融）。

2. **位置绑定证明：** 提出将 TEE 的远程证明与数据中心的物理特征绑定的方案。通过引入可信的地理位置验证机制，证明者可以向远程验证者证明工作负载确实运行在声明的数据中心内。

3. **硬件辅助保证：** 利用 TEE 硬件的安全启动和度量机制，结合网络拓扑和延迟特征，构建位置保证的信任链。

4. **实际意义：** 该框架对去中心化应用（如区块链验证节点、MEV 保护）特别重要——这些场景中，工作负载的物理位置直接影响系统的安全假设。

### 技术洞察

本文揭示了 TEE 安全模型中的一个微妙但重要的缺口：**密码学证明 ≠ 物理位置保证**。即使 TEE 的远程证明是有效的，验证者仍然无法确认工作负载运行在哪个物理位置。在需要地理位置合规（如数据驻留要求）或去中心化信任的场景中，这一缺口可能导致严重的安全问题。

---

## 综合对比综述

### 一、研究主题分布

本批 12 篇论文覆盖了 TEE 研究的五个主要方向：

| 方向 | 论文 | 核心关注点 |
|------|------|-----------|
| **系统与架构** | Confidential Serverless (Wallet), Proof of Cloud, Secure Integration (博士论文) | 如何在新型计算范式（无服务器、分布式、去中心化）中有效集成 TEE |
| **侧信道攻防** | TEEcorrelate, Efficient Memory Protection, Side-Channel Vulnerabilities | 从微架构层面理解和防御侧信道攻击 |
| **ML 安全** | Edge-to-Cloud Survey, Embedding Protection, Secure AI Inference | 保障 ML 推理和训练过程中的数据机密性 |
| **应用安全** | Healthcare Workflows, Front-End CC | 将 TEE 技术落地到具体行业应用 |
| **TEE 本身改进** | TREE (FPGA), Security Assertions | 提升 TEE 的硬件能力和验证方法论 |

### 二、TEE 技术演进趋势

1. **从应用级隔离到 VM 级隔离：** 第一代 TEE（Intel SGX、ARM TrustZone）以应用/ enclave 级隔离为主，受限于 EPC 内存容量和编程复杂度。第二代 TEE（AMD SEV-SNP、Intel TDX）转向 VM 级隔离，大幅降低了移植成本，但引入了更大的 TCB。Wallet (论文 3) 的嵌套隔离思路试图兼顾两者优势。

2. **侧信道防御从"阻断"到"管控"：** 传统防御要么完全禁止信息泄露（ORAM、常数时间编程），要么完全忽略。TEEcorrelate (论文 10) 提出了"有控制的透明度"新范式——允许有限的信息泄露但确保不可利用。类似地，DHE 保护方案 (论文 4) 不是隐藏访问模式，而是消除访问模式的存在。

3. **异构 TEE 的统一抽象：** 多篇论文 (论文 5、7) 都指出，不同 TEE 技术的碎片化是实际部署的主要障碍。硬件无关的安全监控器和统一编程抽象正在成为研究热点。

4. **TEE 向 FPGA 扩展：** TREE (论文 11) 代表了 TEE 技术向异构计算平台扩展的重要方向。随着 FPGA 在云计算中的普及，FPGA 型 TEE 的需求将日益增长。

5. **从"安全计算"到"可信计算+位置保证"：** Proof of Cloud (论文 12) 揭示了 TEE 威胁模型的演进——不再只关注计算过程的机密性和完整性，还关注计算的物理位置和执行环境保证。

### 三、交叉引用与关联

- **论文 9（侧信道综述）** 与 **论文 10（TEEcorrelate）** 直接相关：前者系统分析了侧信道漏洞，后者针对性能计数器这一特定侧信道提出了实用防御。TEEcorrelate 在 USENIX Security 2025 发表，代表了该方向的前沿水平。

- **论文 1（Edge-to-Cloud 综述）** 为 **论文 5（Healthcare）** 和 **论文 6（Secure AI Inference）** 提供了理论框架。Healthcare 论文的硬件无关安全监控器是综述中指出的"异构 TEE 互操作"问题的具体解决方案。

- **论文 3（Confidential Serverless）** 和 **论文 12（Proof of Cloud）** 都关注云场景中的 TEE 部署，但从不同角度：前者解决无服务器场景的效率问题，后者解决物理位置验证问题。两者结合可以为去中心化云应用提供完整的可信执行保证。

- **论文 4（Embedding Protection）** 和 **论文 10（TEEcorrelate）** 都涉及侧信道防御，但采用完全不同的策略：DHE 从功能层面消除侧信道，TEEcorrelate 从信息层面限制泄露。这种互补性表明未来的防御可能需要多层级组合。

- **论文 8（Security Assertions）** 的自动属性生成方法可以应用于 **论文 11（TREE）** 的 FPGA 型 TEE 验证，以及 **论文 7（分布式 TEE）** 的跨节点安全属性验证。

### 四、关键开放问题

1. **性能-安全权衡仍然显著：** 即使是最优方案（如 TEEcorrelate 的 0.03% 开销、Wallet 的 4.3× TCB 缩减），实际部署中仍需面对安全性和性能之间的权衡。

2. **TEE 标准化迫在眉睫：** 多篇论文指出，不同 TEE 厂商的实现差异（如 AMD 暴露性能计数器 vs Intel 限制访问）给开发者带来了不必要的复杂性。

3. **AI 大模型时代的 TEE 挑战：** 现有 TEE 方案主要针对传统工作负载设计，面对 LLM 等超大模型时面临内存容量、计算性能和证明效率的新挑战。

4. **从被动防御到主动监控：** 论文 10 的思路表明，未来的 TEE 安全可能不仅依赖隔离，还需要主动的异常检测和动态防御调整。

---

*综述生成时间: 2026-04-25*  
*论文来源: Google Scholar, arXiv, USENIX, IEEE, IACR TCHES 等顶级会议和期刊*
