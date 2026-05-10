# 可信执行环境 (TEE) 论文综述

**下载时间**: 2026-05-05 19:37 UTC  
**来源**: arXiv 2025年相关论文

---

## 目录

本次下载共4篇论文，均来自arXiv，聚焦可信执行环境在隐私计算、AI、区块链等前沿应用。

---

## 论文详解

### 1. Abstraction of Trusted Execution Environments as the Missing Layer for Broad Confidential Computing Adoption: A Systematization of Knowledge
**年份**: 2025  
**arXiv**: [2512.22090](https://arxiv.org/abs/2512.22090)  
**作者**: Quentin Michaud, Sara Ramezanian, Dhouha Ayed, Olivier Levillain, Joaquin Garcia-Alfaro  
**机构**: Télécom SudParis, Lund University, Karlstad University, Thales cortAIx Labs  
**出处**: arXiv:2512.22090v1 [cs.CR] (2025年12月26日)

**摘要**:
本文是关于TEE抽象层的系统化知识综述。TEEs（如Intel SGX、AMD SEV、ARM TrustZone等）保护敏感代码和数据免受操作系统、特权软件的攻击。不同TEE解决方案各具特性，抽象层的目标是统一生态系统，让应用开发者和系统管理员能够广泛高效地利用机密计算。本文首先概述了主流TEE技术，描述并总结了各TEE生态系统，根据主要设计选择进行分类。随后，作者提出了聚焦于不同抽象层的系统化知识，描述了每种设计选择背后的底层技术、抽象层的工作原理和特性。研究发现现有抽象层解决方案存在改进空间，并指出WebAssembly是支持最广泛功能的有前景方向。最后讨论了未来研究方向，如抽象层如何演进并与机密计算生态系统集成。

**关键贡献**:
- 对主流TEE技术（Intel SGX、AMD SEV、ARM TrustZone、RISC-V Keystone等）进行了全面分类
- 系统化分析了TEE抽象层的技术栈，包括语言运行时（WebAssembly、Rust）、SDK层、attestation接口
- 揭示了当前抽象层的不足，如跨平台兼容性、性能开销、信任模型的复杂性
- 指出WebAssembly作为TEE抽象层的优势：语言无关性、隔离执行、便携性

---

### 2. Optimistic TEE-Rollups: A Hybrid Architecture for Scalable and Verifiable Generative AI Inference on Blockchain
**年份**: 2025  
**arXiv**: [2512.20176](https://arxiv.org/abs/2512.20176)  
**作者**: Aaron Chana, Alex Dinga, Frank Chen, Alan Wu, Bruce Zhang, Arther Tian  
**机构**: DGrid AI  
**出处**: arXiv:2512.20176v1 [cs.CR] (2025年12月23日)

**摘要**:
大型语言模型（LLM）集成到去中心化物理基础设施网络（DePIN）当前受制于"可验证性三难"——去中心化推理系统无法同时实现高计算完整性、低延迟和低成本。现有密码学方案（如ZKML）因超线性证明开销而对十亿参数模型不可行；optimistic方法（opML）因争议期过长而无法支持实时交互；而"质量证明"（PoQ）范式牺牲了密码学完整性，留下模型降级攻击的隐患。本文提出Optimistic TEE-Rollups（OTR），利用NVIDIA H100 Confidential Computing TEE提供亚秒级临时确定性，结合optimistic欺诈证明机制和随机ZK抽查来缓解硬件侧信道风险。定义了"高效归属证明"（PoEA）共识机制，将执行踪迹密码学绑定到硬件attestation，保证模型真实性。

**关键贡献**:
- 提出OTR混合验证协议，解决LLM推理在DePIN中的可验证性三难问题
- 利用TEE硬件作为"乐观假设"的信任基础，结合欺诈证明和ZK抽查实现系统性安全
- 定义PoEA共识机制，密码学绑定执行踪迹与硬件attestation
- 首个在区块链场景中结合TEE和optimistic rollup的实用方案

---

### 3. Securing Generative AI in Healthcare: A Zero-Trust Architecture Powered by Confidential Computing on Google Cloud
**年份**: 2025  
**作者**: Adaobi Amanna (Google Cloud), Ishana Shinde (Google Cloud)  
**出处**: arXiv (无明确编号，2025年)

**摘要**:
生成式AI在医疗领域的应用受制于传统框架无法解决的安全挑战，尤其是"数据在使用中"的安全缺口——敏感患者数据和专有AI模型在主动处理时暴露。本文提出机密零信任框架（CZF），将零信任架构的精细访问控制与机密计算的硬件强制数据隔离相结合。详细描述了在Google Cloud上实现CZF的多层架构蓝图，分析了其对抗现实威胁的有效性。CZF提供纵深防御架构，数据在TEE中使用时保持加密。远程attestation提供工作负载完整性的密码学证明，将合规从程序性操作转变为可验证的技术事实。

**关键贡献**:
- 提出Confidential Zero-Trust Framework (CZF)，结合ZTA和机密计算
- 针对医疗AI场景设计"数据在使用中"的保护方案
- 在Google Cloud上实现多层架构，集成Confidential VMs和TEE
- 将合规性从程序性要求转化为可验证的技术保证

---

### 4. zkFL-Health: Blockchain-Enabled Zero-Knowledge Federated Learning for Medical AI Privacy
**年份**: 2025  
**arXiv**: [2512.21048](https://arxiv.org/abs/2512.21048)  
**作者**: Savvy Sharma, George Petrovic, Sarthak Kaushik  
**机构**: George Brown Polytechnic, Toronto, Canada  
**出处**: arXiv:2512.21048v1 [cs.CR] (2025年12月24日)

**摘要**:
医疗AI需要大规模多样的数据集，但严格隐私和治理限制阻止机构间原始数据共享。联邦学习（FL）在数据所在地点训练并仅交换模型更新，缓解了数据外流问题，但实际部署仍面临两大核心风险：(1) 通过梯度或更新泄露隐私（成员推断、梯度反转）；(2) 对聚合服务器的信任——单一故障点可能丢弃、篡改或注入贡献。本文提出zkFL-Health，将FL与零知识证明（ZKP）和TEE结合，提供医疗AI的隐私保护、可验证正确协作训练。

**关键贡献**:
- 提出zkFL-Health架构，结合FL、ZKP和TEE实现隐私保护的医疗AI协作训练
- 使用TEE保护聚合器计算过程，使用ZK证明验证聚合正确性
- 提供隐私（无数据泄露）、完整性（正确聚合）、可审计性（链上记录）的全面保证

---

## 综合对比分析

### 主题分布

| 论文 | 核心主题 | TEE应用场景 |
|------|----------|-------------|
| Abstraction of TEEs | TEE抽象层与机密计算统一化 | 跨平台抽象、云边协同 |
| OTR | LLM推理可验证性 | 区块链DePIN、optimistic rollup |
| AI Healthcare | 医疗AI安全 | Google Cloud、零信任架构 |
| zkFL-Health | 联邦学习隐私保护 | 医疗AI、区块链、ZKP结合 |

### 技术路线对比

**1. TEE作为基础设施**:
- Abstraction of TEEs：系统化分析TEE技术的分类与抽象层设计
- AI Healthcare：使用Google Cloud Confidential VMs作为基础
- OTR和zkFL-Health：均利用TEE作为核心信任根

**2. TEE与密码学结合**:
- zkFL-Health：TEE + ZKP双重保护
- OTR：TEE + optimistic fraud proof + ZK spot check

**3. 应用场景创新**:
- OTR：将TEE应用于区块链智能合约的LLM推理
- zkFL-Health：将TEE应用于医疗联邦学习
- AI Healthcare：将零信任架构与机密计算结合

### 共同趋势

1. **TEE从单一技术走向系统整合**：TEE与零信任、ZKP、区块链等技术结合
2. **抽象层的重要性凸显**：WebAssembly是统一TEE生态的关键
3. **医疗AI成为TEE应用的热门场景**
4. **硬件与软件协同成为主流**

---

## 参考文献

1. Michaud Q., Ramezanian S., Ayed D., Levillain O., Garcia-Alfaro J. (2025). *Abstraction of Trusted Execution Environments as the Missing Layer for Broad Confidential Computing Adoption*. arXiv:2512.22090 [cs.CR]

2. Chana A., Dinga A., Chen F., Wu A., Zhang B., Tian A. (2025). *Optimistic TEE-Rollups: A Hybrid Architecture for Scalable and Verifiable Generative AI Inference on Blockchain*. arXiv:2512.20176 [cs.CR]

3. Amanna A., Shinde I. (2025). *Securing Generative AI in Healthcare: A Zero-Trust Architecture Powered by Confidential Computing on Google Cloud*. arXiv

4. Sharma S., Petrovic G., Kaushik S. (2025). *zkFL-Health: Blockchain-Enabled Zero-Knowledge Federated Learning for Medical AI Privacy*. arXiv:2512.21048 [cs.CR]