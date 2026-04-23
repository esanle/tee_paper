# TEE 论文综述 - 2026-04-21-16-57-20

本目录为本次任务执行记录。

---

## 下载结果

本次任务通过 Semantic Scholar 搜索 2025+ 年可信执行环境（TEE）相关论文，成功下载了 2 篇 PDF：

1. **Janus: A Trusted Execution Environment Approach for Attack Detection in Industrial Robot Controllers** (IEEE TETC 2025)
2. **Secure phasing of private genomes in a trusted execution environment with TX-Phase** (Genome Research 2025)

然而，经去重检查发现，Janus 和 TX-Phase 均已存在于 `2026-04-21-16-46-01` 目录中，本 session 予以删除，不做重复存储。

---

## 下载平台说明

| 平台 | 结果 |
|------|------|
| IEEE Xplore | ✅ 直接 PDF 链接可用 |
| Semantic Scholar PDF | ✅ 直链可用 |
| ACM Digital Library | ❌ Cloudflare 拦截 |
| arXiv | ❌ 网络访问异常 |
| Google Scholar | ❌ 人机验证拦截 |
| MDPI / Springer | ❌ 403 禁止访问 |

---

## Janus 论文摘要

Janus 是 Polito 团队（Politecnico di Milano）发表在 IEEE TETC 2025 的论文，提出利用 TEE 技术（如 Arm TrustZone）保护工业机器人控制器上的攻击检测算法完整性。在传统 IDS 依赖主机软件安全、攻击者可破坏的背景下，Janus 将检测逻辑运行在 TEE 安全世界，即使控制器软件被完全攻陷，攻击检测能力仍保持完整。论文采用状态观测器（state observer）策略检测低层控制器攻击，在 Matlab/Simulink 仿真和真实 TrustZone 开发板上验证了方法的有效性，且不引入显著计算开销。

---

## TX-Phase 论文摘要

TX-Phase 是 Yale/NCI/UCSD 团队发表在 Genome Research 2025 的论文，提出首个基于 TEE 的隐私保护基因组单倍型 phasing 方法。基因型插补（genotype imputation）是 genomics 社区的重要工具，但 phasing 算法的高复杂性使得在隐私约束下维持实用性能极具挑战。TX-Phase 通过压缩参考面板（compressed reference panels）和动态定点算术（dynamic fixed-point arithmetic）两项创新技术全面缓解侧信道泄漏，在 UK Biobank 和 Haplotype Reference Consortium 数据集上验证了精度和实用性，为更广泛的科研社区打开了访问大型参考基因组数据集的安全通道。

---

*本综述基于 2026-04-21-16-57-20 本次下载的论文编写。Janus 和 TX-Phase 完整版请参见 `2026-04-21-16-46-01/README.md`。*
