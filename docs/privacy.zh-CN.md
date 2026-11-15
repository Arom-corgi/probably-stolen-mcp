# 数据与隐私

## 为什么请求网络权限，以及如何自行核对

游戏把套接字访问统一归入名为“访问互联网”的 `network` 权限。beta.3 使用该权限在 `127.0.0.1:20873` 创建 HTTP 监听器，让同机的 MCP 客户端可以发现工具、读取状态并提交游戏动作。这个权限名称描述游戏授予的能力，具体使用方式取决于正在加载的 DLL。

如果你想核实，可以请你信任的 AI 审查自己实际安装的文件：

1. 在模组目录运行 `Get-FileHash .\DeepSeekBridge.dll -Algorithm SHA256`。beta.3 实测 DLL 的 SHA256 为 `DB0495926DEA7BE351A1AD9E2143C5FE95D82B3D9A7793A8A60BED29A85C0DF1`。Release 中 `SHA256SUMS.txt` 的值用于核对整个 ZIP。
2. 用 ILSpy 在本地打开该 DLL，查看 `DeepSeekBridge.NativeMcpHttp` 和它的调用者。可以让 AI 审查反编译代码并指出证据：“它绑定哪个地址？有哪些主动发起的外部连接？哪些游戏数据会被返回、返回给谁？”再看 `manifest.xml` 的权限清单。审查只需模组文件，无需提供存档、账号或密钥。

**English.** The game labels socket access as a network capability. This release uses it to bind to `127.0.0.1:20873` and answer MCP requests from clients on the same PC. To review it yourself, run the hash command above on the installed DLL, then open the DLL locally in ILSpy. Ask a trusted AI to inspect `DeepSeekBridge.NativeMcpHttp` and its callers for bind addresses, outbound connections and returned data. Only the mod files are needed. An AI review can help you inspect the evidence; it is not a security certification.

工坊直连版的游戏进程在 `127.0.0.1:20873/mcp` 接受本机 MCP 客户端的连接，因此游戏会请求模组的网络权限。这个地址仅限运行游戏的电脑，游戏关闭后服务停止。模组同时使用游戏提供的 `persistentDataPath/ModData/deepseek_bridge` 目录保存状态、命令与回执。Windows 默认游戏数据位于 `%USERPROFILE%/AppData/LocalLow/Questing Goose Studio/Probably Stolen`。

使用可选 stdio 桥时，AI 客户端会启动外部 Python 程序，它把 SQLite 记事、玩法资料及动作票据保存在 `%LOCALAPPDATA%/PawnshopHarnessMCP/data`。直接使用游戏内 HTTP MCP 时无需运行它。

本包没有自动上传、遥测或Bug日志发送。你选择的AI/MCP宿主会如何发送游戏工具内容给模型，由该宿主和你配置的模型服务决定。游戏文字、存档编号、物品和对话可能进入该宿主上下文。

The Workshop mod listens on `127.0.0.1:20873/mcp` while the game runs. It requests the game's network capability for this local connection. Your AI client decides which game data it sends to its model provider. The mod does not upload telemetry or bug logs. The optional stdio companion stores its own notes and action records locally.

反馈前手动检查内容。不要上传存档、整个SQLite数据库、`.env`、模型API密钥、Steam令牌、Harness完整配置或个人目录截图。优先只发版本、相关工具与参数、脱敏后的回执及最小前后状态。公开Issues任何人可见。
