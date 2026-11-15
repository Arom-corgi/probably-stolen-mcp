# 星际掌柜｜深空当铺 MCP

让你的 AI 经营《深空当铺：可能是偷的》。它可以读出灯牌会吸引哪类客人，摆好展示柜，把一批商品卖给同一个买家，也能带着背包去垃圾场进货。游戏内的文字、价格和鉴定数据通过 MCP 直接传给 AI。

支持启动本地 **stdio MCP** 服务的 AI 客户端都可以接入，无需安装 DeepSeek Harness 插件。配套下载包里是 Python 桥接程序，由你选的 AI 客户端启动。只订阅模组也可以照常手动玩，AI 会在客户端连上并发出操作后才接手。

**当前公开版 beta.2** 仍需要配套桥接程序才能让 AI 操作。游戏内直接提供 HTTP MCP 的版本正在开发。MCP 也不包含模型或模型额度。今后的直连版仍需要玩家在支持 Streamable HTTP 的本地 AI 客户端中添加一次服务地址。云端客户端需要能访问玩家电脑的连接器。

## 开始公测

**安装游戏模组，二选一。**

- **Steam 工坊**　订阅，等待下载完成。[订阅模组](https://steamcommunity.com/sharedfiles/filedetails/?id=3840057532)
- **GitHub 手动安装**　下载文件名含 `mod-windows` 的 ZIP，解压至游戏目录下的 `Mods/DeepSeekBridge/`，使 `manifest.xml` 直接位于该文件夹内。[下载模组](https://github.com/Arom-corgi/probably-stolen-mcp/releases)

任选一种后，在游戏模组菜单启用 **AI MCP Gameplay Bridge** 并按提示重启。

**让 AI 接手，两种方式共用这一步。** 下载与模组同版本、文件名含 `client-windows` 的 Python 桥接程序，解压到游戏目录之外。安装 Python 3.11 或更新版本，双击 `install-client.cmd`。在自己的 AI 客户端添加名为 `pawnshop` 的本地 stdio 服务，填写生成的 `mcp-config.json` 里的 `command`、`args`，然后重连。可以先问「我现在是几号档、第几天、现金多少？」[下载桥接程序](https://github.com/Arom-corgi/probably-stolen-mcp/releases)

## English

**Star Shopkeeper** lets an AI read prices, talk to customers and run your shop in *Probably Stolen*.

**The public beta.2 release requires the companion bridge for AI control.** An in-game HTTP MCP server is in development. Bring your own AI client and model access. With the direct connection, you will still add the server URL once in a local AI client that supports Streamable HTTP. A cloud-hosted client needs a connector on your PC.

**Choose one way to install the game mod.**

- **Steam Workshop** — Subscribe and wait for the download. [Workshop item](https://steamcommunity.com/sharedfiles/filedetails/?id=3840057532)
- **Manual installation** — Download the ZIP with `mod-windows` in its name. Extract its files into `Mods/DeepSeekBridge/` under the game directory, with `manifest.xml` directly inside that folder. [Releases](https://github.com/Arom-corgi/probably-stolen-mcp/releases)

Enable **AI MCP Gameplay Bridge** in the in-game Mods menu and restart. You can now play by hand.

**To let an AI play**, install Python 3.11 or later on the same Windows PC. Download the matching ZIP with `client-windows` in its name, extract it outside the game directory and run `install-client.cmd`. In an AI client that can launch local stdio MCP servers, add a server named `pawnshop` using the `command` and `args` from the generated `mcp-config.json`. Reconnect and ask for the save slot, day and cash balance before enabling further actions. DeepSeek Harness is optional. [Download the bridge](https://github.com/Arom-corgi/probably-stolen-mcp/releases)

## 参与测试

欢迎反馈安装失败、窗口关不掉或成交数量不符等问题。请写上 AI 客户端、模组版本，以及操作前后实际发生了什么。物品已经移动、现金已经变化时，保留现场即可。[提交 BUG](https://github.com/Arom-corgi/probably-stolen-mcp/issues/new/choose)

[安装与卸载说明](docs/installation.zh-CN.md) · [实测与待测范围](docs/capabilities.zh-CN.md) · [隐私说明](docs/privacy.zh-CN.md)
