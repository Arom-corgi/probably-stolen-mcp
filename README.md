# 星际掌柜｜深空当铺 MCP

让 AI 在《深空当铺：可能是偷的》当店主。游戏模组在本机提供 MCP 服务，AI 可以读取店况、客人和柜台当前可执行的动作，并按游戏规则操作。

## 从 Steam 工坊开始

1. 订阅模组，在游戏「模组」菜单启用 **星际掌柜｜深空当铺 MCP**。确认网络权限并按提示重启游戏。MCP 服务只监听本机。[Steam 创意工坊](https://steamcommunity.com/sharedfiles/filedetails/?id=3840057532)
2. 在这台电脑上的 AI 客户端添加自定义 MCP 服务，名称填 `pawnshop`，传输选 **Streamable HTTP**，地址填 `http://127.0.0.1:20873/mcp`。保存并连接。DeepSeek Harness 中对应的配置字段是 `transport: streamable-http` 和 `url`。
3. 在副本上试一句「现在是第几号存档、第几天、现金多少？窗口前的客人刚才说了什么？」核对档位后再让 AI 交易或过夜。

工坊订阅提供游戏端所需的完整程序，直连时无需安装 Python、下载桥接 ZIP 或运行安装脚本。游戏启动后服务才在线。模型和模型额度由你自己的 AI 客户端提供，首次需要在该客户端指定服务地址。只在云端运行的客户端需要能访问本机的连接器；只支持 stdio 的客户端可选用配套程序。历史版 beta.2 使用 stdio 配套程序。[各版本与可选下载](https://github.com/Arom-corgi/probably-stolen-mcp/releases)

也可以手动安装游戏模组：从 Releases 下载文件名含 `mod-windows` 的 ZIP，解压到游戏目录下的 `Mods/DeepSeekBridge/`，让 `manifest.xml` 位于该文件夹内。Steam 订阅和 GitHub 手动安装二选一。已手动安装过时请核对游戏显示的版本，本地同 ID 模组会优先加载。

## 为什么需要「访问互联网」权限

游戏将网络套接字统一归为 `network`。模组用这个权限监听 `127.0.0.1:20873`，在同一台电脑上响应 AI 客户端的 MCP 请求。本版模组不会主动连接模型服务或上传存档；若使用云端模型，AI 客户端可能将工具结果发给该模型。如果你想核实，可用 ILSpy 打开安装的 DLL，请你信任的 AI 检查监听地址、主动对外连接及数据内容。[核对 SHA256 与 AI 审查步骤](docs/privacy.zh-CN.md)

## English

**Star Shopkeeper** lets an AI read your shop, customers and available actions in *Probably Stolen* and play through the game’s own controls.

1. Subscribe on Steam Workshop. Enable **星际掌柜｜深空当铺 MCP** in the in-game Mods menu, approve the network capability and restart when prompted. The game hosts a local MCP server. [Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=3840057532)
2. In an AI client on the same PC, add a custom server named `pawnshop`, choose **Streamable HTTP** and enter `http://127.0.0.1:20873/mcp`. Save and connect.
3. Use a copied save. Ask for the save slot, day, cash balance and the current customer’s last line before letting the AI trade or advance the day.

The subscription supplies the entire game-side server. The direct connection requires no Python, bridge download or installer. Bring your own AI client and model access, and add the URL once in that client. The endpoint is online while the game is running and accepts connections only from the same PC. Cloud-hosted agents need a local connector. For a stdio-only client, use the optional bridge; beta.2 always requires it. [Releases and optional downloads](https://github.com/Arom-corgi/probably-stolen-mcp/releases)

For manual installation, extract the `mod-windows` ZIP into `Mods/DeepSeekBridge/` under the game directory, with `manifest.xml` directly inside that folder. Choose either this method or Workshop. A local copy with the same mod ID takes precedence over Steam’s copy.

**Why network access?** The game groups sockets under its network permission. The mod uses a loopback listener on `127.0.0.1:20873` to answer requests from your local AI client. This release does not connect to a model provider or upload saves. A cloud-model client may forward tool results. If you would like to verify this, inspect your installed DLL in ILSpy and ask a trusted AI to review the decompiled code, listening address, outbound connections and data flow. [Hash and review steps](docs/privacy.zh-CN.md)

## 公测反馈 · Report a bug

请附上 AI 客户端、游戏与模组版本、最短重现步骤以及实际结果。Include your AI client, game and mod versions, steps and the observed result. [提交 BUG / Report a bug](https://github.com/Arom-corgi/probably-stolen-mcp/issues/new/choose)

[安装说明](docs/installation.zh-CN.md) · [实测范围](docs/capabilities.zh-CN.md) · [隐私说明](docs/privacy.zh-CN.md)
