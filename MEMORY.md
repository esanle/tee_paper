你使用 openclaw profile 控制的 chrome 浏览器，每次打开浏览器都要静默操作，不要尝试夺取焦点

对于每个视频：
* 优先通过本地 yt-dlp工具获取字幕，获取不到则使用 yt-dlp 下载音频然后whisper-cli 命令行(模型在 /opt/homebrew/Cellar/whisper-cpp/1.8.3/share/whisper-cpp/models) 注意我是中文用户，用中文解读

whisper-cpp 任务转写前注意看看空闲内存够不够4g，不要把系统打挂


## TEE Paper Collection (/tmp/tee_paper/)

- GitHub repo: https://github.com/esanle/tee_paper.git
- Papers stored in /tmp/tee_paper/<timestamp>/ directories
- Each directory has README.md with summaries
- Naming: "YYYY - Paper Title.pdf"
- Key conferences: USENIX Security, IEEE S&P, NDSS, CCS, ESORICS
- Download sources: arXiv (优先), USENIX (直接PDF), Semantic Scholar OA, IACR ePrint

### 2026-04-16 上午批次（10:55 NZST）
- **1 篇新论文**下载至 `/tmp/tee_paper/2026-04-16-10-55-46/`：DORAMI (arXiv 2410.03653, RISC-V TEE SM 权限分离)
- Game of Arrows, Phantom, TEEcorrelate, TensorShield 均已在以往批次中收录（重复），已删除当前目录副本
- 现有 327 篇论文去重后确认无其他重复
- README.md 包含 DORAMI 摘要（1000字）+ 与同期论文横向对比综述
- Git push: 见本批次 commit

### 2026-04-16 凌晨批次（7:54 AM NZT）
- 确认现有集合完整性：无新论文收录（arXiv 40 篇验证全部已收录）
- README.md 新增（说明无新论文）
- Git push 成功

### 2026-04-15 下午批次
- 收录 JANUS (NDSS 2026 远程认证) + CCxTrust (协作信任)
- Git push 成功

### 历次去重记录
- 2026-04-16-10-55: 删除 Game of Arrows, Phantom, TEEcorrelate, TensorShield 当前目录副本（已存于 2026-04-13-07-47-53、2026-04-12-18-42-28、2026-04-16-06-16-08）
- 2026-04-12: 批量删除 56 个重复 PDF（保留最旧时间戳副本）
- 2026-04-08: 删除 9 个旧重复文件

### 已知问题
- ACM DL / IEEE S&P / CCS 2025 需机构订阅，curl 下载返回 403
- USENIX Security 论文可直接下载（开源）
- ASGARD (NDSS 2025) PDF 链接失效，建议通过作者或机构获取
