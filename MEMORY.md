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

### 2026-04-08 下午批次
- **13 篇新论文**下载至 `/tmp/tee_paper/2026-04-08-15-50-00/`，涵盖 BadRAM、CipherSteal、PORTAL、ASGARD、PALANTÍR、The Road to Trust、DORAMI、TETD、TEEcorrelate、TELESCOPE、Mole、EXIA、SNPeek
- 9 个旧重复文件从早期目录删除（保留最新下载版本）
- `/tmp/tee_paper/2026-04-08-14-50-00/README.md` 补写完成（2 篇论文）

### 2026-04-03 session (12:13 PM)
- 5 new IACR ePrint papers (2025-2026) - all TEE-focused: Defeating AutoLock (TrustZone cache attack), Intel TDX side-channels, Nested Attestation for serverless, Leaderless BFT consensus, SCALE-FL federated learning. Git push successful (commit 121086c). Total size 12MB.
