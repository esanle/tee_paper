# TEE 论文集 · 2026-04-13

本目录收录 2025 年顶级会议（NDSS 2025 / CCS 2025）中与**可信执行环境（Trusted Execution Environment, TEE）**相关的最新学术论文，共 10 篇。所有论文均经过严格同行评审，发表于网络与系统安全领域顶级会议。

---

## 论文列表

| # | 会议 | 标题 |
|---|------|------|
| 1 | CCS 2025 | Attestable Builds: Compiling Verifiable Binaries on Untrusted Systems using TEE |
| 2 | NDSS 2025 | ASGARD: Protecting On-Device Deep Neural Networks with Virtualization-Based TEE |
| 3 | NDSS 2025 | Blindfold: Confidential Memory Management by Untrusted OS |
| 4 | NDSS 2025 | The Forking Way: When TEEs Meet Consensus |
| 5 | NDSS 2025 | PALANTÍR: A Formal Approach to Multi-Layered Privileges for Enclaves |
| 6 | NDSS 2025 | RContainer: A Secure Container Architecture through Extending ARM CCA |
| 7 | NDSS 2025 | SCRUTINIZER: Towards Secure Forensics on Compromised TrustZone |
| 8 | NDSS 2025 | TME-Box: Scalable In-Process Isolation through Intel TME-MK Memory Encryption |
| 9 | NDSS 2025 | NestedSGX: The Road to Trust – Building Enclaves within Confidential VMs |
| 10 | NDSS 2025 | WAVEN: WebAssembly Memory Virtualization for Enclaves |

---

## 论文详解

### 1. Attestable Builds (CCS 2025)

**标题：** Attestable Builds: Compiling Verifiable Binaries on Untrusted Systems using Trusted Execution Environments

**作者：** Daniel Hugenroth, Mario Lins, René Mayrhofer, Alastair R. Beresford（剑桥大学 & 林茨约翰内斯·开普勒大学）

**会议：** ACM CCS 2025

**一句话摘要：** 利用 TEE 与沙盒构建容器，为软件制品提供从源代码到最终二进制的强对应性证明，有效应对供应链攻击。

**核心贡献：**

本文提出**可证明构建（Attestable Builds）**这一新范式，直击软件供应链安全中最核心的问题之一——如何确保最终分发的二进制文件确实由特定源代码正确编译而来。传统上，软件构建在用户完全不透明的可信构建服务器上进行，构建过程本身就是一个信任黑箱；而可复现构建虽然提供了部分保证，却需要大量工程改造且维护成本极高。

Attestable Builds 的核心思路是：利用现代 TEE（如 Intel SGX、AMD SEV）创建**沙盒构建容器**，将构建过程封装在硬件隔离的可信执行环境中。具体而言，构建容器在 TEE 内运行，任何第三方均可远程验证（Remote Attestation）该容器确实由指定源代码快照构建而来。整个构建流程被记录为可验证的证明（attestation），接收者无需运行构建即可确信二进制文件的来源和完整性。

本文对可复现构建与可证明构建进行了系统比较。可证明构建的优势在于：对现有项目几乎无需修改，可实现即时验证，且能防范供应链攻击（如 SolarWinds 攻击和 XZ Utils 后门事件 CVE-2024-3094）。代价是启动延迟约 42 秒，构建时间增加约 14%，但对大型项目而言这一开销完全可接受。

**安全模型：** 本文形式化建模并验证了可证明构建设计，证明了其对强力资源对手的安全性。原型系统成功构建了 LLVM Clang 等复杂开源项目，无需修改其源代码或构建脚本。

---

### 2. ASGARD (NDSS 2025)

**标题：** ASGARD: Protecting On-Device Deep Neural Networks with Virtualization-Based Trusted Execution Environments

**作者：** Myungsuk Moon, Minhee Kim, Joonkyo Jung, Dokyung Song（延世大学）

**会议：** NDSS 2025

**DOI：** 10.14722/ndss.2025.240449

**一句话摘要：** ASGARD 是首个基于虚拟化 TEE 的方案，在传统 Armv8-A SoC 上以最小 TCB 保护设备端 DNN 模型隐私，实现近零运行时开销。

**核心贡献：**

随着端侧深度学习（on-device deep learning）的普及，DNN 模型本身作为知识产权和用户隐私数据的载体，其保护需求日益迫切。然而现有基于 Arm TrustZone 的保护方案存在根本性局限：TrustZone 只能静态划分物理资源（Normal World / Secure World），导致 Secure World 内存受限（通常仅 10-32MB）且无法访问 NPU 等硬件加速器。

ASGARD 的核心创新在于**将虚拟化技术引入 TEE 设计**，突破了 TrustZone 的资源静态划分限制。具体而言：

1. **安全 I/O 直通（Secure I/O Passthrough）：** 通过虚拟化将 SoC 集成 NPU 安全纳入 TEE 边界，无需修改 Arm 或芯片厂商的专有软件；
2. **TCB 精简（TCB Debloating）：** 从平台级和应用级两个维度裁剪可信计算基，将 TCB 控制在极小范围内；
3. **退出合并（Exit-Coalescing）：** 智能规划 DNN 执行流程，最大程度减少 TEE ↔ REE 之间的上下文切换开销。

实验在 RK358S（Armv8.2-A commodity Android 平台，配备 Rockchip NPU）上进行。评估结果表明，ASGARD 有效保护了设备端 DNN 模型隐私，TKB 大小极小，且推理延迟开销接近零。

---

### 3. Blindfold (NDSS 2025)

**标题：** Blindfold: Confidential Memory Management by Untrusted Operating System

**作者：** Caihua Li, Seung-seob Lee, Lin Zhong（耶鲁大学）

**会议：** NDSS 2025

**DOI：** 10.14722/ndss.2025.240294

**一句话摘要：** Blindfold 提出一种让不可信 Linux 内核能够合法管理机密内存的机密计算设计方案，以轻量级能力系统统一既往逐案处理方案，TCB 更小且性能更具竞争力。

**核心贡献：**

机密计算（Confidential Computing）允许程序在不受信任的操作系统上保护自身数据的机密性，但现有方案普遍面临一个两难困境：**隐藏内存（禁用 OS 访问）** vs. **加密内存（性能开销大）**，且两者都会破坏 OS 的内存优化能力（如大页迁移、内存压缩等）。

Blindfold 的核心洞察是：不需要嵌套页表，而是让 **Guardian**（运行在比内核更高特权级的可信软件组件）**动态切换**页表和中断表，而非将它们嵌套在 TCB 内部。具体提出三项技术：

1. **表切换而非表嵌套：** 将页表和中断表留在 TCB 外部，由 Guardian 决定使用哪套表，从而 mediation OS 对内存的访问和处理异常；
2. **轻量级能力系统（Lightweight Capability System）：** 用统一的能力模型规范 OS 对用户内存的语义访问，替代既往逐案特殊处理；
3. **机密内存管理的安全 ABI：** 无需加密即可安全暴露机密内存管理接口。

在 ARMv8-A/Linux 上的原型实现仅需约 400 行内核修改，TCB 小于同类系统，且 Linux 的大部分内存优化（包括除内存压缩外的功能）均可正常工作。

---

### 4. The Forking Way (NDSS 2025)

**标题：** The Forking Way: When TEEs Meet Consensus

**作者：** Annika Wilde, Tim Niklas Gruel（波鸿鲁尔大学）, Claudio Soriente（NEC 欧洲实验室）, Ghassan Karame（波鸿鲁尔大学）

**会议：** NDSS 2025

**DOI：** 10.14722/ndss.2025.241934

**一句话摘要：** 系统化分析了 29 个 TEE-区块链融合方案中防范分叉攻击的技术路线，揭示了现有生产级系统的未知漏洞并提出对应防御措施。

**核心贡献：**

TEE 与区块链的结合被视为"天作之合"：TEE 为区块链带来机密计算能力，而区块链的共识层可以帮助 TEE 抵御分叉攻击（forking attacks）。然而，这一"婚姻"实际上存在大量未被发现的设计问题。

本文对 **29 个 TEE-区块链方案**（从学术论文到生产级平台，包括 Ten、Phala、Secret Network）进行了系统分析，归纳出**四类 TEE 与共识的互联模式**，并逐一分析其反分叉攻击能力的局限性。

特别重要的是，本文揭示了此前未被记录的攻击面：**基于克隆（cloning）的分叉攻击**。此前工作仅考虑了回滚攻击（rollback attacks），但基于状态克隆的分叉攻击即使在有反回滚机制的系统中仍然可行。

本文还负责任地披露了在 Ten、Phala 和 Secret Network 三个生产级平台中新发现的安全漏洞，并向相关开发者提供了具体的缓解措施。

---

### 5. PALANTÍR (NDSS 2025)

**标题：** A Formal Approach to Multi-Layered Privileges for Enclaves

**作者：** Ganxiang Yang, Chenyang Liu, Zhen Huang, Guoxing Chen, Hongfei Fu, Yuanyuan Zhang, Haojin Zhu（上海交通大学）

**会议：** NDSS 2025

**一句话摘要：** PALANTÍR 提出可验证的多层 enclave 权限模型，通过父-子 enclave 关系实现安全的 Enclave 功能扩展，验证表明安全属性不被破坏且运行时开销 <5%。

**核心贡献：**

随着 TEE（尤其是 RISC-V PENGLAI 等平台）在安全关键应用中的广泛采用，**enclave 功能扩展（feature extension）** 成为一个重要需求——即在已有 enclave 旁运行扩展模块来提供额外功能（如日志、监控）。然而，现有权限扩展方案在安全供给模式上仍存在挑战。

PALANTÍR 引入**父子 enclave 关系**，授予父 enclave 两项特权：**执行控制权（Execution Control）** 和 **空间控制权（Spatial Control）**，以支持对子 enclave 的安全功能扩展。通过嵌套父子关系，PALANTÍR 实现**多层权限（Multi-Layered Privileges, MLP）**，使扩展功能可按最小权限原则部署在不同特权层级。

为证明安全性，本文构建了形式化模型 **TAP∞**，验证权限模型不会破坏或弱化 enclave 的安全保障。在 PENGLAI（RISC-V 开源 TEE 平台）上的原型实现表明，运行时开销 <5%，启动延迟可接受。

---

### 6. RContainer (NDSS 2025)

**标题：** RContainer: A Secure Container Architecture through Extending ARM CCA Hardware Primitives

**作者：** Qihang Zhou, Wenzhuo Cao, Xiaoqi Jia 等（中国科学院信息工程研究所）

**会议：** NDSS 2025

**DOI：** 10.14722/ndss.2025.240328

**一句话摘要：** RContainer 通过扩展 ARM CCA 硬件原语实现安全容器架构，以小体量可信 mini-OS 配合 conshim 隔离机制，显著增强容器安全性，性能开销可控。

**核心贡献：**

容器已成为云原生环境的主流部署方案，但与传统虚拟机相比，其隔离能力较弱（共享宿主机 Linux 内核），这在 ARM 架构云服务器上尤其令人担忧。ARM CCA（Confidential Computing Architecture）虽然提供了新层级的机密 VM 支持，但现有 CCA 方案仍无法同时实现：强隔离、足够轻量、最小特权代码。

RContainer 的设计包括：

1. **可信 mini-OS：** 运行在降权 OS 旁边的小型可信操作系统，负责监控 OS 与容器之间的控制流；
2. **conshim 隔离：** 在内核层通过 ARM GPC（Granule Protection Check）机制为每个容器创建独立的物理地址空间隔离（conshim）；

在 ARMv9-A FVP 和 ARMv8 硬件 SoC 上的实现评估表明，RContainer 可显著增强容器安全性，TCB 小且性能开销可控。

---

### 7. SCRUTINIZER (NDSS 2025)

**标题：** SCRUTINIZER: Towards Secure Forensics on Compromised TrustZone

**作者：** Yiming Zhang, Fengwei Zhang, Xiapu Luo 等（南方科技大学、香港理工大学、Ant Group）

**会议：** NDSS 2025

**DOI：** 10.14722/ndss.2025.230147

**一句话摘要：** SCRUTINIZER 首创针对已陷落 TrustZone 系统的安全数字取证方案，利用 ARM CCA Root world 构建隔离的取证代理，使平台所有者能够进行事件响应和安全扫描。

**核心贡献：**

TrustZone 系统近年来漏洞频发（5 年内超过 200 个 CVE），但数字取证工具的缺失使得平台所有者无法进行事件响应或定期安全扫描。现有方案面临两难：

- **TrustZone 外取证** → 被 TrustZone 隔离阻断，根本不可行
- **TrustZone 内取证** → 如果 Secure World 本身已被攻破，取证工具也被攻击者控制，不安全

SCRUTINIZER 利用 ARM CCA 最新引入的 **Root world**（最高特权域）构建隔离的 **SCRUTINIZER Monitor**，其核心设计：

1. **保护层（Protective Layer）：** 将内存获取功能从 Monitor 解耦，集成到 TrustZone 内的代理中，最小化 Root world 代码扩展；
2. **页表嫁接（Page Table Grafting）：** 将目标的大多数页表嫁接在代理中，减少冗余地址转换和映射操作；
3. **硬件特性安全利用：** 利用标准硬件特性（内存访问陷阱、指令追踪）实现安全取证能力，防范特权对手对硬件配置的篡改。

原型系统在真实 ARM 平台上实现并经受了广泛评估，取证有效且免疫特权攻击者。

---

### 8. TME-Box (NDSS 2025)

**标题：** TME-Box: Scalable In-Process Isolation through Intel TME-MK Memory Encryption

**作者：** Martin Unterguggenberger, Lukas Lamster, David Schrammel, Stefan Mangard（格拉茨理工大学）, Martin Schwarzl（Cloudflare）

**会议：** NDSS 2025

**DOI：** 10.14722/ndss.2025.240277

**一句话摘要：** TME-Box 重新利用 Intel TME-MK（原本为虚拟机加密设计）实现进程内高效沙箱，支持最多 32K 并发沙箱，数据隔离几何平均性能开销仅 5.2%。

**核心贡献：**

云服务商在性能优化与安全隔离之间面临取舍：serverless FaaS 等多租户场景需要极低启动延迟和快速执行，但完全放弃进程隔离会使单个内存安全漏洞导致整个系统被攻破（如 Heartbleed、Cloudbleed）。

现有进程内隔离方案（如 MPK 仅支持 16 个保护域）无法满足现代云需求。TME-Box 的核心创新在于**重新利用 Intel TME-MK（Total Memory Encryption - Multi-Key）**——原本设计用于加密 VM 内存的硬件特性——来实现进程内细粒度隔离。

具体而言，TME-Box 通过**编译器插桩（compiler instrumentation）**强制各沙箱对其内存交互使用指定的加密密钥，实现密码学隔离。这带来：

- **细粒度访问控制：** 从单缓存行到整页的任意粒度
- **灵活数据重定位：** 支持动态内存重新分配
- **可扩展性：** 高效支持最多 32K 并发沙箱

使用 x86 分段寻址的性能优化原型在 SPEC CPU2017 上评估，数据隔离几何平均开销 5.2%，代码+数据隔离开销 9.7%。

---

### 9. NestedSGX / The Road to Trust (NDSS 2025)

**标题：** The Road to Trust: Building Enclaves within Confidential VMs

**作者：** Wenhao Wang, Linke Song, Benshan Mei, Shijun Zhao（中国科学院信息工程研究所）, XiaoFeng Wang（印第安纳大学）, Dan Meng, Rui Hou

**会议：** NDSS 2025

**DOI：** 10.14722/ndss.2025.240385

**一句话摘要：** NestedSGX 在 AMD SEV-SNP 的 VMPL 硬件特性上构建嵌套式 SGX  enclave，允许在 CVM 内部创建类似 Intel SGX 的硬件级 enclave，实现与 Intel SGX 的二进制兼容。

**核心贡献：**

机密虚拟机（CVM，基于 AMD SEV、Intel TDX、ARM CCA）提供了完整的 VM 级隔离，但用户仍然无法控制运行在 CVM 内的代码完整性与信任——Guest OS 被攻破后可以任意加载和执行恶意代码。

vSGX 是在 AMD SEV 上虚拟化 Intel SGX 的先驱工作，但其空 ECall 操作耗时约 1.5ms，是原生 SGX 的约 160 倍，严重限制了服务吞吐量。

NestedSGX 利用 AMD SEV-SNP 引入的 **VMPL（Virtual Machine Privilege Level）** 硬件特性，在 Guest VM 内部创建硬件级 enclave。与 vSGX 的两 VM 方案不同，NestedSGX 将 enclave 直接置于 CVM 内，Guest OS 同样被视为不可信的。

核心设计：
1. 利用 VMPL 在 CVM 内部实现硬件 enclave 创建，Guest OS 无权干预
2. 通过模拟 SGX leaf functions 实现与 Intel SGX 的 SDK 兼容，零修改迁移现有 SGX 应用
3. 已将 SGX SDK 和 Occlum library OS 移植到 NestedSGX

性能评估：上下文切换约 32,000–34,000 周期（约为 Intel SGX 的 1.9×–2.1×），真实应用平均计算/内存密集型工作负载开销 <2%，I/O 密集型 <15.68%。

---

### 10. WAVEN (NDSS 2025)

**标题：** WAVEN: WebAssembly Memory Virtualization for Enclaves

**作者：** Weili Wang, Honghan Ji, Peixuan He, Yinqian Zhang（南方科技大学）

**会议：** NDSS 2025

**DOI：** 10.14722/ndss.2025.230746

**一句话摘要：** WAVEN 首创 Wasm 内存虚拟化方案，使 Wasm 模块间可安全共享内存并实现页级访问控制，为 TEE 上的机密 FaaS 和数据市场等场景铺平道路。

**核心贡献：**

Wasm+TEE 结合是机密计算平台实现**enclave 内多租户**的热门方向：Wasm 运行时提供基于软件故障隔离（SFI）的沙箱，隔离不受信任的代码实例。然而，Wasm 的线性内存模型在跨模块数据共享和细粒度访问控制上存在显著缺陷，限制了机密有状态 FaaS 和数据市场等应用场景。

WAVEN 提出针对 Wasm 的新型**内存虚拟化方案**，核心贡献：

1. **跨模块内存共享：** 实现 Wasm 模块间安全、高效的内存共享机制，填补了此前 Wasm+TEE 栈中的空白；
2. **页级访问控制：** 在页粒度上实施内存访问控制，支持更细的安全隔离；
3. **最小化 TCB：** 方案设计轻量化，在 WAMR（业界流行的 TEE Wasm 运行时）上实现，评估表明其效率和有效性均具竞争力。

这是已知首个在 Wasm 中实现带细粒度访问控制的跨模块内存共享的工作。

---

## 综述与对比分析

### 主题对比

本批次 10 篇论文覆盖了 TEE 领域的多个前沿方向，可归纳为以下几类：

| 方向 | 代表论文 |
|------|---------|
| **TEE 基础设施与隔离** | TME-Box、NestedSGX、Blindfold |
| **TEE 应用场景拓展** | ASGARD、WAVEN、RContainer |
| **TEE 形式化与安全分析** | PALANTÍR |
| **TEE 与其他系统协同** | The Forking Way（区块链）、Attestable Builds（软件供应链） |
| **TEE 安全运维** | SCRUTINIZER（数字取证） |

### 关键趋势

**1. TEE 从单一技术走向融合**

越来越多的工作探索 TEE 与其他系统栈的协同：
- *The Forking Way* 系统分析了 TEE 与区块链的融合模式和安全性
- *Attestable Builds* 将 TEE 引入软件构建流程，解决供应链信任问题
- 这反映了 TEE 作为"信任根"在系统各层次发挥作用的趋势

**2. 硬件特性深度挖掘**

研究者不再满足于使用 TEE 的基本功能，而是挖掘硬件特性的更多潜力：
- *TME-Box* 将 Intel TME-MK（虚拟机内存加密）重新用于进程内隔离
- *NestedSGX* 挖掘 AMD SEV-SNP 的 VMPL 特性实现 enclave 嵌套
- *RContainer* 和 *SCRUTINIZER* 均利用 ARM CCA 的 Root world 扩展能力

这种"特性再利用"的思路对于推动机密计算实用化具有重要意义。

**3. 多层权限与组合式安全**

随着 TEE 部署规模扩大，**多个 enclave 之间的协作与权限管理** 成为新挑战：
- *PALANTÍR* 在 RISC-V TEE 上实现了多层权限模型
- *WAVEN* 研究 Wasm 模块在 enclave 内的安全协作与内存共享
- *Blindfold* 重新思考了 OS 与 TEE 之间的权限边界

**4. 从理论到实践的快速转化**

本批次论文的一个显著特点是**与产业界的紧密联系**：
- SCRUTINIZER 由 Ant Group 研究人员主导
- TME-Box 有 Cloudflare 工程师参与
- ASGARD 面向实际移动 SoC（RK3588S）部署
- The Forking Way 涉及 Ten、Phala、Secret Network 等已上线平台

### 技术创新亮点

| 论文 | 最具创新性的一点 |
|------|----------------|
| Attestable Builds | 将远程认证引入软件构建流水线，从"信任构建服务器"转为"信任构建过程本身" |
| ASGARD | 首个在传统 Armv8-A 上用虚拟化 TEE 保护 DNN 模型，工作量几乎为零 |
| Blindfold | 表切换而非表嵌套的思想，为 OS 与机密内存共存提供了新范式 |
| The Forking Way | 揭示了此前未记录的生产级 TEE-区块链系统中基于克隆的分叉攻击 |
| PALANTÍR | 在 enclave 扩展领域引入多层权限的正式验证 |
| RContainer | conshim 机制巧妙扩展 ARM CCA 保护容器隔离 |
| SCRUTINIZER | 首次解决"已陷落 TrustZone"的安全取证问题 |
| TME-Box | 将 VM 加密硬件重新用于 SaaS 多租户隔离，32K 沙箱可扩展性惊人 |
| NestedSGX | VMPL 硬件特性的创新性使用，实现 CVM 内的 SGX 级 enclave |
| WAVEN | 首个在 Wasm+TEE 栈中实现跨模块安全共享内存共享 + 细粒度访问控制 |

---

## 参考文献（原文交叉引用）

1. Hugenroth et al. "Attestable Builds: Compiling Verifiable Binaries on Untrusted Systems using Trusted Execution Environments." *ACM CCS*, 2025.
2. Moon et al. "ASGARD: Protecting On-Device Deep Neural Networks with Virtualization-Based Trusted Execution Environments." *NDSS*, 2025. DOI: 10.14722/ndss.2025.240449.
3. Li, Lee, Zhong. "Blindfold: Confidential Memory Management by Untrusted Operating System." *NDSS*, 2025. DOI: 10.14722/ndss.2025.240294.
4. Wilde et al. "The Forking Way: When TEEs Meet Consensus." *NDSS*, 2025. DOI: 10.14722/ndss.2025.241934.
5. Yang et al. "A Formal Approach to Multi-Layered Privileges for Enclaves." *NDSS*, 2025.
6. Zhou et al. "RContainer: A Secure Container Architecture through Extending ARM CCA Hardware Primitives." *NDSS*, 2025. DOI: 10.14722/ndss.2025.240328.
7. Zhang et al. "SCRUTINIZER: Towards Secure Forensics on Compromised TrustZone." *NDSS*, 2025. DOI: 10.14722/ndss.2025.230147.
8. Unterguggenberger et al. "TME-Box: Scalable In-Process Isolation through Intel TME-MK Memory Encryption." *NDSS*, 2025. DOI: 10.14722/ndss.2025.240277.
9. Wang et al. "The Road to Trust: Building Enclaves within Confidential VMs." *NDSS*, 2025. DOI: 10.14722/ndss.2025.240385.
10. Wang et al. "WAVEN: WebAssembly Memory Virtualization for Enclaves." *NDSS*, 2025. DOI: 10.14722/ndss.2025.230746.

---

*本文件由 AI 自动生成，内容基于各论文摘要及首轮内容整理。如有疏漏，欢迎指正。*
*生成时间：2026-04-13*
