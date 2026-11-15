# 数据与隐私

模组通过游戏自己的`persistentDataPath/ModData/deepseek_bridge`读写状态、命令与回执。Windows默认游戏数据位于`%USERPROFILE%/AppData/LocalLow/Questing Goose Studio/Probably Stolen`，重定向目录可在MCP参数中显式指定。外部程序只连接这个本机文件桥，不需要开放公网端口。

外部客户端的SQLite记事、玩法资料及动作票据在`%LOCALAPPDATA%/PawnshopHarnessMCP/data`；不放在会被Steam更新覆盖的工坊内容目录。游戏模组不启动外部程序，必须由玩家自己的MCP客户端启动它。

本包没有自动上传、遥测或Bug日志发送。你选择的AI/MCP宿主会如何发送游戏工具内容给模型，由该宿主和你配置的模型服务决定。游戏文字、存档编号、物品和对话可能进入该宿主上下文。

反馈前手动检查内容。不要上传存档、整个SQLite数据库、`.env`、模型API密钥、Steam令牌、Harness完整配置或个人目录截图。优先只发版本、相关工具与参数、脱敏后的回执及最小前后状态。公开Issues任何人可见。
