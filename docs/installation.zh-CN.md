# 星际掌柜｜深空当铺 MCP

版本：0.6.0-beta.3。项目：https://github.com/Arom-corgi/probably-stolen-mcp。反馈：https://github.com/Arom-corgi/probably-stolen-mcp/issues。

游戏模组读取店里的商品、交易和客人，将结果以文字交给你自己的 AI 客户端。游戏和 AI 客户端在同一台电脑运行时可以直接连接。

## 安装（Windows）

1. **游戏模组二选一**。在 Steam 订阅，或从同版 GitHub Release 下载文件名含 `mod-windows` 的 ZIP，解压到游戏目录下的 `Mods/DeepSeekBridge/`，让 `manifest.xml` 直接位于该文件夹内。任选一种后，在游戏模组菜单启用 星际掌柜｜深空当铺 MCP 并重启。本地同 ID 模组会被优先加载。[Steam 创意工坊](https://steamcommunity.com/sharedfiles/filedetails/?id=3840057532)
2. **连接游戏内 MCP**。确认游戏提示的网络权限。在本地 AI 客户端添加名为 `pawnshop` 的服务，传输选 **Streamable HTTP**，填入 `http://127.0.0.1:20873/mcp`。保存后，保持游戏开着。使用直接连接无需安装 Python 或下载桥接程序。
3. 调用 `game_status` 核对连接和模组版本，再读 `game_actions`。要实际交易或过夜时，用自己的存档副本测试。AI 客户端和模型由玩家自行提供。云端 AI 客户端需有能访问本机的连接器。

**English.** Subscribe on [Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=3840057532), enable **星际掌柜｜深空当铺 MCP**, approve the network capability and restart the game. In an AI client on the same PC, add a **Streamable HTTP** server at `http://127.0.0.1:20873/mcp`. The Workshop subscription installs the game-side server. Bring your own AI client and model. No Python or companion download is needed for this connection.

游戏提示的“访问互联网”权限用于在 `127.0.0.1:20873` 接收同机 AI 客户端的请求。本版模组不会主动连接模型提供商或上传存档。你也可以校验安装的 DLL，并让 AI 审查它的反编译代码。[权限说明、SHA256 与审查步骤 / Permissions, checksum and AI review](https://github.com/Arom-corgi/probably-stolen-mcp/blob/master/docs/privacy.zh-CN.md)

### 可选的 stdio 连接

仅支持本地 stdio 的客户端或需要外部 SQLite 记事的玩家，可以从 https://github.com/Arom-corgi/probably-stolen-mcp/releases/tag/v0.6.0-beta.3 下载同版配套程序（文件名含 `client-windows`）。安装 Python 3.11 或更新版本，将 ZIP 解压到游戏目录外，双击 `install-client.cmd`。安装目录默认为 `%LOCALAPPDATA%/PawnshopHarnessMCP/client`。在 AI 客户端中使用生成的 `mcp-config.json` 的 `command` 和 `args`。使用 DeepSeek Harness 时还可沿用安装器对已有 Desktop/Web 配置的自动设置。两种传输可在主机中择一启用，避免给模型两套同名工具。

自检：在外部客户端目录运行 `python -B launcher.py --self-test`。只跑模拟stdio协议，不操作真实游戏。

## 日常使用

连接后先查看客户端列出的工具。工坊直连提供当下游戏状态、物品、来客、可用动作以及执行回执。`game_capabilities` 列出直连版覆盖范围。下面提到的长期 SQLite 记事、跨次游戏知识库和 `game_strategy` 聚合建议属于可选 stdio 版本。

先`game_status`和`game_actions`，只按本帧绑定`game_do`，每次写入后重新观察。旧session/revision必须拒绝；unknown不是失败证明，不能换请求ID盲重试。人工接管时停止MCP客户端调度；桥本身不会自行开始下一步。

开门前查`game_calendar`、库存与`game_strategy(plan="display")`；有货想卖时陈列商品，想进货先`game_item`读灯牌原文。单件说明保留操作、功效、动态数据与价格，排除游戏自身灰斜体风味文。不要把NPC报价、UI基础价与原始内部字段混用。查看资料后用`game_read_and_close`归档并关窗回读；当天报纸只在确切实例已读并确认关窗后，按`newspaper_disposal`指引投桶，再核对位置。

鉴定走正常装备放大镜→目标→填写→原生提交。三类原生正确基准和分项独立于普通交易估价；缺条件时unknown。安全检查、清洁与过夜仍依据当前客人、完整垃圾桶和原生费用确认。

拾荒先选可用包，读当前地面、口袋和嵌入包格；按`afterhours_option`中的`pack_one`装一件，再回读实际ID和位置。`layout=inline`表示原生嵌入格已经可见，不要求独立打开/关闭。满口袋可否装包、形状和容量以当前绑定为准。返回后逐个核对刚记录的实例ID，不用相同名称代替。空间不足拒绝不能当成已装入。

## 兼容与边界

本机研究/历史实测对象为Windows Steam正式本体100-Rev13，旧API报告0.46D。其它游戏更新、平台、职业及Mod组合未验证。beta.2冻结DLL已完成下列原生改造体事件现场测试；其它功能与环境仍需公测，不把单分支测试当成全覆盖。工坊文字版使用游戏提供的 ModData 文件 API，并在回环地址提供 HTTP MCP 服务。它不采集屏幕图像。仍使用 beta.2 的玩家应从该版本发布页下载匹配的 stdio 配套程序。

`CAPABILITIES.zh-CN.md`区分已有现场证据、本地回归和待测内容。没有通关或周日买房保证。客户端、原生模组与游戏版本不匹配时先核对版本和路径，勿通过绕过游戏扫描或反复点击处理。

卸载：移除MCP配置中的独立pawnshop条目，并在游戏Mods页取消订阅/停用。外部客户端与data目录独立保留，按自己需要备份或删除；安装器不删存档。


## beta.2 当前原生改造体事件

已实测冻结DLL SHA256：`42A82580012F53D4C32409725B4AA222DFB3AF9432BEF81886C11A2E02C33C21`。16号副本第41天第二时间线visit15：外显“小偷”、内部aug_material、原生is_aug=true、tier=2、未扫描；take→ready→confirm后原生自动收起，安保原文“看来这确实是个改造体”。实际OnGoodKill生成sec_slip2587，报告原文记129信用点已入账、改造体被消灭。无需对白补丁。此证据只覆盖该次原生分支，其它分支仍待公测。

联合路线（尚未实测）：适合出售且当前顾客预算已知时，可先选货成交，再处理该次原生事件。为避免花光预算后客人离开，选原生整单报价严格小于当前剩余预算的组合并留正余额（预算100时80可，100不可）；报价或预算未知、无法留余额则跳过此交易，不强求卖货。按实际现金、离柜实例和回读预算记账；成交后重新读取同一session/visit且原生is_aug仍true、当帧绑定有效才可继续事件。客人离开即结束，禁止把旧绑定用于下一人。这是此联合路线的策略，不限制普通买家的正常成交。
