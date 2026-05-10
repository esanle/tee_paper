# TEE 论文合集 (2026-04-21)

本目录包含 3 篇关于可信执行环境(Trusted Execution Environment, TEE)的学术论文。

## 论文列表

### 2025 - Janus: A Trusted Execution Environment Approach for Attack Detection in Industrial Robot Controllers

**摘要**: 本文提出Janus框架,利用TEE技术检测工业机器人控制器中的攻击。工业控制系统安全至关重要,Janus通过在TEE中运行关键的安全监控模块,能够检测恶意软件对控制器的不当访问和攻击行为。该方案不仅保护检测逻辑本身不被篡改,还确保检测结果的完整性。

**关键贡献**:
- 提出针对工业机器人的TEE安全监控架构
- 实现低开销的运行时攻击检测
- 在真实工业控制器上验证方案有效性

### 2026 - CONFINE: A TEE-based Approach for Preserving Data Secrecy in Process Mining

**摘要**: CONFINE研究在过程挖掘中保护数据机密性的问题。过程挖掘需要分析业务日志来发现流程模式,但日志往往包含敏感信息。本文提出基于TEE的解决方案,允许在不暴露原始数据的前提下进行安全的过程分析。

**关键贡献**:
- 设计保护隐私的过程挖掘框架
- 利用TEE实现数据隔离和分析
- 平衡隐私保护与分析精度

### 2026 - Styx: Collaborative and Private Data Processing With TEE-Enforced Sticky Policy

**摘要**: Styx提出利用TEE强制执行"粘性策略"的数据处理框架。在多方协作场景中,数据需要跨组织流动,但同时需要确保数据使用符合预设策略。Styx通过在TEE中执行策略引擎,确保数据处理过程始终遵循安全策略。

**关键贡献**:
- 提出TEE强制执行的粘性策略概念
- 实现跨组织的安全数据协作
- 提供灵活策略表达能力

---

## 综合分析

这3篇论文代表了TEE在工业系统和数据处理领域的应用:

1. **工业安全**: Janus展示了TEE在工控系统中的实际价值
2. **隐私计算**: CONFINE和Styx关注数据隐私保护,这是TEE的重要应用方向

---

**下载时间**: 2026-04-21
**论文总数**: 3 篇
**年份分布**: 2025年(1篇), 2026年(2篇)
