> 吸收单元: f08, f09, f10, p43, p44, p45, p50, p53, p54, ce33, ce36（参考素材: p48/p49 权限表；边界素材: ce35 needs_review）

# 工程师模式、安全代码与权限 (RCP-3500/3501)

## R — 原文

- 进入路径: "按下 [Engineer Mode] 以亮起按钮指示灯。出现隐藏的项目"；"要退出工程师模式,按下 [Engineer Mode] 以便熄灭按钮指示灯"；"如果已配置安全代码,当按下 [Engineer Mode] 时将显示安全代码输入画面。输入正确的安全代码,按下 [OK]"。(第 17 页)
- 隐藏入口: "按住PARA、MASTER和CUSTOM PAINT按钮的同时打开控制面板"，"使用数字键盘输入 0359,然后按下 [OK]"。(第 51 页)
- 设码: "使用数字键盘输入任意安全代码（1-8 位数）,然后按下 [OK]"，再次输入以确认。(第 51 页)
- 菜单可见性: File/Maintenance "此菜单仅在工程师模式下显示"(第 38/39 页)；"当控制面板处于工程师模式或 Page Permission 的 Full Paint 设为 ON 时"增加 File/Maintenance/Paint 菜单项。(第 16 页)
- Page 三开关: "Full Lock 禁止控制面板的所有操作"；"View Mode 禁止控制面板的所有操作（查看数据除外）"；"Full Paint 亮起后所有 [Paint] 菜单都变为可用"。(第 20 页)
- Item 七开关: APR / Ref File / Lens File / OHB File / Crop(16:9→4:3) / Knee Max / SW Menu 各 Enable。(第 20 页)

## I — 自述

工程师模式是这台面板的"管理员层"：时钟、连接、安全限制、自定义、备份、初始化等十类设定全部藏在这层后面，File/Maintenance/Paint 三整个菜单也只在其中显示。所以"找不到菜单/找不到设定项"的第一反应应该是查权限，而不是以为设备缺功能。

三层防误操作结构：①工程师模式门（Security 画面开启，可加安全代码保护）；②Page Permission（整机级：Full Lock 全锁 / View Mode 只读 / Full Paint 开放 Paint）；③Item Permission（功能级：APR、参考文件、镜头文件、OHB 文件、Crop、Knee Max、SW 菜单七项逐个开放）。

安全代码生命周期四件事：启用保护（隐藏三键组合 + 万能码 0359）、设置（1-8 位，输两遍）、更改（旧码换新码）、应急（忘了码就走 0359 入口禁用保护或删除代码）。设码后每次进工程师模式都要输码。

## A1 — 书中未提供案例（合成演练）

原书未提供完整案例。两条明确标记的合成演练（均可按原书规则复算）：

1. 接手旧面板、无人知道安全代码（ce33 演练口径）：关机 → 按住 PARA+MASTER+CUSTOM PAINT 开机 → 输 0359 → [OK] 进 Engineer Protection 画面 → [Code Delete] 亮灯 → [OK] 删除旧码 → [Exit] → 此后 Security 画面按 [Engineer Mode] 直接进入。
2. 给普通操作员配只读（f10 演练口径）：进工程师模式 → Security → [Page Permission] → [View Mode] 亮灯 → [Exit] → [Engineer Mode] 熄灯退出。效果：该面板只能看不能改。

## A2 — 未来触发

**情境**：①Category Select 里找不到 Paint/File/Maintenance 菜单，怀疑设备缺功能；②要设/改/删安全代码，或接手面板时前一个人的码没人知道；③要限制现场操作员误触（只读/全锁/开放部分功能）；④要配时钟、连接、备份等工程师模式专属设定，发现选项根本不显示；⑤Knee Max 等带门控的参数调不动。

**语言信号**：工程师模式 / engineer mode、安全代码 / security code、0359、面板锁死 / locked out、权限 / permission、菜单不见了 / menu missing、只读 / view mode、Full Paint。

**相邻区分**：network-setup 讲"连接设定怎么配"（也要先进工程师模式，但那边是配置内容，本卡是"怎么进门+权限怎么管"）；customization 讲"按钮/旋钮/菜单指到哪"（权限可见性归本卡）；paint-adjustment 讲 Paint 菜单里的参数语义（本卡只负责把门打开）。

## E — 可执行步骤

**输入契约**：先确认面板当前状态——是否已设安全代码（决定进入分支）；要做的设定是否属于工程师模式清单（时钟 p17 / 连接 p18 / 安全限制与自定义 p20 / 灵敏度 p24 / 备份 p25 / 初始化 p26 / PIX-WF p49 / Return Settings p50 / Menu Control p51 / 预览输出 p52；例外：Display/Sound 普通模式可配）。缺"目标设定是否工程师模式项"的判断时，先按下面步骤进门再找，不要猜。

**主流程**：
1. MENU → [Config] → [RCP]，进入 RCP Config 画面。
2. [Security] → [Engineer Mode] 亮灯 → 隐藏项出现。已设码：先输码 → [OK]。
3. 执行目标设定（本卡范围内：Page/Item Permission 配置；其余设定到对应能力卡执行）。
4. 完成后 [Exit] → 再按 [Engineer Mode] 熄灯退出（防止停留在高权限层）。

**安全代码分支**：
- 启用保护：关机 → 按住 PARA+MASTER+CUSTOM PAINT 开机 → 输 0359 → [OK] → [Code Enable] 亮灯 → [Exit]。默认禁用，必须由此入口开启。
- 设置：Security 画面 → [Code Change] → 输 1-8 位新码（显示为 *）→ [OK] → 复输确认 → [OK]。此后每次进工程师模式都要求输码。
- 更改：输码进入工程师模式 → [Code Change] → 输旧码（Old）→ 输新码（New）两遍。
- 应急（码丢了）：重复"启用保护"入口 → [Code Enable] 熄灯＝禁用保护；或 [Code Delete] 亮灯 → [OK]＝删除代码。

**输出契约**：进入成功的判据=隐藏项出现；退出成功的判据=指示灯熄灭；权限配置成功的判据=对应菜单/开关按预期出现或消失（如 View Mode 后面板只剩查看）。

## B — 边界

- **不要**在普通模式下反复找 File/Maintenance/Paint——那是权限隐藏（ce36），不是功能缺失；也不要给"菜单少"直接报修。
- **Full Lock 误启用无原文解除路径**（ce35，needs_review）：手册未说明 Full Lock 生效后如何回到 Security 画面，"重新进 Security 画面"未经证实。启用 Full Lock 前先想清楚退出手段，不要在直播中尝试。
- **0359 是万能入口也是安全弱点**（ce33）：任何知道三键组合+0359 的人都能解除代码。手册未讨论此风险；自定义码应入册管理，不要依赖 0359 保密。
- 输错安全代码的表现原书未述，不要向用户断言"会锁定多久"之类行为。
- 源内两处表述差异已消解并留痕：File/Maintenance 显示条件以"需工程师模式"为准（p16 与 p20/28/38/39 合读）；PIX1/WF1 与 PIX2/WF2 接口名（p49 vs p50/53）语义一致，以实机为准。
- 两型号通用（RCP-3500/3501），无型号差异项。
