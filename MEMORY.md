你使用 openclaw profile 控制的 chrome 浏览器，每次打开浏览器都要静默操作，不要尝试夺取焦点


对于每个视频：
* 优先通过本地 yt-dlp工具获取字幕，获取不到则使用 yt-dlp 下载音频然后whisper-cli 命令行(模型在 /opt/homebrew/Cellar/whisper-cpp/1.8.3/share/whisper-cpp/models) 注意我是中文用户，用中文解读

whisper-cpp 任务转写前注意看看空闲内存够不够4g，不要把系统打挂

