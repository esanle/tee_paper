# 2026-04-24 批次 TEE 论文总结

本目录收录了本次搜索下载的 7 篇可信执行环境（TEE）相关论文，涵盖匿名广播、安全聚合、密码货币合约执行、图神经网络隐私保护、LLM自动化移植等多个前沿方向。

---

## 📄 论文列表

| 序号 | 文件名 | 作者 / 机构 | 来源 |
|------|--------|------------|------|
| 1 | `2025 - ZIPNet - Low-bandwidth anonymous broadcast from (dis)Trusted Execution Environments.pdf` | Rosenberg et al. (UMD, Yale, Tsinghua, Purdue) | PoPETs 2025 |
| 2 | `2025 - TEEMS - A Trusted Execution Environment based Metadata-protected Messaging System.pdf` | Sasy, Johnson, Goldberg (CISPA, US Naval Lab, Waterloo) | PoPETs 2025 |
| 3 | `2025 - Auntie - Unobservable Contracts from Zerocash and Trusted Execution Environments.pdf` | Cinal (NASK) | IACR ePrint 2025 |
| 4 | `2025 - Automated TEE Adaptation with LLMs - Identifying, Transforming, and Porting Sensitive Functions in Programs.pdf` | Han et al. (SMU, Alberta, UOW) | arXiv 2025 |
| 5 | `2025 - Graph in the Vault - Protecting Edge GNN Inference with Trusted Execution Environment.pdf` | Ding et al. (Northeastern) | arXiv 2025 |
| 6 | `2025 - Practical Secure Aggregation by Combining Cryptography and Trusted Execution Environments.pdf` | de Laage et al. (Neuchâtel, Bern) | ACM DEBS 2025 |
| 7 | `2025 - Verification of Lightning Network Channel Balances with Trusted Execution Environments (TEE).pdf` | Singh et al. (Stillmark, IBEX, Hoseki) | arXiv 2025 |

---

## 📝 论文摘要

### 1. ZIPNet — 低带宽匿名广播 (PoPETs 2025)

**作者**: Michael Rosenberg, Maurice Shih, Zhenyu Zhao, Rui Wang, Ian Miers, Fan Zhang  
**出处**: Proceedings on Privacy Enhancing Technologies 2025(2), 211–225

ZIPNet 旨在解决匿名广播频道（ABC）在低带宽场景下的服务器成本过高、cover流量代价大、难以吸引志愿者运营者等问题。传统 ABC 系统（如 Riposte、Blinder）依赖少量服务器，在隐私性和可扩展性之间存在根本矛盾。ZIPNet 提出三大设计目标：（1）通过最小化每台服务器的計算成本，扩展至数百台 anytrust 服务器；（2）将客户端消息聚合外包给不受信任的基础设施，从根本上降低服务器带宽成本；（3）支持廉价的 cover 流量生成和处理。

技术层面，ZIPNet 利用 TEE 实现了一个分布式匿名广播系统，通过新颖的路由协议在多个服务器间分配负载，同时保证消息的隐私性。论文详细分析了"匿名三难困境"——强匿名性、低延迟、低带宽三者不可兼得，而 TEE 的引入可以有效缓解服务器端资源瓶颈。评估表明，ZIPNet 在保持强匿名性（anytrust 模型）的同时，显著降低了运营成本，使得志愿者运营成为可能。ZIPNet 是 TEE 在匿名通信领域的创新应用，其贡献在于将服务器端的计算和带宽开销降低至可实用水平。

---

### 2. TEEMS — 基于 TEE 的元数据保护消息系统 (PoPETs 2025)

**作者**: Sajin Sasy, Aaron Johnson, Ian Goldberg  
**出处**: Proceedings on Privacy Enhancing Technologies 2025(4), 56–75

TEEMS 解决了在线消息系统中元数据泄露这一核心难题。虽然 E2EE 加密可以保护通信内容，但元数据（谁与谁通信、何时通信、频率如何）仍然被广泛泄露。过去的四十年里，研究者提出了多种元数据保护通信系统（MPCS），但没有一种能同时满足四个关键特性：（i）低延迟、（ii）高吞吐量、（iii）水平可扩展性、（iv）异步性。

TEEMS 首创性地利用 TEE 架构同时实现这四个特性。其核心创新包括：（1）设计了一种分布式"oblivious mailbox"结构，消息在 TEE 保护的服务器间以混淆方式路由存储；（2）提出了 TokenColumnRoute 和 IDColumnRoute 两个新颖的 oblivious 路由协议，基于先前 oblivious 分布式排序工作进行适配；（3）引入 ID 和 token 信道机制以克服先前设计的缺陷。评估显示 TEEMS 可在不到 1 秒内支持 220 个客户端进行元数据保护对话，在 205 核环境下吞吐量提升 18 倍。相比 mixnet（RIPOR 等）和反向 PIR（Sparta 等）方案，TEEMS 在延迟、吞吐量、可扩展性和异步性四个维度均实现了最优平衡。

---

### 3. Auntie — 结合 Zerocash 与 TEE 的不可观测合约 (IACR 2025)

**作者**: Adrian Cinal (NASK)  
**出处**: IACR Cryptology ePrint Archive 2025/1965

隐私导向的加密货币（如 Zerocash / Zcash）仅支持直接转账，无法执行复杂合约；而 Bitcoin/Ethereum 虽然支持智能合约，却无法保证隐私且面临抢先交易和矿工贿赂攻击。Auntie 创新性地将 Zerocash 的隐私保证与 TEE 的可验证性结合，构建了一个公平、去中心化且完全不可观测的合约执行框架。

具体而言，Auntie 实现了以下四个核心安全属性：（1）**不可观测性**——合约执行对网络完全不可见，外部观察者无法区分已执行和未执行账本；（2）**匿名性**——相互不信任的合约方互相保持匿名，单次或重复交互均不可链接；（3）**保密性**——合约方的输入输出（包括余额变动）对彼此保密；（4）**公平终止**——合约结果原子化地与链上资金变动绑定，并立即抵抗抢先交易和矿工贿赂攻击。Auntie 仅依赖 Zerocash 内置的（认证）加密算法，无需额外零知识证明或 MPC，实现极轻量级构造。论文还讨论了现有 TEE 技术（如 Intel SGX）的安全局限性及其应对策略，对 TEE+隐私币的混合架构具有重要参考价值。

---

### 4. AutoTEE — LLM 驱动的自动化 TEE 适配 (arXiv 2025)

**作者**: Ruidong Han, Zhou Yang, Chengyan Ma, Ye Liu, Yuqing Niu, Siqi Ma, Debin Gao, David Lo  
**出处**: arXiv:2502.13379

AutoTEE 是首个利用大语言模型（LLM）自动将程序中的敏感函数迁移至 TEE 保护区域的研究工作。TEE 虽能提供强安全隔离，但将现有程序适配到 TEE 环境需要深厚的领域知识（识别哪些函数涉及加密等敏感操作）和大量人工干预。AutoTEE 旨在最小化开发者负担，实现自动化流程。

AutoTEE 的工作流程包括四个关键步骤：（1）**敏感函数识别**——对 Java/Python 程序生成 AST，提取叶子函数（不调用其他用户定义函数的函数），LLM 判断是否包含敏感操作（加密、序列化等）；（2）**代码转换**——LLM 将识别出的敏感函数转换为功能等价的 TEE 原生代码实现；（3）**功能等效性验证**——通过测试输入生成和覆盖率分析验证转换后代码的正确性，采用 ReAct 策略迭代改进；（4）**TEE 集成**——通过 port-based 通信机制将原函数替换为对 TEE 保护版本的远程调用。AutoTEE 基于 68 个代码仓库手工构建了 385 个敏感函数的基准数据集，在 GPT-4o 下 Java 敏感函数识别 F1 达 0.94，转换成功率达 91.8%（Java）和 84.3%（Python）。

---

### 5. GNNVault — 基于 TEE 的边缘图神经网络安全推理 (arXiv 2025)

**作者**: Ruyi Ding, Tianhong Xu, Aidong Adam Ding, Yunsi Fei (Northeastern University)  
**出处**: arXiv:2502.15012

GNNVault 是首个专门针对图神经网络（GNN）安全部署的 TEE 框架。随着边缘 AI 的普及，在设备上本地运行 GNN 的需求日益增长（社区发现、推荐系统等），但本地推理面临两大安全威胁：模型 IP（权重参数）盗窃和图数据隐私泄露（如成员推断攻击、边盗窃攻击）。

GNNVault 核心创新在于"先分割再训练"（partition-before-training）策略：将 GNN 模型分为公共主干（public backbone）和私有修正器（private GNN rectifier）。公共主干计算密集但精度有限，在不受信任环境中用替代图训练；私有修正器利用真实私有图结构对主干输出进行校正，设计为极小模型存放于 TEE 内部，从而同时保护关键模型参数和私有边信息。由于 GNN 的消息传递机制需要访问完整图结构（节点特征和邻接矩阵），而 TEE 内存受限，论文提出了多种主干-修正器通信方案并评估其性能开销。基于 Intel SGX 的实际系统实现表明，GNNVault 仅引入微小推理开销（<2%精度损失），即可有效抵御状态-of-the-art 边盗窃攻击。

---

### 6. Practical Secure Aggregation — 密码学与 TEE 的安全聚合混合架构 (ACM DEBS 2025)

**作者**: Romain de Laage, Peterson Yuhala, François-Xavier Wicht, Pascal Felber, Christian Cachin, Valerio Schiavoni  
**出处**: ACM DEBS 2025

安全聚合（Secure Aggregation）是隐私保护计算的核心协议，使多方能在不泄露各自私有输入的前提下协作计算聚合值。纯密码学方法（如全同态加密 FHE）安全性强但计算开销巨大；TEE 提供近原生速度但受限于硬件可用性和信任假设。论文系统性地探索了将两者结合的混合架构，分析不同配置下的安全-性能权衡。

论文贡献包括：（1）对多种硬件/软件混合安全聚合架构的全面探索；（2）在不同参与方数量和数据规模下的详细性能评估；（3）各方案的安全性与性能权衡分析。论文考虑了包括阈值同态加密、秘密共享、TEE 外包等多种组合方案，为实际部署提供了系统性的参考框架，对隐私保护数据分析、联邦学习等应用场景具有直接指导意义。

---

### 7. Lightning Network Channel Balance Verification — 基于 TEE 的 LN 余额验证 (arXiv 2025)

**作者**: Vikash Singh, Barrett Little, Philip Hayes, Max Fang, Matthew Khanzadeh, Alyse Killeen, Sam Abbassi  
**出处**: arXiv:2512.12095

闪电网络（LN）的支付通道余额本质上是私密信息，但审计员、流动性服务提供商等外部实体需要可验证的储备证明来评估风险。论文提出了一种结合 TEE 与零知识传输层安全（zkTLS）的 LN 通道余额验证方法，提供硬件级别的完整性保证。

方案核心是将节点的余额报告软件运行在 TEE 中，生成远程证明引文（remote attestation quote）来证明软件完整性，再通过 zkTLS（TLSNotary 协议）确保引文传递的真实性。论文还提出了"热证明"（Hot Proofs，通过 TEE 生成用于速度优先的可验证声明）和"冷证明"（Cold Proofs，链上结算作为最终仲裁）的区分，讨论了硬件漏洞、第三方 API 隐私泄露和围界操作性能开销等关键安全考量。相较于基线的支付探测和纯软件 API 报告，该框架在信任模型上实现了质的飞跃，是 TEE 在区块链(layer-2)领域的创新应用。

---

## 🔄 横向对比与综述

本次下载的 7 篇论文涵盖了 TEE 技术在隐私通信（ZIPNet、TEEMS）、密码货币（Auntie、Lightning Verification）、隐私保护机器学习（GNNVault、AutoTEE、Secure Aggregation）三大应用场景，反映了 2025 年 TEE 研究的核心趋势。

**应用领域对比：**

| 论文 | 应用场景 | TEE 角色 | 核心价值 |
|------|---------|---------|---------|
| ZIPNet | 匿名通信 | 服务器端隐私路由 | 降低 anytrust 服务器成本 |
| TEEMS | 元数据保护消息 | oblivious mailbox | 兼顾低延迟+高吞吐+可扩展+异步 |
| Auntie | 隐私币合约 | 合约执行引擎 | 不可观测+匿名+公平终止 |
| AutoTEE | 代码安全移植 | 敏感代码隔离 | LLM 自动化识别与转换 |
| GNNVault | 边缘 AI/GNN | 模型+数据保护 | 参数和图结构双重隐私 |
| Secure Aggregation | 安全多方计算 | 聚合计算加速 | 混合密码学性能优化 |
| Lightning Verification | 区块链/L2 | 余额证明 | TEE+zkTLS 硬件级信任 |

**技术趋势观察：**

1. **TEE 与密码学深度融合**：Auntie 和 Secure Aggregation 均展示出将 TEE 与零知识证明、同态加密等纯密码学工具相结合的混合架构趋势，取长补短——TEE 补性能，密码学补信任假设。

2. **TEE 在隐私通信领域走向实用**：ZIPNet 和 TEEMS 均发表于隐私增强技术研讨会（PoPETs），表明 TEE 在匿名通信系统中的应用已获得顶级venue认可，不再是概念性探索，而是进入性能优化和实用化阶段。

3. **AI+TEE 交叉创新**：AutoTEE 代表了 LLM 在系统安全领域的开创性应用，将代码分析和转换过程自动化，降低 TEE 技术的使用门槛；GNNVault 则展示了在边缘 AI 场景下 TEE 对图数据和模型参数的双重保护需求。

4. **信任模型多样化**：Lightning Verification 和 Auntie 均涉及对 TEE 硬件信任假设的反思——前者结合 zkTLS 构建传输层信任，后者讨论了现实 TEE 实现（如 SGX）的安全局限性并提出缓解方案。

**共性挑战：**

- **侧信道安全**：TEEMS 和 Auntie 均需正视 TEE 侧信道攻击风险，前者通过 oblivious 协议缓解，后者需要 TEE 实现本身的安全性保障。
- **内存受限**：GNNVault 明确指出 TEE 内存容量有限与 GNN 图数据存储需求之间的矛盾，提出 partition 策略作为解决方案。
- **自动化门槛**：AutoTEE 的出现正是为了解决 TEE 代码移植的人工成本问题，表明 TEE 技术的普及仍需大量工程努力。

---

## 📚 参考文献

本文涉及的 7 篇论文：

1. M. Rosenberg et al., "ZIPNet: Low-bandwidth anonymous broadcast from (dis)Trusted Execution Environments," *PoPETs* 2025(2), 211–225. DOI: `10.56553/popets-2025-0058`
2. S. Sasy, A. Johnson, I. Goldberg, "TEEMS: A Trusted Execution Environment based Metadata-protected Messaging System," *PoPETs* 2025(4), 56–75. DOI: `10.56553/popets-2025-0119`
3. A. Cinal, "Auntie: Unobservable Contracts from Zerocash and Trusted Execution Environments," *IACR Cryptol. ePrint Arch.* 2025/1965. DOI: `10.56553/iacr.2025/1965`
4. R. Han et al., "Automated TEE Adaptation with LLMs: Identifying, Transforming, and Porting Sensitive Functions in Programs," *arXiv:2502.13379*, 2025 (updated 2026).
5. R. Ding et al., "Graph in the Vault: Protecting Edge GNN Inference with Trusted Execution Environment," *arXiv:2502.15012*, 2025.
6. R. de Laage et al., "Practical Secure Aggregation by Combining Cryptography and Trusted Execution Environments," *ACM DEBS* 2025.
7. V. Singh et al., "Verification of Lightning Network Channel Balances with Trusted Execution Environments (TEE)," *arXiv:2512.12095*, 2025.

---

*生成时间：2026-04-24 | 由 OpenClaw AI 自动整理*
