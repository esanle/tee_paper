# TEE 论文集（2026-04-22 下载）

本目录包含本次从 arXiv 下载的 14 篇可信执行环境（TEE）相关论文。

## 论文列表

### 2025 年论文（5 篇）

1. **Abstraction of Trusted Execution Environments as the Missing Layer for Broad Confidential Computing Adoption: A Systematization of Knowledge**
   - 来源：arXiv:2512.22090
   - 作者：Quentin Michaud et al. (SAMOVAR/Télécom SudParis/Thales cortAIx Labs)
   - 摘要：本文对 TEE 作为机密计算的缺失层进行了系统化研究，分析了当前 TEE 部署的障碍，并提出抽象层设计以促进广泛采用。

2. **Amulet: Fast TEE-Shielded Inference for On-Device Model Protection**
   - 来源：arXiv:2511.13717
   - 摘要：提出 Amulet 方案，用于在 TEE 内实现快速、安全的设备端模型推理保护。

3. **Enhancing the Security of Rollup Sequencers using Decentrally Attested TEEs**
   - 来源：arXiv:2511.22317
   - 摘要：研究如何使用去中心化认证的 TEE 增强 Rollup 排序器的安全性。

4. **PDRIMA: Policy-Driven Runtime Integrity Measurement and Attestation Approach for ARM TrustZone-based TEE**
   - 来源：arXiv:2512.06500
   - 作者：Jingkai Mao, Xiaolin Chang
   - 摘要：提出 PDRIMA 方案，一种基于 ARM TrustZone TEE 的策略驱动运行时完整性测量与远程认证方法。

5. **TZ-LLM: Protecting On-Device Large Language Models with Arm TrustZone**
   - 来源：arXiv:2512.07495
   - 摘要：提出 TZ-LLM 方案，利用 Arm TrustZone 保护设备端大语言模型的安全。

### 2026 年论文（9 篇）

6. **Committee Configuration Optimization for Parallel Byzantine Consensus in a Trusted Execution Environment**
   - 来源：arXiv:2602.19450
   - 摘要：优化 TEE 环境下的拜占庭共识委员会配置，实现并行处理。

7. **Gyokuro: Source-assisted Private Membership Testing using Trusted Execution Environments**
   - 来源：arXiv:2602.11088
   - 摘要：提出 Gyokuro 方案，基于 TEE 实现源辅助的私有成员资格测试，延迟仅 7ms，吞吐量约 1400 请求/秒/核。

8. **HPCCFA: Leveraging Hardware Performance Counters for Control Flow Attestation**
   - 来源：arXiv:2603.14445
   - 作者：Claudius Pott, Luca Wilke, Jan Wichelmann, Thomas Eisenbarth
   - 摘要：提出 HPCCFA 方案，使用硬件性能计数器（HPC）实现 RISC-V Keystone 架构的 TEE 控制流认证。

9. **On Securing the Software Development Lifecycle in IoT RISC-V Trusted Execution Environments**
   - 来源：arXiv:2601.09273
   - 作者：Annika Wilde, Samira Briongos, Claudio Soriente, Ghassan Karame
   - 摘要：针对 IoT RISC-V TEE 的安全 Enclave 更新和迁移问题，提出安全工具包，状态连续性开销不足 1.5%。

10. **Red-Teaming Claude Opus and ChatGPT-based Security Advisors for Trusted Execution Environments**
    - 来源：arXiv:2603.24878
    - 作者：Kunal Mukherjee (Virginia Tech)
    - 摘要：对 Claude Opus 和 ChatGPT 作为 TEE 安全顾问进行红队测试，发现可迁移失败率达 12.02%，提出 LLM-in-the-loop 评估管道可减少 80.62% 失败。

11. **Ringmaster: How to juggle high-throughput host OS system calls from TrustZone TEEs**
    - 来源：arXiv:2603.17757
    - 作者：Richard Habeeb, Man-Ki Yoon, Hao Chen, Zhong Shao (Yale/NCSU)
    - 摘要：提出 Ringmaster 框架，让 TrustZone TEE 能异步访问 Linux io_uring 服务，树莓派上实现近 1GiB/s 数据吞吐量，开销仅 0-3%。

12. **The Real Menace of Cloning Attacks on SGX Applications**
    - 来源：arXiv:2603.23226
    - 作者：Samira Briongos, Ghassan Karame, Claudio Soriente, Annika Wilde
    - 摘要：系统性研究 Intel SGX 应用的克隆攻击，分析 72 个基于 SGX 的方案，发现约 20% 对克隆攻击不安全。

13. **TrEEStealer: Stealing Decision Trees via Enclave Side Channels**
    - 来源：arXiv:2603.29749
    - 摘要：提出 TrEEStealer 攻击，通过 Enclave 侧信道窃取决策树模型。

14. **Trusted-Execution Environment (TEE) for Solving the Replication Crisis in Academia**
    - 来源：arXiv:2603.29749（注意：与上一篇冲突，需核实）
    - 作者：Jiasun Li (George Mason University)
    - 摘要：利用 Intel TDX 等 TEE 技术解决学术界的可复现性危机，成本约 $1.35-$1.80/包。

15. **What You Trust Is Insecure: Demystifying How Developers (Mis)Use Trusted Execution Environments in Practice**
    - 来源：arXiv:2604.18716
    - 摘要：实证研究开发者实际使用 TEE 的方式，揭示常见的安全误用模式。

---

## 对比分析综述

本次下载的论文涵盖 TEE 领域的多个前沿方向，可以归纳为以下几类：

### 1. TEE 基础设施与抽象（3 篇）
Abstraction 论文对 TEE 机密计算的广泛采用障碍进行了系统化分析，是该方向少见的 SoK（Systematization of Knowledge）论文，对于理解 TEE 生态的全貌具有重要价值。

### 2. LLM 与 TEE 的结合（3 篇）
TZ-LLM、Amulet 和 Vulnerabilities 论文均关注 LLM 与 TEE 的交叉。TZ-LLM 和 Amulet 专注于如何在 TEE 内保护设备端 LLM；Red-Teaming 论文则反思了将 LLM 作为安全顾问的风险。 Vulnerabilities 论文揭示了部分 TEE 屏蔽的 LLM 推理存在的安全漏洞。这些论文反映了随着 LLM 部署从云端向边缘扩展，TEE 作为安全基础的必要性日益凸显。

### 3. 区块链与共识（2 篇）
Committee Configuration Optimization 和 Enhancing Security of Rollup Sequencers 研究 TEE 在区块链共识和 Layer 2 扩展方案中的应用。这两篇论文的思路相似——利用 TEE 的硬件信任来增强去中心化系统的安全性，但侧重点不同：前者关注拜占庭共识的委员会配置，后者关注 Rollup 排序器的安全。

### 4. 控制流认证与侧信道（2 篇）
HPCCFA 和 TrEEStealer 形成有趣对比：HPCCFA 探索如何利用硬件性能计数器来增强 TEE 的控制流认证能力，而 TrEEStealer 则反过来研究 Enclave 侧信道对决策树模型的威胁。这两篇论文共同揭示了 TEE 安全研究中攻守两端的动态。

### 5. 运行时完整性（2 篇）
PDRIMA 和 HPCCFA 都关注 TEE 的运行时完整性，但针对不同平台：PDRIMA 面向 ARM TrustZone，提出策略驱动的运行时完整性测量；HPCCFA 面向 RISC-V Keystone，利用硬件性能计数器实现控制流认证。两者都试图弥补传统安全启动只验证静态状态的缺陷。

### 6. 安全开发生态（2 篇）
What You Trust Is Insecure 和 On Securing the SDLC in IoT RISC-V TEE 都关注 TEE 的实际使用问题。前者通过实证研究揭示开发者的误用模式，后者则提出 IoT RISC-V TEE 的安全 Enclave 更新和迁移工具包。两者都指向 TEE 从理论安全到实际安全落地之间的鸿沟。

### 7. 隐私计算（1 篇）
Gyokuro 论文利用 TEE 实现源辅助的私有成员资格测试，在 7ms 延迟下达到约 1400 请求/秒/核的吞吐量，展示了 TEE 在隐私保护计算领域的应用潜力。

### 8. 学术诚信（1 篇）
TEE for Solving Replication Crisis 论文是唯一的跨学科研究，尝试用 TEE 技术解决学术界的可复现性危机，这一应用场景较为新颖。

### 9. 系统接口（1 篇）
Ringmaster 论文专注于解决 TEE 在时间敏感系统中的可用性问题，让 TrustZone 能异步访问不可信的 Linux 服务，同时保持安全性。这一研究填补了 TEE 在实时系统应用中的一项空白。

---

## 总结

本次下载的论文呈现以下趋势：

1. **LLM 与 TEE 的结合是 2025-2026 年的研究热点**，涉及模型保护、安全评估、漏洞分析等多个角度
2. **RISC-V TEE 的研究显著增加**，反映 RISC-V 在安全领域的发展
3. **开发者安全意识和安全开发生态**受到更多关注，How Developers Misuse 和 SDLC 论文都是例证
4. **区块链与 TEE 的结合**持续受到关注，特别是在 Layer 2 扩展方案中的应用

---

*下载时间：2026-04-22 17:13 UTC*
*论文来源：arXiv*
*共 14 篇 PDF*
