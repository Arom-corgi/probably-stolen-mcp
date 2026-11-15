# 公测能力与验收范围

## beta.3 工坊直连实测 · Direct MCP test

待发布的文字版 DLL、清单和配套工坊文件通过了游戏官方加载器。日志显示 `running=True`、`trust=Updated`，仅声明 `network`。测试时将同一套文件装在本地 Mods 目录。发行 DLL 的 SHA256 为 `DB0495926DEA7BE351A1AD9E2143C5FE95D82B3D9A7793A8A60BED29A85C0DF1`。

Terra 仅用官方 MCP SDK 经 HTTP 发现 15 个工具，从主菜单载入 16 号副本。资料未关时，打开电话的请求被拒绝；读完并关闭名片和档案箱后，手拨 8376 接通助手。升级目录的选中项从空变为“水资源交易”（费用 600），滚动位置从 1 到 0.300000072 再回到 1，关闭目录后电话也已关闭。整个流程没有启动 Python 桥、购买或跨日，最终为第 43 天早晨、现金 700。

The release DLL and Workshop manifest were loaded from the local Mods folder and tested through the official MCP SDK. All 15 tools were discovered. The test loaded slot 16 over HTTP, read and closed the card, dialed Joe’s assistant, selected Water Trader (600) and scrolled down and back. It ended on day 43 with 700 credits. No Python companion was run.

## 电话与升级目录

16 号副本第 43 天，测试用游戏内电话手动拨出 **8376**，接听者为「乔·王尔德的助手」。名片上的号码印在 `card_wild` 图像中，原生文字字段只提供姓名和「随时为您效劳」。数字来自玩家截图核对后的转录，只有读到匹配的名片才提供；返回的来源标签为 `artwork_transcription`。未识别的名片保留未知。已验证关闭名片与档案箱后仍能从本局已读记录取号。

通过电话对话打开目录后，当天可见「水资源交易」费用 600，「水产养殖」费用 800 且前置为水资源交易。该次浏览使用测试副本，现金为 700，全程未购买升级。这个结果来自 stdio 实机测试。

The digits **8376** are printed on Joe’s card artwork. The card’s native text supplies the name and tagline. For this verified artwork the tool returns a player-checked transcription marked `artwork_transcription`. A live stdio test on day 43 confirmed that the card and archive closed, the number remained available, the assistant answered a manual call, and the upgrade catalog opened. The test did not buy an upgrade.

以下表格记录早期版本积累的实机证据和仍待测试的分支。本页另列 beta.2 与 0.6.0-beta.3 的具体实测范围。

| 能力 | 已有证据 | 本版仍需公测 |
| --- | --- | --- |
| MCP连接与正常动作 | stdio、session/revision、回执去重、未知结果先观察已有本地回归与现场经营使用 | 新电脑发现路径、客户端配置、断线恢复、当前发行DLL的游戏扫描 |
| 经营/资料 | 当前客人、报价方向、库存、资料读关、日切已有现场记录 | 所有特殊客人、事件分支、生产链和不同Mod组合 |
| 精准说明/展示 | 灯牌与普通物品单件原文、展示柜和普通交易历史现场核对 | 全部动态设备与新游戏版本；商品/灯牌效果不保证下一客人 |
| 日历/报纸 | 原生只读事件查询、日期事件回调、按日原文缓存有代码和回归覆盖 | 新发行现场读详页/关窗/报纸确切来源；空已知事件不等于没有隐藏效果 |
| 工具/鉴定 | 真实工具箱绑定和当前放大镜对象；三类原生基准与分项；正常提交路径有现场使用 | 所有工具、模态、重绑与异步边界；不承诺全部职业 |
| 嵌入包格/满口袋装包 | 第40夜：包467出门18空格，工具箱27保留；口袋2411垃圾/2412螺丝占满；地面2413垃圾走pack_one入包后18→12空格；回店同ID2413在item:467:0，2411/2412在back_counter | 本发行不同包形、容量不足拒绝、叠堆拆分后ID变化等现场分支；不以别的作者实测冒充本项目实测 |
| 容量不足与未知结果 | 原生空间/形状门禁及模拟拒绝覆盖；unknown位置回读不改成功状态 | 自己的容量不足现场拒绝与物品不变证据；投桶后NullReference历史个案待复核 |
| 清洁/交换 | 完整桶核对与非空容器保护、原生兑换条目读取有回归与部分现场记录 | 不同兑换输入/实际次日产物、负面状态及生产盈利闭环 |

历史现场补充：已读取日历事件修正文`-35%`并正常关窗；转换器一次匹配元件操作曾读回单位电费`1.50→1.40`。这些是具体存档/版本证据，不推广成全部设备或固定成交价。整单面板曾显示8件估价111，确认后实际只有4件离柜、现金增加51，其余物品仍在且客户不再感兴趣；必须按每件去向和真实现金记账，不能把整单面板估价当成全部卖出。

现场验收应记录版本、准确实例ID、动作前后容器/数量/金额与原始回执。拆堆、合堆或消耗时不能凭名称宣称同实例保留；回店先核对袋内和口袋转移后的实际位置。没有原生绑定时保持未知。

本版未包括任意C#执行、改钱、造物、跳时间、读取模型密钥、Steam账号操作或自动上传日志。公开参考项目仅用于行为与验收方法调研，没有复制其代码。


## beta.2 当前原生改造体事件

已实测冻结DLL SHA256：`42A82580012F53D4C32409725B4AA222DFB3AF9432BEF81886C11A2E02C33C21`。16号副本第41天第二时间线visit15：外显“小偷”、内部aug_material、原生is_aug=true、tier=2、未扫描；take→ready→confirm后原生自动收起，安保原文“看来这确实是个改造体”。实际OnGoodKill生成sec_slip2587，报告原文记129信用点已入账、改造体被消灭。无需对白补丁。此证据只覆盖该次原生分支，其它分支仍待公测。

联合路线（尚未实测）：适合出售且当前顾客预算已知时，可先选货成交，再处理该次原生事件。为避免花光预算后客人离开，选原生整单报价严格小于当前剩余预算的组合并留正余额（预算100时80可，100不可）；报价或预算未知、无法留余额则跳过此交易，不强求卖货。按实际现金、离柜实例和回读预算记账；成交后重新读取同一session/visit且原生is_aug仍true、当帧绑定有效才可继续事件。客人离开即结束，禁止把旧绑定用于下一人。这是此联合路线的策略，不限制普通买家的正常成交。
