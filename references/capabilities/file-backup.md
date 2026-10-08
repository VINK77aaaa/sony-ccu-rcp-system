> 吸收单元: f20, f25, p50, p51, p52, ce18

# USB 备份/恢复/初始化（RCP Config 与 Network Config 两类备份 / 撞号覆盖 / All Preset）

## R — 原文

（带引号者为原文直接引用；未带引号者为依据 verified 单元整理的原文要点摘录，页码为原文所在页。）

- 两类备份互斥（p25，摘录）：[RCP Config]="RCP 自定义设定,不包括网络设定"；[Network Config]=网络设定。
- 覆盖规则（p25）：选择已存在的文件编号保存，"则会覆盖其数据"。
- Store/Recall/Delete 共用流程（p25-26，摘录）：执行至选编号步骤后改按对应按钮，之后操作相同；编号可经 File ID 软键盘命名。
- All Preset 初始化（p26，摘录）：Security 画面→[All Preset]→[OK]，所有 RCP 配置菜单设定重置为默认；须在工程师模式中执行。
- 时钟与备份的关系（p17-18，摘录）：内部时钟用于记录参考文件和场景文件保存到 USB 驱动器时的日期和时间；对时技巧："在接收到时间信号的同时按下 [Set]"。

## I — Interpretation

RCP 的设定资产要落 U 盘，先分清"备什么"：

1. 备份分两类且互斥：[RCP Config] 装自定义设定（不含网络），[Network Config] 装网络设定。完整换机必须两类各做一次，只备一类=丢另一半。
2. 存/取/删共用一个骨架：进工程师模式→USB Backup→选类别→Store（或 Recall/Delete）→选编号→Enter→确认画面再 Enter；可选 File ID 命名。
3. 编号是唯一防线：选了已占用的编号就直接覆盖旧备份，没有回收站、没有二次警告——选号前必须查列表。
4. 备份文件的时间戳取自面板内部时钟，所以校时（对时间信号按 Set）是备份可信度的一部分。
5. All Preset 是全量回默认的"格式化"，入口在 Security，工程师模式执行——执行前先有备份。

## A1 — Application Example

原书未提供本能力的亲历/结果类案例。以下为一条明确标记的**合成演练**（按 p25-26 规则可复算，非作者经历）：

- 输入：面板 A 退役换新面板 B，要求配置完整迁移、可恢复。
- 执行：B 步前先校时钟（Config>Date/Time，时分秒对准时间信号按 [Set]）；插 USB→进工程师模式→Config>USB Backup→①选 [RCP Config]→Store→滚动列表选空闲编号→[Enter]→确认画面 [Enter]（可选 File ID 命名）；②再选 [Network Config] 重复一遍。恢复：面板 B 同路径改按 [Recall] 选对应编号→两次 Enter。
- 预期：U 盘上有两类各一文件，恢复后 B 的自定义分配与网络参数均在。
- 反例推演：只备份 [RCP Config]→网络设定丢失（由类别定义直接推出）；直接键入已占用编号→旧备份被覆盖且无回收（ce18）。
- 原书未交代实际结果（未说明）。

## A2 — Future Trigger

使用情境：
1. 换面板/退役前备份（"这台面板要换新，配置怎么导出去"/"backup panel settings"）。
2. 故障后恢复（"新面板能不能把旧配置导进去"/"recall from USB"）。
3. 配置混乱要重置（"恢复出厂设置"/"all preset"/"初始化面板"）。
4. 备份文件日期不对（"备份时间怎么是错的"→内部时钟未校准）。
5. 怕覆盖旧备份（"1 号文件会不会被覆盖"/"file number conflict"）。

语言信号（中英）：USB 备份 backup、RCP Config、Network Config、恢复 recall、删除 delete、初始化 All Preset、恢复出厂 factory reset、文件编号 file number、覆盖 overwrite、File ID、时钟设定 time setting、时间信号。

与相邻能力的区分（初稿，阶段 3 回填）：
- scene-files：场景/参考/镜头文件的 CAM↔USB 传输（File 菜单 Scene Transfer 等）归那边；本卡 USB Backup 只管 RCP 自身两类设定（[RCP Config] 不含场景文件）。
- engineer-mode-security：工程师模式是本卡一切操作的门槛，"怎么进/怎么设码"归那边。
- customization：备份内容包含自定义分配，但"改自定义"本身归那边。
- maintenance-correction：OHB Store 落盘的是摄像机侧校正资产，不是本卡的 USB 备份对象。

## E — Execution

输入契约：
- 必需 (a) 动作：Store/Recall/Delete/All Preset；(b) USB 驱动器已插入；(c) 工程师模式已进入（未进入先走 engineer-mode-security，判停）；(d) 目标文件编号——未指定时先滚动列表报占用情况给用户，不得默认选 1 号；(e) 执行 All Preset 前须确认已有可用备份。
- 缺 (b)(c) 先补做；缺 (d) 询问用户，不猜。

步骤：
1. 校时（推荐，保证时间戳可信）：Config>Date/Time→Time Zone 设与格林威治标准时间的时差→[Set]；Date 用左侧三旋钮设年月日→[Set]；Time 用左侧三旋钮设时分秒→接收时间信号的同时按 [Set]（p17-18）。
2. Store：Config>USB Backup→选 [RCP Config]→Store→查列表选空闲编号→[Enter]→确认画面再 [Enter]→可选 File ID 命名（p25）。
3. **判停分支**：目标编号已被占用→换空闲号；用户坚持覆盖→必须口头确认并核对旧文件 File ID 后再执行（ce18 规避）。
4. 对 [Network Config] 重复步骤 2——两类必须分开各备一次，缺一即残缺备份（p25）。
5. Recall/Delete：执行至选编号步骤后改按对应按钮，之后操作相同（p26）。
6. All Preset：确认备份在手→Security→[All Preset]→[OK]→全部配置菜单设定回默认（p26；工程师模式）。
7. 验证：恢复后抽查自定义按钮分配与网络连通性（面板与 CCU 通信正常）。

输出契约：每个备份报告"类别 + 编号 + File ID + 时间戳"四元组；恢复后报告验证点结果；覆盖操作留确认记录。

## B — Boundary

- 失败模式 ce18：选用已占用文件编号→"则会覆盖其数据"，无回收机制、手册未见二次警告；备份前查列表避让是有意覆盖前的唯一防线。
- 覆盖缺口（needs-review/f25）：备份文件的跨面板、跨固件格式兼容性原书未述——恢复失败时先核对同型号与固件口径，别急着反复重写。
- 口径区分（p52 notes 如实记录）：All Preset "执行前应已有 USB 备份"为操作建议（引申自备份能力），非原文明文前置；原文明文的只有范围与路径。
- 资产边界：场景/参考/镜头/OHB 文件不经本通道备份（g13/g16 口径）；本卡只管 RCP 自身设定。
- 时钟边界：秒级对时依赖外部时间信号；无信号时的对时精度原书未说明，备份排序前留意时间戳可信度。
- 反场景：想备份"画面风格套装"→那是场景文件（scene-files / File>Scene Transfer）；想改自定义分配→customization；进不了工程师模式→engineer-mode-security。
