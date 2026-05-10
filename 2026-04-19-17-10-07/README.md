# 2026-04-19-17-10-07

本目录包含 1 篇最新下载的 TEE 相关论文。

## 论文列表

| 文件名 | 年份 | 会议/期刊 | DOI |
|--------|------|----------|-----|
| 2025 - The Road to Trust - Building Enclaves within Confidential VMs.pdf | 2025 | NDSS | — |

## 论文概要

### The Road to Trust: Building Enclaves within Confidential VMs

**作者**：Wenhao Wang, Linke Song, Benshan Mei, Shuang Liu, Shijun Zhao, Shoumeng Yan, XiaoFeng Wang, Dan Meng, Rui Hou

**核心问题**：在基于 VM 的 TEE（如 AMD SEV、Intel TDX、ARM CCA）中，如果 guest OS 被攻破，如何建立对机密 VM 内应用程序的信任？

**主要贡献**：
1. **NestedSGX 架构**：在 AMD SEV 机密 VM（Confidental VM, CVM）内部实现 Intel SGX 风格的飞地（enclave），即使 guest OS 已沦陷也能保护应用安全。
2. **信任链设计**：通过 AMD SEV 的硬件根信任出发，构建从 CVM 启动到飞地运行的全链路信任。
3. **安全分析**：分析了 NestedSGX 对不受信任的 guest OS、主机 VMM 和飞地本身的安全性。
4. **实现**：基于 Linux SVSM 框架，约 7500 行代码（Rust + C），已在 AMD EPYC 7543 服务器上部署。

**技术细节**：
- **NestedSGX Driver**：运行在 kernel 模式，专门负责在 VMPL（Virtual Machine Privilege Level）之间切换页面表
- **安全监控器（Security Monitor）**：控制飞地的页面表，防止飞地绕过安全策略
- **度量与证明（Attestation）**：支持 EGETKEY/EREPORT 等 SGX 指令，在 SEV 环境中实现远程证明
- **性能**：VMPL 切换约 19400 周期，与传统 SGX 相比开销可接受

**与本合集中其他论文的关系**：
- 与 *The Forking Way: When TEEs Meet Consensus*（本会话同期下载）同属 NDSS 2025，均研究 TEE 的安全属性
- 与 *TME-Box*（本会话同期下载）均涉及内存隔离技术，但 TME-Box 关注 Intel TME-MK 内存加密，而本文关注在 VM-TEE 内重建进程级隔离
- 与 *Transparent Attested DNS*（2026-04-19-16-46-35）共享机密计算主题，但本文聚焦于 VM-TEE 架构设计

**关键词**：AMD SEV, 机密虚拟机, 飞地, 嵌套 SGX, 信任链, 远程证明
