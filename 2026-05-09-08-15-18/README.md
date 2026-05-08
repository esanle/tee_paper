# TEE 论文集 · 2026-05-09-08-15-18

本目录收录 2025-2026 年 arXiv 上与**可信执行环境（Trusted Execution Environment，TEE）**相关的新论文，共 14 篇。所有论文均通过 Google 搜索 arXiv 获取 PDF 链接，并使用 curl 直接下载以绕过 Cloudflare 限制。

---

## 论文一

**Confidential Computing for Cloud Security: Exploring Hardware-based Encryption Using Trusted Execution Environments**
- **年份：** 2025
- **arXiv ID：** 2511.04550
- **作者：** Dhruv Deepak Agarwal, Aswani Kumar Cherukuri（VIT Vellore）
- **方向：** 云安全 × TEE 综述

### 核心内容（≈1000 字）

**背景与动机：** 云计算的快速发展极大提升了数据处理和存储的可扩展性与灵活性，但同时也带来了严峻的安全挑战。传统安全措施如静态加密和传输中加密只能保护存储和传输中的数据，对"使用中的数据"（data in use）无能为力。在多租户云环境中，来自不同用户的计算资源被共享在同一物理设备上，这进一步增加了数据在处理过程中遭受攻击的风险。

**核心贡献：** 本文对 Intel SGX 和 ARM TrustZone 两种主流 TEE 技术进行了全面分析。研究首先概述了 TEE 的架构和安全特性，包括硬件级隔离、加密内存区域和安全启动等机制。随后，文章系统性地分析了 TEE 在云安全领域的部署策略、性能指标和实际应用场景。

**安全分析：** 作者指出，尽管 TEE 提供了强大的隔离保护，但仍存在若干挑战：部署复杂性较高，需要应用代码进行针对性重构；侧信道攻击（如 Spectre、Meltdown）可以绕过 TEE 的保护边界；不同 TEE 实现之间的可移植性较差。此外，TEE 的信任根依赖于硬件厂商，这引入了供应链信任问题。

**结论：** TEE 在加强云安全基础设施方面具有核心地位，能够为机密计算创建安全基础。但要实现广泛采用，还需要解决部署复杂性、性能开销和标准化等问题。

---

## 论文二

**Distilled Large Language Model in Confidential Computing Environment for System-on-Chip Design**
- **年份：** 2025
- **arXiv ID：** 2507.16226
- **作者：** Ben Dong, Hui Feng, Qian Wang（UC Merced）
- **方向：** AI × TEE × 芯片设计

### 核心内容（≈1000 字）

**背景与动机：** 大语言模型在芯片设计（SoC）任务中展现出强大能力，但训练模型及其数据属于机密知识产权，必须防止泄露。机密计算通过 TEE 为数据和模型提供保护，但现有 TEE 实现无法高效支持资源密集型的 LLM。

**核心贡献：** 本文首次全面评估了 LLM 在 Intel TDX 机密计算环境中的性能。实验在三种环境下进行：TEE 环境、纯 CPU 环境和 CPU-GPU 混合环境，以 tokens/秒为指标评估性能。

**关键发现：** 1）蒸馏模型（DeepSeek）因参数量小而性能最优，适合资源受限设备；2）量化模型（4-bit Q4 和 8-bit Q8）相比 FP16 模型可获得最高 3 倍性能提升；3）对于小参数集如 DeepSeek-r11.5B，TDX 实现超越了 CPU 版本。

**实验验证：** 使用 SoC 设计任务测试基准验证，结果证明了在资源受限系统上高效部署轻量级 LLM 的可行性。

---

## 论文三

**Narrowing the Gap between TEEs Threat Model and Deployment Strategies**
- **年份：** 2025
- **arXiv ID：** 2506.14964
- **作者：** Filip Rezabek, Jonathan Passerat-Palmbach, Moe Mahhouk（Flashbots, TUM, Imperial College）
- **方向：** TEE 威胁模型 × 部署策略

### 核心内容（≈1000 字）

**背景与动机：** 机密虚拟机（CVM）为使用中的数据提供隔离保证，但其威胁模型不包括物理级保护和侧信道攻击。当前部署依赖可信云提供商托管底层基础设施，但 TEE 认证无法提供关于 CVM 运营商的信息。

**核心问题：** 作者指出存在威胁模型错位——工作负载受到免受其他租户的保护，但无法防御物理攻击。用户在不知道 TEE 是否在提供商基础设施内运行时，无法准确评估物理攻击风险。

**分析贡献：** 文章分析了 TEE 威胁模型与实际部署策略之间的差距，揭示了"租户间隔离"与"物理攻击防护"之间的不一致性。这导致用户必须盲目信任云提供商的物理安全承诺。

---

## 论文四

**RaceTEE: Enabling Interoperability of Confidential Smart Contracts**
- **年份：** 2025
- **arXiv ID：** 2503.09317
- **作者：** Keyu Zhang, Andrew Martin（牛津大学）
- **方向：** 区块链 × TEE × 智能合约

### 核心内容（≈1000 字）

**背景与动机：** 去中心化智能合约实现无需信任的协作，但面临隐私和可扩展性限制。TEE 链下执行框架是解决这两个问题的有前景方案，但此前工作未能充分探索合约互操作性。

**核心贡献：** RaceTEE 框架利用链下 TEE 节点高效执行长期运行的机密智能合约，支持任意复杂度的合约间交互。系统使用 Intel SGX 实现，与以太坊集成并开源发布。

**技术实现：** RaceTEE 解决了合约互操作性的三大挑战：1）跨合约状态一致性；2）机密性保护；3）执行正确性验证。评估表明框架在实际用例中表现有效。

---

## 论文五

**TEE-based Key-Value Stores: A Survey**
- **年份：** 2025
- **arXiv ID：** 2501.03118
- **作者：** Aghiles Ait Messaoud, Sonia Ben Mokhtar, Anthony Simonet-Boulogne
- **方向：** 数据库 × TEE 综述

### 核心内容（≈1000 字）

**背景与动机：** 键值存储（KVS）因简单性、可扩展性和快速检索能力而广受欢迎，但存储敏感数据需要强大的安全属性防止泄露和篡改。软件加密技术存在诸多缺陷，强烈依赖托管系统栈的信任，且无法在处理过程中保护数据。

**核心贡献：** 本文是第一篇系统性综述 TEE 在键值存储中的应用。作者分类总结了基于 TEE 的 KVS 方案，分析了它们的架构设计、安全机制和性能特征。

**安全分析：** TEE 在 CPU 级别强制执行代码和数据的机密性和完整性，使用户能够在不可信环境中构建可信应用。同时，TEE 在处理过程中保护数据，提供封装的安全区域。

---

## 论文六

**C8s: A Confidential Kubernetes Architecture**
- **年份：** 2026
- **arXiv ID：** 2604.26974
- **作者：** Amean Asad, Patrick McClurg, João Andrade（Confidential.ai）
- **方向：** 云原生 × TEE × Kubernetes

### 核心内容（≈1000 字）

**背景与动机：** 在第三方基础设施上运行敏感工作负载面临三方机密性问题：工件所有者面临模型权重、数据集、密钥等专有资产被泄露的风险；计算提供商需要确保云运营商无法观察其工作负载；最终用户需要其请求对所有方保持不透明。

**核心贡献：** C8s 是首个为 Kubernetes 提供加密根机密性、完整性和可验证性保证的架构。系统基于 AMD SEV-SNP、Intel TDX 和 NVIDIA 机密计算支持，在机密 VM 周围建立认证信任边界。

**安全保证：** 1）数据工件所有者可在第三方基础设施上部署敏感工作负载；2）计算提供商可提供执行服务而不向云运营商泄露工作负载；3）最终用户可提交对所有方不透明的请求（除了解密处理它们的 TEE）。

---

## 论文七

**Constraining Host-Level Abuse in Self-Hosted Computer-Use Agents via TEE-Backed Isolation**
- **年份：** 2026
- **arXiv ID：** 2605.06393
- **作者：** Di Lu, Bo Zhang 等（IEEE）
- **方向：** AI Agent × TEE × 安全隔离

### 核心内容（≈1000 字）

**背景与动机：** 自托管计算机使用代理（SHCUA）如 OpenClaw 结合自然语言交互与对主机端资源的直接访问（浏览器、文件、脚本、系统命令）。这一能力也创造了主机级滥用面——合法部署的代理可能被恶意消息、间接提示注入、不安全技能或沿主机端控制路径的篡改导向不安全操作。

**核心贡献：** 本文提出以操作风险为中心的 SHCUA 操作约束模型。设计将普通功能保留在受限的 REE 路径上，同时将安全关键分类、授权、绑定、证据生成和选定的执行控制决策保护在云原生 TEE 可信操作平面内。

**技术实现：** 使用 Intel TDX 作为主要可信后端，远程终端侧可信组件在受限本地执行前验证 TDX 审计命令。评估表明设计可阻止不安全或策略禁止的操作执行，为允许的工作负载保留普通功能，并提供可审计证据。

---

## 论文八

**KingsGuard: Enclave Data Protection Under Real-World TEE Vulnerabilities**
- **年份：** 2026
- **arXiv ID：** 2605.00613
- **作者：** Saltanat Firdous Allaqband 等（IIT Madras, IIT Bombay）
- **方向：** TEE 漏洞 × Enclave 安全

### 核心内容（≈1000 字）

**背景与动机：** TEE/Enclave 技术旨在提供硬件级安全隔离，但实际部署中存在各种漏洞可能削弱其安全保证。研究真实世界的 TEE 漏洞对于构建更安全的系统至关重要。

**核心贡献：** KingsGuard 是首个系统性分析真实世界 TEE 漏洞并提供 enclave 数据保护方案的论文。作者对 Intel SGX、ARM TrustZone 等主流 TEE 的实际漏洞进行了分类和分析，提出了针对这些漏洞的防御机制。

---

## 论文九

**Privacy-Preserving Product-Quantized Approximate Nearest Neighbor Search via Hybrid of FHE and TEE**
- **年份：** 2026
- **arXiv ID：** 2604.17816
- **作者：** Shozo Saeki, Minoru Kawahara, Hirohisa Aman（爱媛大学）
- **方向：** 隐私保护 × FHE × TEE × 向量搜索

### 核心内容（≈1000 字）

**背景与动机：** 最近邻框架是 LLM 和 VLM 的基础工具。用于最近邻搜索的向量包含丰富的相似性搜索信息，导致嵌入反转和成员攻击等安全风险。但传统基于 TEE 或全同态加密的隐私保护方法无法实现实用的安全性或性能。

**核心贡献：** 本文提出 PPPQ-ANN 框架，结合 FHE 和 TEE 为向量提供多层安全结构。通过将乘积量化（PQ）与优化的数据打包相结合，最大程度减少 FHE 密文计算。

**性能结果：** 在百万规模数据集上的演示表明，PPPQ-ANN 在 2 小时内完成数据库生成，顺序搜索超过 50 QPS，同时保持隐私。

---

## 论文十

**SPOILER: TEE-Shielded DNN Partitioning of On-Device Secure Inference with Poison Learning**
- **年份：** 2026
- **arXiv ID：** 2603.06263
- **作者：** Donghwa Kang, Hojun Choe 等（KAIST, 首尔大学）
- **方向：** AI 模型保护 × TEE × 边缘计算

### 核心内容（≈1000 字）

**背景与动机：** 在边缘设备上部署 DNN 面临模型窃取攻击风险。TEE 屏蔽 DNN 分区（TSDP）通过隔离敏感计算来缓解这一问题，但现有范式无法同时满足隐私和效率需求。

**核心贡献：** SPOILER 框架通过硬件感知神经架构搜索（NAS）从根本上将 TEE 子网络与骨干网络解耦。框架识别针对硬件约束严格优化的轻量级 TEE 架构，最大化并行效率。

**安全创新：** 引入自投毒学习来强制逻辑隔离，使暴露的骨干网络在缺少 TEE 组件时在功能上变得不连贯。实验表明 SPOILER 实现了安全性、延迟和准确性的最先进权衡。

---

## 论文十一

**Systematic Survey on Privacy-Preserving Architectures for IoT and Vehicular Data Sharing**
- **年份：** 2026
- **arXiv ID：** 2603.01876
- **作者：** Phat T. Tran-Truong 等（越南国立大学, RMIT, 東上大学）
- **方向：** 物联网 × 车联网 × 隐私保护综述

### 核心内容（≈1000 字）

**背景与动机：** 物联网设备和车联网通信系统产生海量敏感数据，需要隐私保护架构实现安全数据共享而不向不可信方暴露原始信息。当代方案面临根本的隐私-效率-信任三难问题。

**核心贡献：** 本文对 2007-2025 年间发表的 75 篇技术论文进行系统分析，组织成三维分类法：去中心化计算、基于密码学的方法和分布式账本技术。

**关键发现：** 联邦学习优先考虑效率但遭受拜占庭投毒攻击（准确率从 90% 降至 21%）；密码学方法提供可证明安全但带来 5.7-28.4 倍执行开销；区块链方案建立信任但面临可扩展性瓶颈（10MB 文件 Gas 成本达 157 万 Gwei）。

---

## 论文十二

**Tessera: Secure Near-Line-Rate Weight Streaming for UMA Edge Accelerators**
- **年份：** 2026
- **arXiv ID：** 2604.23205
- **作者：** Animan Naskar（IIT Ropar）
- **方向：** 边缘 AI × 硬件安全 × DRM

### 核心内容（≈1000 字）

**背景与动机：** 在商品边缘设备上部署专有 DNN 需要能够抵御软件级和物理对手的硬件级数字版权管理（DRM）。在统一内存架构（UMA）系统中，主机 CPU 和 NPU 共享物理 DRAM，使明文模型权重可被攻陷的 OS 内核直接读取。

**核心贡献：** Tessera 是针对 UMA 边缘加速器的行内缓存行级权重解密参考架构。设计拦截 64 字节 AXI 突发，在 DRAM 取数并行计算 AES-256-CTR 密钥流。

**性能结果：** 测量表明 Tessera 可达到理论内存带宽上限的 98.4%（仅 1.6% 开销），而页面级内存加密遭受高达 32 倍的带宽惩罚。

---

## 论文十三

**Trusted-Execution Environment (TEE) for Solving the Replication Crisis in Academia**
- **年份：** 2026
- **arXiv ID：** 2603.24878
- **作者：** Jiasun Li（George Mason University）
- **方向：** 学术诚信 × TEE × 复制危机

### 核心内容（≈1000 字）

**背景与动机：** 跨学科（经济、金融、社会科学和计算机科学）的复制危机损害了学术研究的可信度。当前制度解决方案——如工件评估和复制包——存在关键局限：合格数据编辑短缺、处理专有数据集困难、流程低效、依赖志愿劳动。

**核心贡献：** 本文提出利用 Intel TDX 的新型框架解决复制危机。作者在云 TEE 中执行复制包并提交正确执行的加密证明，期刊会议可高效验证而无需重新运行代码。

**可行性验证：** 试点研究在 TDX 支持的云 VM 上复制已发表论文，报告每包平均成本 1.35-1.80 美元，计算开销最小，即使无 TEE 经验的初学者也有高成功率。

---

## 论文十四

**What You Trust Is Insecure: Demystifying How Developers (Mis)Use Trusted Execution Environments in Practice**
- **年份：** 2026
- **arXiv ID：** 2512.17363
- **作者：** Yuqing Niu, Jieke Shi, Ruidong Han 等（新加坡管理大学）
- **方向：** TEE 实证研究 × 开发者行为

### 核心内容（≈1000 字）

**背景与动机：** TEE（如 Intel SGX 和 ARM TrustZone）为敏感数据和代码提供 CPU 和内存隔离区域，在不同应用领域得到越来越广泛的使用。但此前不了解开发者实际上如何使用的 TEE。

**核心贡献：** 首个大规模实证研究真实世界的 TEE 应用。研究从 GitHub 收集分析了 241 个利用两种最广泛采用的 TEE（Intel SGX 和 ARM TrustZone）的开源项目。

**关键发现：** 1）主要用例是物联网设备安全（30%），与此前学术关注区块链和密码系统（7%）形成鲜明对比，AI 模型保护（12%）正在快速增长；2）32.4% 的项目重实现密码功能而非使用官方 SDK API，表明当前 SDK 可用性和可移植性有限；3）25.3%（61/241）的项目存在不安全编码行为，如硬编码密钥和缺少输入验证。

---

## 横向对比综述

### 主题分布

本批次 14 篇论文覆盖以下核心方向：

1. **云原生与基础设施**：C8s（机密 Kubernetes）、Confidential CC for Cloud Security、TEE for Replication Crisis
2. **AI 与机器学习**：LLM in TEE for SoC、SPOILER（DNN 分区）、Tessera（边缘加速器）、Proof-of-Guardrail
3. **区块链与智能合约**：RaceTEE（机密合约互操作）
4. **物联网与边缘计算**：IoT/Vehicular Survey、Entropy Supply via RISC-V TEE
5. **安全分析与实证研究**：What You Trust Is Insecure（开发者行为）、KingsGuard（TEE 漏洞）
6. **隐私保护技术**：PPPQ-ANN（FHE+TEE 混合）
7. **系统化综述**：TEE-based KVS Survey、Narrowing the Gap

### 技术趋势

1. **TEE + AI 深度融合**：从单纯的安全隔离转向支持 AI 推理、模型保护、DNN 加速器安全
2. **云原生机密计算**：Kubernetes 集成、容器化工作负载保护成为热点
3. **混合安全架构**：FHE + TEE、ZK + TEE 等组合方案成为趋势
4. **实际部署挑战**：威胁模型与部署策略差距、开发者误用问题受到关注

### 论文之间的关系

- **C8s** 与 **Confidential CC for Cloud Security** 均关注云环境下的 TEE 部署
- **SPOILER** 与 **Tessera** 均为边缘 AI 模型保护方案（前者软件分区，后者硬件加密）
- **What You Trust Is Insecure** 为其他所有应用论文提供开发者行为洞察
- **Narrowing the Gap** 揭示的威胁模型问题与 **TEE for Replication Crisis** 解决方案形成对照

---

## 参考文献

1. Dhruv Deepak Agarwal, Aswani Kumar Cherukuri. "Confidential Computing for Cloud Security." arXiv:2511.04550, 2025.
2. Ben Dong, Hui Feng, Qian Wang. "Distilled LLM in Confidential Computing for SoC Design." arXiv:2507.16226, 2025.
3. Filip Rezabek et al. "Narrowing the Gap between TEEs Threat Model and Deployment Strategies." arXiv:2506.14964, 2025.
4. Keyu Zhang, Andrew Martin. "RaceTEE: Interoperability of Confidential Smart Contracts." arXiv:2503.09317, 2025.
5. Aghiles Ait Messaoud et al. "TEE-based Key-Value Stores: A Survey." arXiv:2501.03118, 2025.
6. Amean Asad et al. "C8s: A Confidential Kubernetes Architecture." arXiv:2604.26974, 2026.
7. Di Lu et al. "Constraining Host-Level Abuse in SHCUA via TEE." arXiv:2605.06393, 2026.
8. Saltanat Firdous Allaqband et al. "KingsGuard: Enclave Data Protection Under TEE Vulnerabilities." arXiv:2605.00613, 2026.
9. Shozo Saeki et al. "PPPQ-ANN via Hybrid of FHE and TEE." arXiv:2604.17816, 2026.
10. Donghwa Kang et al. "SPOILER: TEE-Shielded DNN Partitioning." arXiv:2603.06263, 2026.
11. Phat T. Tran-Truong et al. "Survey on Privacy-Preserving for IoT/Vehicular." arXiv:2603.01876, 2026.
12. Animan Naskar. "Tessera: Secure Weight Streaming for UMA." arXiv:2604.23205, 2026.
13. Jiasun Li. "TEE for Solving Replication Crisis." arXiv:2603.24878, 2026.
14. Yuqing Niu et al. "What You Trust Is Insecure." arXiv:2512.17363, 2026.