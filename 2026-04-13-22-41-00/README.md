# TEE 论文下载会话 (2026-04-13-22-41-00)

## 概述

本目录包含 2026 年 4 月 13 日通过 Google 搜索下载的可信执行环境 (TEE) 相关顶级会议论文。

## 下载来源

- 目标会议: NDSS (Network and Distributed System Security Symposium), ACM, IEEE 等顶级会议
- 时间范围: 2025-2026 年
- 搜索关键词: Trusted Execution Environment, TEE, Confidential Computing

## 本次下载的论文

### 1. SoK: Analysis of Accelerator TEE Designs (2026)

**会议**: NDSS Symposium 2026  
**日期**: 2026年2月23-27日  
**地点**: San Diego, CA, USA  
**DOI**: https://doi.org/10.14722/ndss.2026.241424

**作者**:
- Chenxu Wang* (南方科技大学)
- Junjie Huang* (南方科技大学)
- Yujun Liang (南方科技大学)
- Xuania Peng (中国科学院大学)
- Yuqun Zhang (南方科技大学)
- Fengwei Zhang* (南方科技大学)
- Jiannong Cao (香港理工大学)
- Hang Lu (中国科学院大学)
- Rui Hou (中国科学院大学)
- Shoumeng Yan (蚂蚁集团)
- Tao Wei (蚂蚁集团)
- Zhengyu He (蚂蚁集团)

(*: 共同一作; *: 通讯作者)

**摘要 (Abstract)**:

可信执行环境 (TEE) 是一种流行的技术,能为加速器上的敏感数据/代码提供强大的机密性、完整性和隔离保护。然而,大多数研究都是针对特定 CPU 或加速器设计的,因此缺乏通用性最近的 TEE 调查部分总结了加速器计算的安全威胁和保护,但尚未提供构建加速器 TEE 的指南,也未比较其安全解决方案的优缺点。本文我们对多年来的加速器 TEE 进行了全面的分析。我们总结了一个典型的加速器 TEE 构建框架,并总结了广泛使用的攻击向量,从软件攻击到物理攻击。此外,我们对加速器 TEE 的三个主要安全机制进行了系统化:(1)访问控制,(2)内存加密/解密,(3)认证。对于每个方面,我们比较了现有研究中的各种安全解决方案,并总结了它们的见解。最后,我们分析了在真实平台上部署 TEE 的影响因素,特别是在可信计算基 (TCB) 和兼容性问题方面。

**贡献**:

1. 将加速器 TEE 的当前设计选择总结为三个主要分类:Host-type、Acc.-type 和 Mix-type 设计。
2. 描述了加速器计算的攻击向量及其能力。此模型有利于 TEE 设计者防御特定攻击。
3. 总结了访问控制的 mainstream 解决方案。还分析了现有研究中解决方案及其组合的偏好。
4. 分类了内存加密的解决方案。比较了这些解决方案在粒度、安全保证和性能方面的优缺点。
5. 分析了现有认证解决方案,包括详细的认证工作流程以及现有研究中缺少的组件。
6. 分析了现有研究中的 TCB 大小。我们的分析表明,加速器 TEE 设计中 guest/system TCB 的增加存在安全担忧。
7. 全面讨论了跨现有研究的兼容性问题,特别是在多类型和即插即用软件/硬件支持方面。

**核心内容**:

### 研究问题 (Research Questions)

- **RQ1**: 构建加速器 TEE 的典型框架是什么?
- **RQ2**: 如何在不同的 CPU/加速器上构建具有强安全性的加速器 TEE?
- **RQ3**: 什么因素影响加速器 TEE 在真实平台上的部署?

### 加速器 TEE 分类

1. **Host-type designs**: 主要使用 CPU 端软件/固件保护加速器
2. **Acc.-type designs**: 更倾向于在加速器和连接 I/O 总线上设计保护
3. **Mix-type designs**: 两种类型的混合设计

### 攻击向量

- **AT (Attack on accelerator task)**: 包括任务代码、数据、元数据等
- **AE (Attack on accelerator environment)**: 包括加速器软件、MMIO 寄存器、硬件设备
- **AA (Attack on authenticity)**: 针对真实性的攻击

### 安全机制

1. **访问控制 (Access Control)**: SAC1-SAC6 不同层次的解决方案
2. **内存加密 (Memory Encryption)**: SM E1-SM E3 不同机制
3. **认证 (Attestation)**: SAT1-SAT4 不同验证方式

### 主要发现

1. **物理对手被低估**: 缺乏针对不同部署场景的内存加密会使系统暴露于严重攻击向量
2. **不恰当的粒度会增加开销**: 为特定加速器设计内存加密时,盲目重用 CPU TEE 或其他加速器 TEE 的解决方案会增加大量性能开销
3. **CPU 和加速器之间加密粒度不一致会导致性能开销**
4. **缺乏认证实现的加速器面临真实性和完整性风险**

**评估的加速器 TEE 数量**: 51 项研究,来自顶级会议和主流行业设计

## 格式规范

所有论文按以下格式命名:
```
年份 - 标题.pdf
```

例如: `2026 - SoK - Analysis of Accelerator TEE Designs.pdf`

## 更新日志

- 2026-04-13: 初始下载 - SoK: Analysis of Accelerator TEE Designs (NDSS 2026)

## 注意事项

本次会话尝试下载了多篇论文,但由于 ACM Digital Library 等来源需要订阅认证,大部分下载失败。成功获取的论文仅有本篇 NDSS 2026 论文。

---
生成时间: 2026-04-13 22:41:00 (Pacific/Auckland)
