
## 输入——涉及 LLM 在 TEE 中执行/推理的论文列表

这些论文在当前 tee_paper 目录下

### 1. **TZ-LLM: Protecting On-Device Large Language Models with Arm TrustZone**

- **作者**: Xunjie Wang, Jiacheng Shi, Zihan Zhao, et al.
- **来源**: arXiv:2511.13717 (EUROSYS 2026)
- **概述**: 使用 Arm TrustZone 保护移动设备上的 LLM，提出"流水线恢复"和"协同驱动设计"技术

### 2. **Trustworthy and Controllable Professional Knowledge Utilization in Large Language Models with TEE-GPU Execution**

- **作者**: Yifeng Cai, Zhida An, Yuhan Meng, et al.
- **来源**: arXiv:2512.16238 (2025)
- **概述**: PKUS 框架，将专业知识编码为适配器在 TEE 中执行，GPU 用于加速

### 3. **Optimistic TEE-Rollups: A Hybrid Architecture for Scalable and Verifiable Generative AI Inference on Blockchain**

- **作者**: Aaron Chan, Alex Ding, Frank Chen, et al.
- **来源**: arXiv:2512.20176 (2025)
- **概述**: 使用 NVIDIA H100 Confidential Computing TEE 进行区块链上的 LLM 推理验证

### 4. **Vulnerabilities in Partial TEE-Shielded LLM Inference with Precomputed Noise**

- **来源**: 2026
- **概述**: 探讨部分 TEE 屏蔽 LLM 推理的漏洞

### 5. **Confidential LLM Inference Performance and Cost Across CPU and GPU TEEs**

- **年份**: 2025
- **概述**: 分析在不同 TEE 平台上运行 LLM 推理的性能和成本权衡

### 6. **Amulet: Fast TEE-Shielded Inference for On-Device Model Protection**

- **作者**: Zikai Mao, Lingchen Zhao, Lei Xu, et al.
- **来源**: arXiv:2512.07495 (2025)
- **概述**: 在设备上使用 TEE 保护 LLM 模型的框架，结合 GPU 加速

### 7. **DistilLock - Safeguarding LLMs from Unauthorized Knowledge Distillation on the Edge**

- **作者**: Asmita Mohanty, Gezheng Kang, Lei Gao, Murali Annavaram
- **来源**: arXiv:2510.16716 (NeurIPS 2025 Workshop)
- **概述**: 使用 Intel SGX TEE 进行边缘设备上的隐私保护知识蒸馏

### 8. **Fastrack - Fast IO for Secure ML using GPU TEEs**

- **作者**: Yongqin Wang, Rachit Rajat, Jonghyun Lee, et al.
- **来源**: arXiv:2410.15240 (2024)
- **概述**: 优化 GPU TEE 中 CPU-GPU 通信，提升 ML 推理性能

### 9. **No Privacy Left Outside - On the In-Security of TEE-Shielded DNN Partition for On-Device ML**

- **作者**: Ziqi Zhang, Chen Gong, Yifeng Cai, et al.
- **来源**: arXiv:2310.07152 (IEEE S&P 2024)
- **概述**: 研究 TEE 屏蔽的 DNN 分区安全问题，提出 TEESLICE 解决方案

### 10. **TensorTEE - Unifying Heterogeneous TEE Granularity for Efficient Secure Collaborative Tensor Computing**

- **作者**: Husheng Han, Xinyao Zheng, Yuanbo Wen, et al.
- **来源**: arXiv:2407.08903 (ASPLOS 2024)
- **概述**: 异构 TEE 设计用于 CPU-NPU 协作计算，提升 LLM 训练性能 4.0×

### 11. **Performance of Confidential Computing GPUs** (Llama-3.1-8B, gemma-7b, granite-7b-base 测试)

- **作者**: Antonio Martínez Ibarra, Julian James Stephen, et al.
- **来源**: arXiv:2505.16501 (IEEE 2025)
- **概述**: 在 NVIDIA H100 机密计算 GPU 上测试 LLM 推理性能

### 12. **Spore in the Wild - A Case Study of Sovereign AI Agents on TEE-Secured Blockchains**

- **作者**: Botao Amber Hu, Helena Rong
- **来源**: arXiv:2506.04236 (ALIFE 2025)
- **概述**: 在 TEE 保护的区块链上部署自主 LLM 代理的案例研究


# 输出

`tee_tcb_for_llm/README.md`

要求确认下，现在主流 paper 中， TEE 下如果要把 LLM 推理部分放进来，需要LLM 推理那部分放在  TEE

，哪部分在REE
