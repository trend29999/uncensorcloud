# uncensorcloud — 免费 Windows AI 去除马赛克与本地字幕

**在自己的电脑上用 AI 去除视频马赛克、跟踪移动区域，并生成、翻译和编辑字幕。**

[下载 Windows 免费版](https://uncensorcloud.com/download/free) · [版本与源码](https://github.com/trend29999/uncensorcloud/releases/latest) · [官网](https://uncensorcloud.com) · [English](README.md)

当前版本 **3.5.0**，支持 Windows 10/11 x64。运行库和模型已随便携包提供。视频修复使用本机 NVIDIA GPU，字幕可使用 GPU 或 CPU。视频与字幕文本保留在本机；需要免费验证账号和联网授权，无需支付卡。

## 功能

- AI 去除马赛克：自动检测或手动选择马赛克区域，支持时间线校正、运动跟踪和切镜重置。
- 先做 10 秒预览，比较原片与结果，再导出完整 HEVC/MP4 视频及音轨。
- 可调整时间稳定性、区域增强和低显存设置。
- 本地语音识别、字幕翻译、时间与文本编辑，导出 SRT/VTT 或可切换字幕轨视频。
- 字幕支持英文、简体中文、繁体中文、日文、韩文、西班牙文、葡萄牙文、阿拉伯文。
- 实际 CUDA/NVENC 检查及合成素材测速，帮助估算处理时间。

## 快速上手

1. 下载约 **8.9 GB** 的完整 ZIP，为解压、导入副本及输出预留空间。
2. 完整解压到可写文件夹，双击 `Start-Free.cmd`。
3. 在官网注册或登录免费验证账号，确认桌面授权码，等待设备检查结束。
4. 导入短视频，选择区域尝试 10 秒修复预览；需要字幕时，在有对白的位置尝试 30 秒字幕。
5. 确认效果后处理、导出完整视频。任务完成或取消后，使用 `Stop-Free.cmd` 停止程序。

关闭浏览器不会停止后台任务，原始文件不会被覆盖。[完整桌面指南（英文）](DESKTOP-GUIDE.md)。

## 设备与使用限制

视频修复需要现代 NVIDIA GPU 和兼容 CUDA 13 的驱动。长视频建议 16 GB 显存、32 GB 内存、8 个逻辑 CPU 核心和 50 GB 可用空间；实际兼容性由程序检查，建议先用短片与低显存模式尝试。开发验证使用 RTX 4090 Laptop 16 GB，其他型号未逐一验证。

修复输入暂限偶数尺寸、SDR、8 位视频。字幕 CPU 模式可独立于 GPU 视频修复使用，但仍需联网进行账号验证。重建细节、识别及翻译均为模型估计，应人工检查，不能保证恢复原始信息。

![非人物合成测试图卡](synthetic-demo.jpg)

示例用于验证流程和导出，不代表真实素材效果。[下载合成对比短片](https://github.com/trend29999/uncensorcloud/releases/download/v3.5.0/synthetic-comparison.mp4)。

## 下载、源码和校验

此仓库提供公开下载说明和问题反馈入口。完整对应源码附在 [3.5.0 Release](https://github.com/trend29999/uncensorcloud/releases/tag/v3.5.0)，文件名为 `uncensorcloud-3.5.0-source-full.zip`；也可从 [官网源码入口](https://uncensorcloud.com/download/source) 下载。GitHub 自动生成的仓库 ZIP 只有说明文件，运行程序请下载 Windows 完整包。

Windows 包超过 GitHub 单个 Release 附件 2 GiB 的限制，因此从官网提供。Release 附有 `SHA256SUMS.txt`，解压后可运行 `Verify-Release.cmd`。官网固定下载链接可能更新至新版本，请核对文件名、版本及对应哈希。

## 帮助产品成长

欢迎 **Star**、订阅 Release 更新、分享下载链接，或 [提交问题](https://github.com/trend29999/uncensorcloud/issues/new)。请附版本、GPU/驱动、复现步骤和去除敏感内容的错误信息；不要公开私人视频、登录码和密钥。

[云端工作台](https://uncensorcloud.com/workspace) 是可选的独立服务，提供预览和付费完整视频处理。本地版不会自动上传本地视频。

引擎和衍生应用保留 **AGPL-3.0**；依赖和模型各自保留原许可。感谢 Jasna、Lada、Whisper、Faster Whisper、CTranslate2、M2M100 等上游作者。[许可证](LICENSE) · [第三方声明](THIRD-PARTY-NOTICES.md) · [品牌说明](BRAND-NOTICE.md)。
