# 星际掌柜｜深空当铺 MCP

版本：0.6.0-beta.2。项目：https://github.com/Arom-corgi/probably-stolen-mcp。反馈：https://github.com/Arom-corgi/probably-stolen-mcp/issues。

游戏模组读取店里的商品、交易和客人，配套服务把这些信息以文字交给你的 AI。两者安装在运行游戏的同一台 Windows 电脑上。支持启动本地 stdio MCP 服务的 AI 客户端都可以接入，无需安装 DeepSeek Harness 插件。

## 安装（Windows）

1. **游戏模组二选一**。在 Steam 订阅，或从同版 GitHub Release 下载文件名含 `mod-windows` 的 ZIP，解压到游戏目录下的 `Mods/DeepSeekBridge/`，让 `manifest.xml` 直接位于该文件夹内。任选一种后，在游戏模组菜单启用 AI MCP Gameplay Bridge 并重启。本地同 ID 模组会被优先加载。[Steam 创意工坊](https://steamcommunity.com/sharedfiles/filedetails/?id=3840057532)
2. **想让 AI 接手时**，两种安装方式都要从 https://github.com/Arom-corgi/probably-stolen-mcp/releases/tag/v0.6.0-beta.2 下载同版本的 Python 桥接程序（文件名含 `client-windows`），解压到游戏和工坊目录之外。只想手动游玩时可以停在第 1 步。
3. 安装Python 3.11+（本包在Python 3.12测试，无需pip依赖）。双击 `install-client.cmd`，或PowerShell运行 `configure-client.ps1`。它自动找Python，将精选客户端文件校验后复制到 `%LOCALAPPDATA%/PawnshopHarnessMCP/client`，状态放在旁边的`data`目录。
4. 打开安装目录里的 `mcp-config.json`。在你的 AI 客户端添加名为 `pawnshop` 的本地 stdio 服务，填写其中的 `command` 和 `args`，或使用客户端的 JSON 导入功能。使用 DeepSeek Harness 的玩家也可沿用安装器对已有 Desktop/Web 配置的自动设置。希望只生成通用配置时，可运行 `configure-client.ps1 -NoHarness`。
5. 在MCP客户端重连，先调用`game_status`核对已连接、模组版本与游戏版本，再读`game_actions`。测试用自己的副本存档；游戏决定实际结果及自动保存。

自检：在外部客户端目录运行 `python -B launcher.py --self-test`。只跑模拟stdio协议，不操作真实游戏。

## 日常使用

先`game_status`和`game_actions`，只按本帧绑定`game_do`，每次写入后重新观察。旧session/revision必须拒绝；unknown不是失败证明，不能换请求ID盲重试。人工接管时停止MCP客户端调度；桥本身不会自行开始下一步。

开门前查`game_calendar`、库存与`game_strategy(plan="display")`；有货想卖时陈列商品，想进货先`game_item`读灯牌原文。单件说明保留操作、功效、动态数据与价格，排除游戏自身灰斜体风味文。不要把NPC报价、UI基础价与原始内部字段混用。查看资料后用`game_read_and_close`归档并关窗回读；当天报纸只在确切实例已读并确认关窗后，按`newspaper_disposal`指引投桶，再核对位置。

鉴定走正常装备放大镜→目标→填写→原生提交。三类原生正确基准和分项独立于普通交易估价；缺条件时unknown。安全检查、清洁与过夜仍依据当前客人、完整垃圾桶和原生费用确认。

拾荒先选可用包，读当前地面、口袋和嵌入包格；按`afterhours_option`中的`pack_one`装一件，再回读实际ID和位置。`layout=inline`表示原生嵌入格已经可见，不要求独立打开/关闭。满口袋可否装包、形状和容量以当前绑定为准。返回后逐个核对刚记录的实例ID，不用相同名称代替。空间不足拒绝不能当成已装入。

## 兼容与边界

本机研究/历史实测对象为Windows Steam正式本体100-Rev13，旧API报告0.46D。其它游戏更新、平台、职业及Mod组合未验证。beta.2冻结DLL已完成下列原生改造体事件现场测试；其它功能与环境仍需公测，不把单分支测试当成全覆盖。默认文字版只用游戏自带ModData文件API，不含屏幕图像能力。

`CAPABILITIES.zh-CN.md`区分已有现场证据、本地回归和待测内容。没有通关或周日买房保证。客户端、原生模组与游戏版本不匹配时先核对版本和路径，勿通过绕过游戏扫描或反复点击处理。

卸载：移除MCP配置中的独立pawnshop条目，并在游戏Mods页取消订阅/停用。外部客户端与data目录独立保留，按自己需要备份或删除；安装器不删存档。


## beta.2 当前原生改造体事件

已实测冻结DLL SHA256：`42A82580012F53D4C32409725B4AA222DFB3AF9432BEF81886C11A2E02C33C21`。16号副本第41天第二时间线visit15：外显“小偷”、内部aug_material、原生is_aug=true、tier=2、未扫描；take→ready→confirm后原生自动收起，安保原文“看来这确实是个改造体”。实际OnGoodKill生成sec_slip2587，报告原文记129信用点已入账、改造体被消灭。无需对白补丁。此证据只覆盖该次原生分支，其它分支仍待公测。

联合路线（尚未实测）：适合出售且当前顾客预算已知时，可先选货成交，再处理该次原生事件。为避免花光预算后客人离开，选原生整单报价严格小于当前剩余预算的组合并留正余额（预算100时80可，100不可）；报价或预算未知、无法留余额则跳过此交易，不强求卖货。按实际现金、离柜实例和回读预算记账；成交后重新读取同一session/visit且原生is_aug仍true、当帧绑定有效才可继续事件。客人离开即结束，禁止把旧绑定用于下一人。这是此联合路线的策略，不限制普通买家的正常成交。
