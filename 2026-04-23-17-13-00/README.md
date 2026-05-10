# TEE 论文集（2026-04-23 下载）

本目录包含本次下载的 4 篇可信执行环境（TEE）相关论文。

## 论文列表

### 2025 年论文（3 篇）

1. **DITING: A Static Analyzer for Identifying Bad Partitioning Issues in TEE Applications**
   - 来源：arXiv:2502.15281
   - 作者：Chengyan Ma, Ruidong Han, Jieke Shi, Ye Liu, Yuqing Niu, Di Lu, Chuang Tian, Jianfeng Ma, Debin Gao, David Lo（新加坡管理大学、西安电子科技大学）
   - 会议：一般期刊论文（非顶会，但值得关注）
   - 摘要：本文发现 TEE 应用中存在"错误分区"（bad partitioning）漏洞——当正常世界（normal world）与 TEE 之间交换参数时（输入/输出/共享内存），若缺乏加密或边界检查等安全机制，会导致敏感数据泄漏或缓冲区溢出。作者提出了 DITING 工具，通过数据流分析检测这些参数是否违反三条安全规则，从而识别分区问题。该工具在包含 110 个测试用例的自建基准上达到 0.90 的 F1 分数。目前是首个针对 TEE 错误分区的自动化静态分析工具。

2. **Silentflow: Leveraging Trusted Execution for Resource-Limited MPC via Hardware-Algorithm Co-design**
   - 来源：arXiv:2508.13357
   - 作者：Zhuoran Li, Hanieh Totonchi Asl, Ebrahim Nouri, Yifei Cai, Danella Zhao（亚利桑那大学）
   - 会议：arXiv 2025（暂未确认发表 venue）
   - 摘要：安全多方计算（MPC）常用不经意传输（OT）实现隐私保护的机器学习推理，但在资源受限的 IoT 设备上 OT 生成是性能瓶颈。Silentflow 利用 TEE 通过硬件-算法协同设计消除 OT 生成中的通信开销。核心创新包括：内核融合（kernel fusion）提升并行度、Blocked On-chip eXpansion（BOX）优化内存访问模式、向量化批处理最大化内存带宽利用。在 Zynq-7000 SoC 上实现了最高 39.51 倍加速，ImageNet 推理比 Cryptflow2 和 Cheetah 分别快 4.62 倍和 3.95 倍。

3. **TEEBFT: Pricing the Security of Proof of Cloud**
   - 来源：arXiv:2510.26091
   - 作者：Alex Shamis, Matt Stephenson, Linfeng Zhou（Subzero Labs）
   - 会议：arXiv econ.TH 2025（经济学/安全交叉论文）
   - 摘要：区块链与外部系统交互时面临可信性问题，TEE 是一种有前景的解决方案。本文建立了一个成本-串通博弈模型，分析破坏数据中心执行保证（Data Center Execution Assurance）设计中 TEE 的攻击者激励。模型关注四个核心变量：(i) 成功串通的 K-of-n 阈值；(ii) 检测风险；(iii) 被检测后每个成员的处罚 Fi；(iv) 可提取的流动性奖励 ω。论文推导了理性串通条件和威慑阈值，标定结果表明协议可在约 1 万亿美元价值规模下达"串通无利可图"的设计边界。

### 2026 年论文（1 篇）

4. **SPARTA: A Secure, Confidential, and Verifiable Decision Support System**
   - 来源：arXiv:2509.02413
   - 作者：Edoardo Marangone, Eugenio Nerio Nemmi, Daniele Friolo, Giuseppe Ateniese, Ingo Weber, Claudio Di Ciccio（罗马大学、乔治梅森大学、慕尼黑工业大学、乌得勒支大学）
   - 会议：arXiv 2026（近期修订）
   - 摘要：协作式决策支持系统（DSS）需要同时满足四个属性：(i) 输入数据和决策逻辑对包括计算平台在内的所有参与方保密；(ii) 不暴露输入的前提下验证决策过程；(iii) 用户自定义决策规则并实施细粒度访问控制；(iv) 实际工作负载下的实用性能。现有方案无法同时满足。SPARTA（Secure Platform for Automated decision Rules via Trusted Applications）利用 TEE 解决这一"机密可验证决策支持问题"：将决策规则翻译为经过认证的软件对象部署在 TEE 内执行，决策数据加密存储在分布式文件系统，以公链作为公证层保证可追溯性和完整性，密钥通过 TEE 内 mutual attestation 生成的共享种子派生，消除中心化密钥管理单点故障。实验表明该方案可扩展且额外开销有限。

---

## 对比分析综述

本次 4 篇论文覆盖了 TEE 研究中较为独特且互补的四个方向：**静态分析**、**性能优化**、**经济安全建模**和**应用架构**，彼此之间形成了从工具→性能→激励→系统的完整研究链条。

### 一、从错误分区静态分析到可验证决策（DITING → SPARTA）

DITING 和 SPARTA 表面上分别关注安全工具和应用架构，但核心都指向 TEE 与正常世界之间的**数据交换接口安全**这一根本问题。DITING 指出当前 TEE 应用中交换参数（输入/输出/共享内存）时普遍存在"错误分区"——即在正常世界进行的边界检查不可信，缺乏独立验证。这一发现揭示了 TEE 安全的一个系统性盲点：开发者往往依赖正常世界的输入验证，但这些验证本身可能被恶意操控。

SPARTA 恰好回应了这一问题：它在 TEE 内使用经过认证的决策规则对象，并在 TEE 内派生密钥，使得"即使正常世界被攻破，攻击者也无法获取决策数据"。两个工作组合在一起，正好构成了"发现接口安全问题→在 TEE 内部重新设计安全数据处理"的完整链条。

从技术路线看，DITING 属于**防御性白盒检测**（静态数据流分析），SPARTA 属于**机密性保护架构设计**（TEE 内密钥派生 + 区块链公证）。两者共同强调：TEE 的安全不仅仅依赖硬件隔离，还需要对跨世界数据流进行系统性安全管理。

### 二、Silentflow 与 TEEBFT：从性能到激励的互补视角

Silentflow 和 TEEBFT 都关注 TEE 在**多参与者系统**中的实际可用性，但切入点完全不同：Silentflow 解决资源受限设备上 MPC 的计算瓶颈（OT 生成），通过 TEE 硬件-算法协同设计实现了 39 倍性能提升；TEEBFT 则建模了在更大规模经济激励下，TEE 提供商的串通威慑条件。

这两篇论文在研究尺度上形成互补：Silentflow 面向**边缘/IoT 场景**（资源受限，单设备），TEEBFT 面向**数据中心/区块链场景**（资源丰富，多方博弈）。两者都体现了 TEE 从"安全隔离工具"向"可编程信任基础设施"演进的趋势——Silentflow 把 TEE 用作加速器，TEEBFT 把 TEE 用作经济合约的锚点。

### 三、四篇论文的交叉关系与 TEE 研究趋势

综合来看，本次 4 篇论文反映了一个核心趋势：**TEE 研究正在从"如何保护 TEE 本身"向"如何在 TEE 之上构建安全系统"演进**。

- DITING 通过静态分析发现分区问题的系统性盲点，推动更严格的接口设计
- Silentflow 通过硬件-算法协同设计让 TEE 在资源受限场景下真正可用
- TEEBFT 通过经济模型证明：当设计合理时，TEE 可以保护万亿美金规模的价值
- SPARTA 展示了 TEE 与区块链结合的实用路径——在多参与方场景下同时满足机密性、可验证性和定制化

值得注意的是，这四篇论文中有三篇来自跨学科合作（经济学/安全/DSS），且两篇采用了形式化方法（博弈论、静态分析），反映了 TEE 研究日益成熟和多元化的趋势。

### 四、与前次下载论文的关系

前次下载的论文（2026-04-22）主要关注：LLM 与 TEE 的结合（TZ-LLM、Amulet、Vulnerabilities）、区块链共识（Committee Configuration、Enhancing Rollup）、控制流认证与侧信道（HPCCFA、TrEEStealer）。

本次的 DITING 与 HPCCFA 在方法论上有趣地互补：HPCCFA 利用硬件性能计数器进行控制流认证，DITING 则针对 TEE 的数据流接口进行静态分析——两者分别从"运行时行为监控"和"静态分区检查"两个维度加固 TEE。Silentflow 与 TZ-LLM/Amulet 都关注 LLM 隐私保护，但 Silentflow 聚焦 MPC 加速，而 TZ-LLM/Amulet 聚焦模型本身在 TEE 内的安全执行——技术路线不同但目标一致。TEEBFT 与 Committee Configuration Optimization 都研究共识场景，但 TEEBFT 从经济学视角建模激励，Committee Configuration 从系统视角优化委员会配置。

---

## 参考文献（交叉引用）

1. Chengyan Ma et al. "DITING: A Static Analyzer for Identifying Bad Partitioning Issues in TEE Applications." arXiv:2502.15281, 2025.
2. Zhuoran Li et al. "Silentflow: Leveraging Trusted Execution for Resource-Limited MPC via Hardware-Algorithm Co-design." arXiv:2508.13357, 2025.
3. Alex Shamis, Matt Stephenson, Linfeng Zhou. "TEEBFT: Pricing the Security of Proof of Cloud." arXiv:2510.26091, 2025.
4. Edoardo Marangone et al. "SPARTA: A Secure, Confidential, and Verifiable Decision Support System." arXiv:2509.02413, 2026.
5. Quentin Michaud et al. "Abstraction of Trusted Execution Environments as the Missing Layer for Broad Confidential Computing Adoption." arXiv:2512.22090, 2025.
6. Jingkai Mao, Xiaolin Chang. "PDRIMA: Policy-Driven Runtime Integrity Measurement and Attestation Approach for ARM TrustZone-based TEE." arXiv:2512.06500, 2025.
7. X Wang et al. "TZ-LLM: Protecting On-Device Large Language Models with Arm TrustZone." arXiv:2511.13717, 2025.
8. Richard Habeeb et al. "Ringmaster: How to juggle high-throughput host OS system calls from TrustZone TEEs." arXiv:2603.17757, 2026.
9. Samira Briongos et al. "The Real Menace of Cloning Attacks on SGX Applications." arXiv:2603.23226, 2026.
10. Claudius Pott et al. "HPCCFA: Leveraging Hardware Performance Counters for Control Flow Attestation." arXiv:2603.14445, 2026.
11. Kunal Mukherjee. "Red-Teaming Claude Opus and ChatGPT-based Security Advisors for Trusted Execution Environments." arXiv:2603.24878, 2026.
