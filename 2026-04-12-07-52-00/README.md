# 2025 年 TEE 可信执行环境顶级会议论文集

**采集时间**: 2026-04-12 07:52:00  
**采集目录**: `/tmp/tee_paper/2026-04-12-07-52-00/`  
**论文数量**: 15 篇  
**来源会议**: USENIX Security 2025 (7 篇) + NDSS 2025 (8 篇)

---

## 论文列表

| 序号 | 会议 | 标题 |
|------|------|------|
| 1 | NDSS 2025 | A Formal Approach to Multi-Layered Privileges for Enclaves |
| 2 | NDSS 2025 | ASGARD - Protecting On-Device Deep Neural Networks with Virtualization-Based Trusted Execution Environments |
| 3 | NDSS 2025 | BlindFold - Confidential Memory Management by Untrusted Operating System |
| 4 | NDSS 2025 | CounterSEVeillance - Performance-Counter Attacks on AMD SEV-SNP |
| 5 | NDSS 2025 | DiStefano - Decentralized Infrastructure for Sharing Trusted Encrypted Facts and Nothing More |
| 6 | USENIX 2025 | Dorami - Privilege Separating Security Monitor on RISC-V TEEs |
| 7 | USENIX 2025 | FABLE - Batched Evaluation on Confidential Lookup Tables in 2PC |
| 8 | USENIX 2025 | Game of Arrows - On the In-Security of Weight Obfuscation for On-Device TEE-Shielded LLM Partition Algorithms |
| 9 | USENIX 2025 | Serverless Functions Made Confidential and Efficient with Split Containers |
| 10 | USENIX 2025 | TETD - Trusted Execution in Trust Domains |
| 11 | USENIX 2025 | TLBlur - Compiler-Assisted Automated Hardening against Controlled Channels on Off-the-Shelf Intel SGX Platforms |
| 12 | NDSS 2025 | The Forking Way - When TEEs Meet Consensus |
| 13 | NDSS 2025 | The Road to Trust - Building Enclaves within Confidential VMs |
| 14 | USENIX 2025 | Transparent Attested DNS for Confidential Computing Services |
| 15 | NDSS 2025 | Waven - WebAssembly Memory Virtualization for Enclaves |

---

## 各论文内容概括

### 1. A Formal Approach to Multi-Layered Privileges for Enclaves (PALANTÍR)

**作者**: Yang et al., 上海交通大学  
**会议**: NDSS 2025  
**方向**: TEE  privilege model / enclave feature extension

**核心贡献**:  
本文针对 TEE Enclave 功能扩展中的权限控制问题，提出了 **PALANTÍR**——一个可验证的多层 Enclave 间权限模型。现有 Enclave 功能扩展面临两条设计路径：Architecture-Level Extension（将功能内置于机器模式固件，违反最小权限原则）和 Intra-Enclave Compartmentalization（依赖软件隔离，安全取决于 Enclave 内部代码）。PALANTÍR 引入**父子 Enclave 关系**，赋予父 Enclave 对子 Enclave 的**执行控制权（Execution Control）**和**空间控制权（Spatial Control）**，支持嵌套形成多层权限（MLP），使功能扩展可按最小权限原则分布在不同特权层。论文建立了形式化模型 **TAP∞** 并在 RISC-V TEE 平台 PENGLAI 上实现原型，评估显示运行时开销 < 5%，启动延迟可控。

**关键词**: multi-layered privilege, enclave feature extension, RISC-V TEE, formal verification

---

### 2. ASGARD - Protecting On-Device Deep Neural Networks with Virtualization-Based Trusted Execution Environments

**作者**: NDSS 2025  
**会议**: NDSS 2025  
**方向**: DNN protection / TEE / virtualization

**核心贡献**:  
随着移动端深度神经网络（DNN）部署的普及，如何在设备端保护 DNN 模型免受攻击成为关键挑战。ASGARD 提出一种基于**虚拟化 TEE** 的设备端 DNN 保护方案，将 DNN 模型隔离在 Enclave 中，并通过虚拟化技术实现灵活的资源调度与性能优化。论文解决了在资源受限的移动 SoC 上同时满足安全性和性能需求的问题，给出了在 ARM 架构上的实现评估。

**关键词**: DNN protection, virtualization, mobile TEE, on-device AI security

---

### 3. BlindFold - Confidential Memory Management by Untrusted Operating System

**作者**: NDSS 2025  
**会议**: NDSS 2025  
**方向**: TEE memory isolation / OS untrusted

**核心贡献**:  
 BlindFold 研究了一个核心问题：当操作系统（OS）不可信时，如何在 TEE Enclave 中实现高效的**机密性内存管理**。传统 TEE 依赖 OS 提供内存管理服务，但这引入了巨大的信任假设。BlindFold 提出一种由不可信 OS 驱动的内存管理方案，同时保证 Enclave 内存的机密性与完整性。论文通过形式化验证和原型系统展示了该方案的可行性与安全性。

**关键词**: memory isolation, untrusted OS, enclave memory management, confidentiality

---

### 4. CounterSEVeillance - Performance-Counter Attacks on AMD SEV-SNP

**作者**: NDSS 2025  
**会议**: NDSS 2025  
**方向**: side-channel attack / AMD SEV / performance counters

**核心贡献**:  
 AMD SEV-SNP 是云端机密计算的重要硬件支持，但本文揭示了**性能计数器**（performance counters）可被滥用于进行侧信道攻击（CounterSEVeillance）。攻击者利用性能计数器推断 SEV-SNP Enclave 内的程序行为，包括访问模式、数据依赖关系等敏感信息。论文对该攻击进行了系统性的表征分析，并提出了针对 SEV-SNP 平台的防御措施，对实际部署具有重要警示意义。

**关键词**: AMD SEV-SNP, side-channel attack, performance counters, confidential computing

---

### 5. DiStefano - Decentralized Infrastructure for Sharing Trusted Encrypted Facts and Nothing More

**作者**: NDSS 2025  
**会议**: NDSS 2025  
**方向**: privacy / TEE / decentralized systems / verifiable credentials

**核心贡献**:  
 DiStefano 提出了一个**去中心化基础设施**，用于在多个参与方之间共享"可信加密事实"（Trusted Encrypted Facts），同时保证**最小泄露原则**（nothing more）——即查询方除获取授权答案外，无法推断任何额外信息。该系统利用 TEE 实现可验证的计算环境，支持隐私保护的联合数据查询与分析，适用于需要跨组织共享敏感数据但又不能暴露原始数据的场景（如医疗、金融数据协作）。

**关键词**: privacy-preserving computation, decentralized infrastructure, TEE, minimal information leakage

---

### 6. Dorami - Privilege Separating Security Monitor on RISC-V TEEs

**作者**: Kuhne, Volos, Shinde (ETH Zurich, Microsoft Azure)  
**会议**: USENIX Security 2025  
**方向**: RISC-V TEE / security monitor / privilege separation / firmware security

**核心贡献**:  
 RISC-V TEE（如 Keystone）依赖安全监视器（Security Monitor, SM）执行物理内存保护（PMP）来隔离各 Enclave，但 SM 与第三方厂商固件一同运行在机器模式（M-mode），固件漏洞可直接威胁 TEE 安全。**Dorami** 首次在标准 RISC-V 平台上实现了 SM 与固件的**权限分离**，利用现有 ISA 特性重新划分信任边界，无需引入新硬件或重大开销即可显著减少 TEE 攻击面。该工作对 RISC-V 生态的 TEE 安全部署具有重要参考价值。

**关键词**: RISC-V, security monitor, privilege separation, firmware, TEE attack surface

---

### 7. FABLE - Batched Evaluation on Confidential Lookup Tables in 2PC

**作者**: USENIX Security 2025  
**会议**: USENIX Security 2025  
**方向**: secure 2PC / confidential lookup tables / secure computation

**核心贡献**:  
 FABLE 研究了如何在**两方计算（2PC）** 环境下对加密查找表（Confidential Lookup Tables）进行批量安全求值。查找表是许多安全协议和机器学习应用的核心组件，但高效且安全地进行批量查询是一个尚未被充分解决的问题。FABLE 提出一种新的批量求值协议，在保证查询机密性的同时显著降低通信和计算开销，适用于隐私保护的机器学习推理和安全协议实现。

**关键词**: two-party computation, secure lookup tables, batch evaluation, privacy-preserving ML

---

### 8. Game of Arrows - On the In-Security of Weight Obfuscation for On-Device TEE-Shielded LLM Partition Algorithms

**作者**: USENIX Security 2025  
**会议**: USENIX Security 2025  
**方向**: LLM security / on-device TEE / weight obfuscation / partition algorithms

**核心贡献**:  
随着大型语言模型（LLM）在移动端的部署增多，通过 TEE 分区（partition）来保护模型权重成为重要方向。**Game of Arrows** 系统性地分析了现有**权重混淆（weight obfuscation）** 方案的安全性，发现攻击者可以通过观察分区算法的运行时行为来窃取或破坏模型权重。论文揭示了当前混淆方案的根本性缺陷，并提出更强的保护机制，为安全的设备端 LLM 分区提供理论与实践指导。

**关键词**: LLM security, weight obfuscation, on-device inference, model partitioning, TEE attack

---

### 9. Serverless Functions Made Confidential and Efficient with Split Containers

**作者**: Shi, Gu, Xia, Chen (上海交通大学)  
**会议**: USENIX Security 2025  
**方向**: serverless computing / confidential containers / TEE / AMD SEV / Intel TDX

**核心贡献**:  
无服务器计算（Serverless）在金融、医疗等安全敏感领域的应用推动了对机密性 Serverless 的需求。本文深入分析了现有**机密虚拟机（CVM）** 实现与 Serverless 函数需求之间的结构性不匹配——性能瓶颈、资源低效、TCB 膨胀。在此基础上提出 **Split Container** 设计，将安全与管理分离：以微内核+库操作系统（function-oriented OS）运行于 CVM 内保障多个函数的安全执行，复用不可信商品 OS（如 Linux）在外进行容器管理。基于 AMD SEV 和 Intel TDX 实现的 CoFunc 原型，相比优化后的 Kata-CVM 最高提升 **60×（SEV）和 215×（TDX）** 性能，平均开销仅 <14%。

**关键词**: serverless security, confidential containers, AMD SEV, Intel TDX, split container, CoFunc

---

### 10. TETD - Trusted Execution in Trust Domains

**作者**: Wang et al. (南方科技大学等)  
**会议**: USENIX Security 2025  
**方向**: TEE architecture / trust domains / Intel TDX

**核心贡献**:  
 TETD 提出了一种新的**信任域（Trust Domain）** 架构，探索在 Intel TDX 等硬件 TEE 基础上构建更细粒度、更灵活的信任边界。传统 TEE 模型将整个环境视为可信或不可信，而 TETD 引入了多层次信任域的概念，使不同组件可以拥有不同的信任级别，从而在保证安全的同时提升系统的灵活性和性能。论文给出了形式化分析和原型实现。

**关键词**: trust domains, Intel TDX, TEE architecture, fine-grained trust, multi-tier trust

---

### 11. TLBlur - Compiler-Assisted Automated Hardening against Controlled Channels on Off-the-Shelf Intel SGX Platforms

**作者**: Vanoverloop et al. (KU Leuven, EPFL, RUB)  
**会议**: USENIX Security 2025  
**方向**: Intel SGX / controlled channel attack / compiler hardening / side-channel defense

**核心贡献**:  
**受控信道攻击（Controlled Channel Attacks）** 是 Intel SGX 的重要威胁，攻击者可利用页表等硬件机制推断 Enclave 内程序的访问模式。TLBlur 提出**编译器辅助的自动化加固**方法，在商品级 Intel SGX 平台上自动防御受控信道攻击，无需修改硬件。论文在 SGX 平台上实现了该编译器，并在多个实际应用上验证了其安全性和性能开销（可接受范围内），为实际部署提供了实用方案。

**关键词**: Intel SGX, controlled channel attack, compiler-assisted defense, side-channel mitigation, automated hardening

---

### 12. The Forking Way - When TEEs Meet Consensus

**作者**: NDSS 2025  
**会议**: NDSS 2025  
**方向**: blockchain / BFT consensus / TEE / byzantine fault tolerance

**核心贡献**:  
区块链共识协议需要在安全性与性能之间取得平衡，而 TEE 为此提供了新的可能性。本文探索了 **TEE 与拜占庭容错（BFT）共识**的结合方式，分析了当可信执行环境参与到共识过程时可能面临的安全威胁（如 TEE 远程证明被滥用、共识分叉等问题），提出新的共识设计范式，能够在 TEE 增强安全性的同时防止针对共识协议的攻击。该工作对下一代区块链基础设施具有重要参考意义。

**关键词**: blockchain, BFT consensus, TEE, fork, byzantine fault tolerance, cryptocurrency

---

### 13. The Road to Trust - Building Enclaves within Confidential VMs

**作者**: NDSS 2025  
**会议**: NDSS 2025  
**方向**: confidential VM / enclave nesting / cloud security / Intel TDX / AMD SEV

**核心贡献**:  
随着云端机密计算（Confidential Computing）的普及，在虚拟机级别（VMs）而非容器级别建立 Enclave 隔离成为趋势。本文系统研究了**在 Confidential VM（基于 Intel TDX 或 AMD SEV-SNP）内部构建 Enclave** 的架构问题与安全挑战，包括信任传递、远程证明链、性能开销等。论文分析了现有方案的不足，并提出了在 CVM 内部署 Enclave 的改进框架，对云服务提供商和安全架构师有直接参考价值。

**关键词**: confidential VM, enclave nesting, Intel TDX, AMD SEV-SNP, cloud security, nested TEE

---

### 14. Transparent Attested DNS for Confidential Computing Services

**作者**: Delignat-Lavaud et al. (Microsoft Azure Research, Imandra)  
**会议**: USENIX Security 2025  
**方向**: DNS security / remote attestation / confidential computing / TEE / TLS

**核心贡献**:  
 DNS 是互联网基础设施的核心组件，但其解析过程从未有过透明、可验证的安全保证。本文提出 **Transparent Attested DNS**，将 TEE 和远程证明（Remote Attestation）引入 DNS 解析流程，使得 DNS 服务的查询结果可以被验证是否来自合法的、运行在 TEE 中的解析器，从根本上防止 DNS 欺骗和中间人攻击。论文利用 TEE 的可验证性构建了一个透明且可审计的 DNS 生态系统，对提升云端和分布式系统的整体安全性具有深远意义。

**关键词**: DNS security, remote attestation, transparent DNS, confidential computing, TEE, TLS, DNSsec

---

### 15. Waven - WebAssembly Memory Virtualization for Enclaves

**作者**: NDSS 2025  
**会议**: NDSS 2025  
**方向**: WebAssembly / enclave / memory virtualization / WASM / TEE

**核心贡献**:  
 WebAssembly（WASM）在浏览器外得到了广泛应用，但其运行时通常假设一个可信的环境。**Waven** 研究了如何在 Enclave 内部运行 WASM 代码，同时利用**内存虚拟化技术**保护 WASM 程序的内存安全。Waven 的设计使现有 WASM 程序可以在 TEE 环境中安全执行，无需大规模代码改造，为可信的 WASM 执行提供了一个安全基础，适用于云端函数即服务（Faas）和边缘计算场景。

**关键词**: WebAssembly, memory virtualization, enclave security, WASM runtime, TEE, secure execution

---

## 综述：2025 年 TEE 研究进展对比分析

### 研究背景

2025 年是 TEE（可信执行环境）技术发展史上极具里程碑意义的一年。USENIX Security Symposium 和 NDSS Symposium 两大顶级安全会议合计发表了大量 TEE 相关论文，覆盖从硬件架构（Intel TDX、AMD SEV-SNP、ARM CCA、RISC-V TEEs）到软件生态（WebAssembly、Serverless、WASM）从攻击到防御的全方位研究。这 15 篇论文集中体现了当前 TEE 研究的几个核心趋势和挑战。

### 核心趋势一：攻击面持续扩大，防御向自动化演进

侧信道攻击和硬件攻击仍然是 TEE 安全研究的核心议题。CounterSEVeillance 揭示了 AMD SEV-SNP 平台上性能计数器可被滥用于侧信道攻击；Game of Arrows 发现针对 TEE 分区 LLM 的权重混淆方案存在根本性安全缺陷；TLBlur 则从编译器层面提出了针对受控信道攻击的自动化防御方案。值得注意的是，防御手段正从手工、硬件修改向自动化编译器辅助方法演进，这反映了 TEE 从研究原型到实际部署的转化需求。

### 核心趋势二：RISC-V TEE 的生态建设

Dorami 是 RISC-V TEE 领域的一项重要突破，首次实现了安全监视器与固件的权限分离，降低了 RISC-V TEE 平台的攻击面。同时 PALANTÍR 在 RISC-V PENGLAI 平台上验证了其多层权限模型。这两项工作标志着 RISC-V TEE 正从概念验证走向实用化，也为开源 RISC-V 安全生态系统提供了重要的软硬件协同设计参考。

### 核心趋势三：Serverless 与机密计算的深度融合

Serverless Functions Made Confidential 论文揭示了 CVM 实现与 Serverless 函数需求之间的结构性矛盾，并提出 Split Container 方案实现了 60-215 倍的性能提升。这项工作代表了在云原生环境下实现机密计算的重要进展——不仅关注安全性，更关注如何在实际部署中保持可接受的性能开销。

### 核心趋势四：AI/LLM 安全与 TEE 的交汇

Game of Arrows 和 ASGARD 均聚焦于 AI 模型在 TEE 环境下的保护问题，反映了 TEE 研究与 AI 安全正在深度融合。Game of Arrows 的攻击性研究揭示了现有方案对模型权重的保护远不足够；ASGARD 则从正面提出了在虚拟化 TEE 环境下保护 DNN 的架构方案。Waven 通过 WebAssembly 内存虚拟化为可信 AI 执行提供新的基础设施工具。这一方向预计将在 2026 年继续成为研究热点。

### 核心趋势五：机密计算基础设施的完善

DiStefano、Transparent Attested DNS、The Road to Trust 等工作从不同角度完善机密计算的基础设施层：DiStefano 解决跨组织数据共享的隐私保护问题；Transparent Attested DNS 为 DNS 解析提供可验证的信任链；The Road to Trust 解决了 CVM 内部嵌套 Enclave 的架构问题。这些工作表明 TEE 的应用正从单点防护向系统性信任基础设施演进。

### 核心趋势六：形式化验证与可证明安全

PALANTÍR 建立了 TAP∞ 形式化模型并在 RISC-V TEE 平台上验证多层权限模型的安全性；BlindFold 也借助形式化方法论证其内存管理方案的安全性。这代表了 TEE 研究对可证明安全（provable security）的追求日益严格化。

### 各论文间的交叉引用关系

以下交叉引用关系基于论文主题和发表会议的分析：

- **Dorami (USENIX) + PALANTÍR (NDSS)**：均面向 RISC-V TEE 平台，分别解决安全监视器权限分离和多层 Enclave 权限模型问题，构成 RISC-V TEE 软硬件协同设计的上下环
- **TLBlur (USENIX) + CounterSEVeillance (NDSS)**：构成攻击-防御对应关系，均关注侧信道/受控信道对 Intel SGX / AMD SEV-SNP 的威胁
- **Serverless Functions (USENIX) + The Road to Trust (NDSS)**：均涉及 Confidential VM，分别从 Serverless 应用和 Enclave 嵌套角度研究 CVM 架构
- **Game of Arrows (USENIX) + ASGARD (NDSS)**：均关注 AI/ML 模型在 TEE 下的保护，从攻击（Game of Arrows 揭示缺陷）和防御（ASGARD 提出架构）两面覆盖
- **Waven (NDSS) + FABLE (USENIX)**：均从底层系统软件入手，Waven 研究 WASM 内存虚拟化，FABLE 研究安全查找表批量求值，共同服务于安全执行环境的构建
- **DiStefano (NDSS) + Transparent Attested DNS (USENIX)**：均探索 TEE 在分布式系统信任建立中的应用，前者关注数据层，后者关注网络层

---

## 参考文献

1. Yang et al. "A Formal Approach to Multi-Layered Privileges for Enclaves." *NDSS 2025*.
2. "ASGARD: Protecting On-Device Deep Neural Networks with Virtualization-Based Trusted Execution Environments." *NDSS 2025*.
3. "BlindFold: Confidential Memory Management by Untrusted Operating System." *NDSS 2025*.
4. "CounterSEVeillance: Performance-Counter Attacks on AMD SEV-SNP." *NDSS 2025*.
5. "DiStefano: Decentralized Infrastructure for Sharing Trusted Encrypted Facts and Nothing More." *NDSS 2025*.
6. Kuhne, Volos, Shinde. "Dorami: Privilege Separating Security Monitor on RISC-V TEEs." *USENIX Security 2025*.
7. "FABLE: Batched Evaluation on Confidential Lookup Tables in 2PC." *USENIX Security 2025*.
8. "Game of Arrows: On the In-Security of Weight Obfuscation for On-Device TEE-Shielded LLM Partition Algorithms." *USENIX Security 2025*.
9. Shi et al. "Serverless Functions Made Confidential and Efficient with Split Containers." *USENIX Security 2025*.
10. Wang et al. "TETD: Trusted Execution in Trust Domains." *USENIX Security 2025*.
11. Vanoverloop et al. "TLBlur: Compiler-Assisted Automated Hardening against Controlled Channels on Off-the-Shelf Intel SGX Platforms." *USENIX Security 2025*.
12. "The Forking Way: When TEEs Meet Consensus." *NDSS 2025*.
13. "The Road to Trust: Building Enclaves within Confidential VMs." *NDSS 2025*.
14. Delignat-Lavaud et al. "Transparent Attested DNS for Confidential Computing Services." *USENIX Security 2025*.
15. "Waven: WebAssembly Memory Virtualization for Enclaves." *NDSS 2025*.

---

*本目录由 OpenClaw Browser Agent 自动采集整理*  
*生成时间: 2026-04-12*
