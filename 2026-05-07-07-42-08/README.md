# 2025-05-07 TEE 论文下载

本目录收录本次从 arXiv 下载的 7 篇 TEE 相关论文（2025 年）。

## 目录内容

| # | 文件名 | 来源 |
|---|--------|------|
| 1 | Attestable Audits - Verifiable AI Safety Benchmarks Using Trusted Execution Environments | arXiv:2506.23706 |
| 2 | Attestable Builds - Compiling Verifiable Binaries on Untrusted Systems using Trusted Execution Environments | arXiv:2505.02521 |
| 3 | Automated TEE Adaptation with LLMs - Identifying, Transforming, and Porting Sensitive Functions in Programs | arXiv:2502.13379 |
| 4 | CyFence - Securing Cyber-physical Controllers Via Trusted Execution Environment | arXiv:2506.10638 |
| 5 | Graph in the Vault - Protecting Edge GNN Inference with Trusted Execution Environment | arXiv:2502.15012 |
| 6 | Practical Secure Aggregation by Combining Cryptography and Trusted Execution Environments | arXiv:2504.08325 |
| 7 | Verification of Lightning Network Channel Balances with Trusted Execution Environments (TEE) | arXiv:2512.12095 |

---

## 论文详解

### 1. Attestable Audits: Verifiable AI Safety Benchmarks Using Trusted Execution Environments

**作者**：Christoph Schnabl, Daniel Hugenroth, Bill Marino, Alastair R. Beresford（剑桥大学）
**来源**：arXiv:2506.23706，发表于 ICML 2025

**一句话摘要**：将 AI 安全评估基准运行在 TEE 可信执行环境中，使审计结果可验证且模型权重和数据集保密。

**核心贡献**：
- 提出 **Attestable Audits**（可审计评估），一个三层验证协议：审计方和模型提供方将模型、审计代码和数据集安全加载到硬件支持的 TEE 中，运行基准测试，然后将结果通过加密证明发布到公共注册表供用户验证。
- 使用 AWS Nitro Enclaves 原型验证可行性，相比 CPU 推理开销 2.2×、GPU 推理开销 21.7×。
- 解决 AI 治理框架中的核心挑战：当模型提供商不共享权重、审计方只与监管机构共享代码和数据、系统运行在不可信第三方基础设施上时，用户仍可验证是否在与合规 AI 系统交互。

**主要发现**：基准测试是评估大规模 AI 模型安全和合规性的关键工具，但现有基准缺乏可验证结果和对模型 IP 及基准数据集的保密性。TEEs 提供的机密计算（Confidential Computing）可以隔离执行并加密内存，同时利用完整性保证提供类似零知识证明的保证。

**相关工作**：该论文属于 AI 治理 + 机密计算交叉领域，引用了 Casper et al. 2024、Raji et al. 2020 等 AI 安全评估框架相关工作，以及 Chen et al. 2023 关于机密计算的论文。

---

### 2. Attestable Builds: Compiling Verifiable Binaries on Untrusted Systems using Trusted Execution Environments

**作者**：Daniel Hugenroth, Mario Lins, René Mayrhofer, Alastair R. Beresford（剑桥大学 & 林茨约翰内斯·开普勒大学）
**来源**：arXiv:2505.02521

**一句话摘要**：用现代 TEE 和沙盒构建容器实现从源代码到二进制制品的可信对应证明，无需对现有项目做重大修改。

**核心贡献**：
- 提出 **attestable builds**（可验证构建）新范式，解决不透明构建管道将源代码（可审计）和最终二进制制品（难以检查）之间的信任断开问题。
- 相比可复现构建需要大量修改现有构建配置和依赖项，attestable builds 只需最小化更改即可实现近乎即时的源到二进制对应验证。
- 开销很小（启动延迟 42 秒，构建时长增加 14%），可构建复杂项目如 LLVM Clang 而无需修改源代码和构建脚本。
- 正式建模并验证设计安全性，抵御资源充足的对手。

**背景**：2020 年 SolarWinds 攻击中，攻击者入侵公司构建服务器在更新中注入额外代码；2024 年 CVE-2024-3094 针对构建管道的复杂供应链攻击。Attestable builds 可在构建时验证制品确实来自特定的源代码快照。

---

### 3. Automated TEE Adaptation with LLMs: Identifying, Transforming, and Porting Sensitive Functions in Programs

**作者**：Ruidong Han, Zhou Yang, Chengyan Ma, Ye Liu, Yuqing Niu, Siqi Ma, Debin Gao, David Lo（新加坡管理大学、阿尔伯塔大学、卧龙岗大学）
**来源**：arXiv:2502.13379

**一句话摘要**：首个基于大语言模型（LLM）自动化识别、转换和移植程序中敏感函数到 TEE 的工具 AUTOTEE。

**核心贡献**：
- **AUTOTEE** 是首个 LLM 驱动的自动化 TEE 适配方案，可自动识别、转换和移植包含敏感操作的函数到 TEE，最小化开发者干预。
- 通过手动审查 68 个代码库构建基准数据集，包含 385 个符合转换条件的有敏感函数；在 Java 上平均 F1 0.94，Python 上 0.87。
- 使用 GPT-4o 转换成功率为 Java 91.8%、Python 84.3%。

**为什么难**： adaptation 现有程序到 TEE 面临两大挑战：(1) 安全关键代码隔离要求高，需要深度专业知识；(2) TEE 约束执行环境，大多数 TEE 设计运行为低级代码（C/Rust），而高级语言（Java/Python）需要专用运行时支持。

---

### 4. CyFence: Securing Cyber-physical Controllers Via Trusted Execution Environment

**作者**：Stefano Longari, Alessandro Pozone, Jessica Leoni, Mario Polino, Michele Carminati, Mara Tanelli, Stefano Zanero（米兰理工大学）
**来源**：arXiv:2506.10638

**一句话摘要**：利用 TEE 对网络物理系统（CPS）执行语义检查，在不显著增加计算开销的情况下检测控制回路中的异常行为。

**核心贡献**：
- 提出 **CyFence**，一种利用 TEE 执行语义检查的新型软件架构，用于检测基于控制回路的系统中的异常行为。
- 关注 CPS 的网络物理特性（而非常规网络安全方案），确认系统按预期运行。
- 在真实主动制动数字控制器上评估，证明可以减轻不同类型攻击且计算开销可忽略不计。
- 填补了自动驾驶和工业机器人等安全关键控制系统中 TEE 应用的空白——这些系统对实时性有严格要求，现有方案（高度耗时）无法满足。

**背景**：CPS（工业机器人、车辆控制系统等）正变得越来越互联，在提供新功能的同时也扩大了攻击面。但大多数现有方案来自嵌入式系统或 IoT 安全领域，使用 HSM 认证加密功能、安全启动确保固件真实性，无法满足严格实时要求。

---

### 5. Graph in the Vault: Protecting Edge GNN Inference with Trusted Execution Environment

**作者**：Ruyi Ding, Tianhong Xu, Aidong Adam Ding, Yunsi Fei（美国东北大学）
**来源**：arXiv:2502.15012

**一句话摘要**：提出 GNNVault，首个基于 TEE 的安全图神经网络（GNN）边缘推理框架，通过"划分-后-训练"策略保护模型参数和图数据隐私。

**核心贡献**：
- **GNNVault** 是首个专门为 GNN 设计的安全部署框架，采用"划分-后训练"策略：公共骨干网（计算密集但不准确，用替代图训练，部署在不可信环境）和私有 GNN 修正器（利用真实私有图结构修正节点嵌入，设计得更小，驻留在 TEE 内）。
- 在 Intel SGX 上实现真实部署，GNNVault 可防范最新链接攻击（link stealing attacks），同时精度损失小于 2%。
- 同时保护模型 IP（超参数、训练参数）和数据隐私（节点特征、邻接矩阵等图结构信息），解决了现有 TEE 安全方案主要针对计算机视觉和 LLM 数据集、不适用于 GNN 的问题。

**为什么难**：GNN 操作要求根据邻居节点信息更新图节点表示，整个图数据在推理时必须本地存储；同时 TEE 内存有限，大图需要大量存储。

---

### 6. Practical Secure Aggregation by Combining Cryptography and Trusted Execution Environments

**作者**：Romain de Laage, Peterson Yuhala, François-Xavier Wicht, Pascal Felber, Christian Cachin, Valerio Schiavoni（纽沙德尔大学、伯尔尼大学）
**来源**：arXiv:2504.08325

**一句话摘要**：将密码学技术与 TEE 混合，提出多种安全聚合架构，在安全和性能之间取得实际权衡。

**核心贡献**：
- 指出安全聚合面临的主要挑战：纯密码学技术（如全同态加密 FHE）计算开销大，使得安全聚合协议不切实际；TEE 硬件方案速度快但可能被认为相对较新。
- 提出多种整合密码学和 TEE 的安全聚合架构，分析安全性与性能之间的权衡。
- 应用场景：联邦学习（federated learning）、安全电子投票、隐私保护拍卖、隐私保护数据分析。

**背景**：现代组织需要第三方数据做决策，但 GDPR、CCPA、HIPAA 等数据隐私法规限制数据共享。安全聚合是一种密码学协议，允许多方计算聚合值同时保护各自输入的隐私。

---

### 7. Verification of Lightning Network Channel Balances with Trusted Execution Environments (TEE)

**作者**：Vikash Singh, Barrett Little, Philip Hayes, Max Fang, Matthew Khanzadeh, Alyse Killeen, Sam Abbassi（Stillmark, IBEX Mercado, Hoseki, Lexe）
**来源**：arXiv:2512.12095

**一句话摘要**：结合 TEE 和 zkTLS 提出 Lightning Network 通道余额可验证性框架，区分"热证明"（TEE 生成，快速）和"冷证明"（链上结算，最终裁决）。

**核心贡献**：
- 核心贡献：将 TEE 与 zkTLS（零知识传输层安全）结合，为 Lightning Network 通道余额验证提供硬件支持的强保证。
- 运行 TEE 内的余额报告软件生成远程证明引证（attestation quote）证明软件完整性；通过 API 提供服务；使用 zkTLS 证明传递的真实性。
- 区分"热证明"（Hot Proofs，通过 TEE 生成以保证速度和运营连续性）和"冷证明"（Cold Proofs，链上结算作为最终裁决）。
- 分析了硬件漏洞对 TEE 的影响、第三方 API 隐私泄露风险以及飞地操作性能开销。

**背景**：LN 隐私设计是双刃剑：用户受益但外部实体（审计方、流动性市场、交易对手方）需要可验证的节点通道储备证明。之前的 TEE-LN 系统（Teechan、Teechain）专注于通道建立，本文专注于可验证余额证明。

---

## 综合对比分析

本批次 7 篇论文覆盖了 TEE 在 AI 安全、软件供应链、自动化、 CPS 控制、金融支付和隐私保护等多个领域的创新应用，反映了 2025 年 TEE 研究的几个重要趋势：

### 趋势一：TEE 与 AI 安全评估深度融合

**Attestable Audits** 和 **Graph in the Vault** 都展示了 TEE 在 AI 领域的新兴应用场景。Attestable Audits 将 TEE 用于 AI 模型的第三方安全评估，解决了 AI 治理框架中"可验证性"的核心挑战；Graph in the Vault 则专门针对边缘 GNN 部署中的模型 IP 和数据隐私保护。两篇论文共同指向一个趋势：随着 AI 模型部署从云端向边缘和多方协作场景扩展，TEE 正在成为保护模型权重、推理过程和评估结果的核心基础设施。

### 趋势二：TEE 降低开发者门槛

**AutoTEE** 论文明确指出"尽管 TEE 提供了强大保护，将现有程序适配到 TEE 仍然需要深度领域知识和大量手动工作"。AutoTEE 用 LLM 自动化敏感函数识别和 TEE 移植，F1 达 0.94（Java），成功率达 91.8%。这反映了 TEE 生态系统中一个关键瓶颈——可用性——正在被大语言模型工具化解决。未来可能有更多研究探索如何用 AI 降低 TEE 开发门槛。

### 趋势三：软件供应链安全成为 TEE 热点

**Attestable Builds** 针对的是软件供应链安全中最难的问题之一：如何确保最终分发的二进制制品确实来自特定版本的源代码。传统可复现构建需要大量项目配置修改，而 attestable builds 利用 TEE 和沙盒构建容器实现最小侵入性的即时验证。SolarWinds 和 CVE-2024-3094 等供应链攻击事件的频发推动了这一领域的研究热度。

### 趋势四：CPS 控制系统的 TEE 实用化

**CyFence** 代表了 TEE 在网络物理系统安全中的实用化方向，其核心洞察是"大多数现有防御专注于安全而非网络物理特性"。CyFence 的创新在于利用 CPS 的物理特性（控制回路的预期行为）作为安全检查的基础，而 TEE 只负责保护语义检查代码的执行。这篇文章代表了 TEE 从通用安全方案向领域定制化安全方案演化的趋势。

### 趋势五：密码学与 TEE 的混合架构

**Practical Secure Aggregation** 系统性地分析了纯密码学方案（全同态加密）和纯 TEE 方案的各自优缺点，提出多种混合架构。这一研究路径很有价值，因为它不假设一种技术能解决所有问题，而是为不同信任模型和性能要求的场景提供适配的混合方案。这反映了 TEE 研究社区对实用主义的追求——在现实部署中，安全、性能和可用性往往需要权衡。

### 趋势六：TEE 在去中心化金融中的应用深化

**Verification of Lightning Network Channel Balances** 延续了 Teechan/Teechain 的研究路线，但聚焦于更细粒度的余额验证问题，而非通道建立。这篇论文对"热证明"（TEE 生成，快速）和"冷证明"（链上结算，最终）的区分非常有洞见——它认识到在实际金融系统中，速度和最终确定性之间存在天然的张力，而 TEE 为这一权衡提供了新的技术选项。

### 安全考量汇总

所有 7 篇论文都提及了 TEE 固有的安全考量，包括：
- **硬件侧信道攻击**：多篇论文提及 TEE 硬件漏洞可能影响安全性（如 CacheZoom、SGX-Step 等）
- **远程证明的复杂性**：Attestable Builds 等强调需要验证整个软件栈而非单个 enclave
- **信任模型假设**：所有方案都假设 TEE 硬件制造商本身可信
- **隐私泄露风险**：Lightning 论文特别讨论了向第三方 API 泄露余额信息的风险

---

## 下载说明

- 下载时间：2026-05-07
- 来源：arXiv（所有论文均可在 arXiv 免费获取）
- 命名格式：`年份 - 标题.pdf`
- 所有文件均已通过 MD5 哈希去重检查，无重复文件
