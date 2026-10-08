> 吸收单元: f28, f29, f33, f34, p66, p80（支撑：c16、ce17、ce24、ce27、p48、p61、f19、f36、g60、g66、p38）

# 本机菜单操作与可编配按钮 (HDCU5000/5500/3500)

## R — 原文

- "当 <OUTPUT FORMAT1> t SDI-OUT4 t MONITOR 设为 C (不添加字符) 时,可以将 DISP/MENU 杆保持在 MENU 位置 3 秒钟以强制显示 CCU MENU。"(第 18 页)
- "将 CANCEL/ENTER 控制杆设定到 ENTER 位置和按 CONTROL 旋钮执行的功能相同。"；"按下此旋钮可执行与将 CANCEL/ENTER 控制杆设定到 ENTER 位置相同的功能。"(第 18 页、第 10 页)
- 字符串输入（第 19 页）："选择 INS 在光标位置插入空格字符。"；"选择 DEL 删除光标位置处的字符。"；"选择 RET 返回步骤 1,而不会更改字符串。"；"输入最多数量的字符 (至右边缘),将光标移动到字符列表右下方的 ESC。"；"3 转动 CONTROL 旋钮将光标移动到 END,然后按 CONTROL 旋钮。"
- M03："CAMERA MENU CTRL OFF、ON 显示摄像机菜单。如果 CAM MENU 设定为 ON,CCU 菜单操作无法执行,因为只有摄像机菜单操作可用。输出 SD 信号时,不显示摄像机菜单。"；"PAGE RESUME ON、OFF"；"ALARM JUMP ON、OFF"。(第 76 页)
- M08："ASSIGNABLE SWITCH NONE、BARS、CAM POWER、FORCE LEGACY、OPTICAL SIGNAL"；"SIGNAL BAR … READY COLOR WHITE、GREEN、BARS … BRIGHTNESS LOW、MIDDLE、HIGH"。(第 77 页)
- 前面板（第 10 页）："m 菜单锁定开关 锁定前面板菜单操作区域的操作。"；"l POWER 开关 打开和关闭整个摄像机系统的电源,包括本机、摄像机和连接至本机 REMOTE 接口的 RCP-3000/1000 系列遥控面板。"
- 菜单惯例（第 29 页）："设定列值 (例如 ON、OFF、0)：默认设定带有下划线"；"通过使用 ENTER 执行：直接使用设置菜单时,可按下 CONTROL 旋钮或将 CANCEL/ENTER 控制杆移到 ENTER 位置来执行操作。使用 Web 菜单时,可单击 OSD 菜单中的 ENTER 按钮来执行操作。"

## I — 自述

本卡是**操作通法卡**：教你用前面板 MENU 控制区块把 CCU 菜单走一遍，以及配可编配按钮、管菜单可用性。它不是"某个参数怎么设"，而是"任何参数怎么设"的公共动作层。

**三个物理控件 + 两条控制杆**（第 10 页）：

- `DISP/MENU` 控制杆：两个位置——`DISP` 显示状态画面、`MENU` 显示设定菜单（指示灯点亮）。有两个隐藏行为：摄像机编号不为 0 时，`DISP` 位置**保持 3 秒**→ 滚动显示 LAN COM 的 IP 与子网掩码；当 `SDI-OUT4 MONITOR=C` 时，在 `MENU` 位置**向下按住 3 秒**→ 返回 MONITOR 的 `M` 设置，并强制显示 CCU MENU。
- `CANCEL/ENTER` 控制杆：取消 / 输入。
- `CONTROL` 旋钮（旋转编码器）：状态画面模式换页；设定菜单模式移光标、改值；**按下等同 ENTER**。

**"指针↔闪烁问号↔注册"三段式**是核心交互范式（第 19 页）：指针 `(,)` 移到项目 → 按旋钮 → 变**闪烁问号 `(?)`** → 转旋钮改值 → 再按旋钮 → 变回指针，设定即注册。改页同理：指针移到页码 → 按 → 问号 → 转旋钮换页 → 按 → 变回指针。

**字符串输入**（第 19 页）走专用子流程，用到 `INS / DEL / RET / END / ESC` 五个功能键：输入到右边缘时光标自动移到 `ESC`，`END` 注册、`ESC` 取消。书中示例字符串项目为 `VIDEO/MONITOR t BAR CHARACTER`。

**两条可用性铁律**（最易被误判为故障）：

1. `CAMERA MENU CTRL=ON` 时，**只有摄像机菜单可用，CCU 菜单操作无法执行**；且**输出 SD 信号时不显示摄像机菜单**（第 76 页 M03）。
2. **菜单锁定开关 ON** 时，前面板菜单操作区域被锁定；且**无法使用 Web 菜单配置本机**（第 10 页 m、第 21 页）。菜单"按不动"的第一嫌疑就是它。

**POWER 开关作用域**（第 10 页 l）：它开关的是**整个摄像机系统**——本机、摄像机、以及连接至 REMOTE 接口的 RCP-3000/1000 系列面板；`?` 开机、`a` 关机。

## A1 — 书中配置示例

以下均为**书中操作示例**（原书自带演算，非实际工程记录）：

1. 字符串输入演算（c16，第 19 页）：以 `VIDEO/MONITOR t BAR CHARACTER` 页为对象——指针移到该项 → 按旋钮（出现矩形光标与字符列表）→ 光标移到输入位置 → 按（出现第二光标）→ 转旋钮选字符 → 按；重复；需要时用 `INS` 插空格、`DEL` 删字符、`RET` 退回步骤 1 不改；输入到右边缘后光标移到 `ESC`；最后移到 `END` → 按注册；放弃则移到 `ESC` → 按。
2. 强制显示 CCU MENU（第 18 页）：当 `SDI-OUT4 MONITOR=C`（不添加字符）时，把 `DISP/MENU` 杆保持在 `MENU` 位置 3 秒，即可强制显示 CCU MENU。
3. 返回 MONITOR 的 M 设置（第 10 页）：当 `SDI-OUT4 MONITOR=C` 时，在 `MENU` 位置向下按住 `DISP/MENU` 控制杆 3 秒，可返回 `M` 设置。

**手册未给出**"配一串可编配按钮"的过程性算例；上述为原书真实演算，可编配按钮取值选择属**合成演练（非原书内容）**。

## A2 — 未来触发

**情境**：

1. 无监视器现场操作："菜单怎么调出来 / 怎么翻页 / 怎么改值 / 怎么输名字"。
2. 菜单"按不动"排查："前面板菜单没反应 / 能连 Web 但改不了设置"。
3. 摄像机菜单与 CCU 菜单切换："想看摄像机菜单 / CCU 菜单不见了"。
4. 可编配按钮分配："这个空按钮设成彩条 / 摄像机电源 / 强制 LEGACY"。
5. 电源与菜单可用性："POWER 开关关的是哪些设备 / 菜单锁定开关管什么"。

**语言信号**：中文——"菜单 / 调菜单 / 翻页 / 光标 / 改值 / 字符串输入 / 按不动 / 锁了 / 摄像机菜单 / 可编配按钮 / 电源开关"；英文——"menu / navigate / cursor / string input / assignable switch / camera menu / menu lock / POWER switch"。

**相邻区分**（初稿，阶段 3 回填）：

- **ccu-specs-reference**：`MONITOR` 固定为 C 的完整固定值清单归彼卡；本卡只讲"当 MONITOR=C 时按住 3 秒"这一操作行为。
- **ccu-audio-intercom / ccu-trunk-prompter**：本卡管"怎么操作"，彼二卡管"设什么值"。
- **led-diagnostics / 状态类卡**：状态画面的进入/翻页与灯语判读归状态卡与灯语卡；本卡只覆盖"进入/退出/改值/字符串输入"的公共动作。
- **network-setup（RCP 侧）**：Web 菜单的访问流程（Chrome、IP、CCU 列表）归网络卡；本卡只收录"锁定开关 ON → Web 无法配置"这一条联动。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：①目标——改设置 / 看状态 / 输字符串 / 分配按钮；②监视器接在哪里（`CHARACTER` / `SDI OUT 3` / `SDI OUT 4`）；③前面板菜单是否可操作（若不可，先确认菜单锁定开关与 `CAMERA MENU CTRL`）；④可编配按钮用途。不明先问。

1. **显示菜单**（第 18 页）：`DISP/MENU` 杆 → `MENU` 位置（指示灯点亮）。**判停**：若 `SDI-OUT4 MONITOR=C` 而不显示菜单 → 在 `MENU` 位置**向下按住 3 秒**强制显示 CCU MENU。用 `SDI OUT 3`/`SDI OUT 4` 接监视器须先把 `SYSTEM CONFIG t <OUTPUT FORMAT1> t SDI-OUT3/4 t MONITOR` 设为 `M`。
2. **进 CCU MENU**（第 18 页）：在菜单显示模式，转动 `CONTROL` 旋钮把指针移到菜单页右上角 `TOP` → 按旋钮 → 显示 `CCU MENU`（SYSTEM CONFIG / VIDEO/MONITOR / AUDIO/INTERCOM / MAINTENANCE / FILE / NETWORK / DIAGNOSIS）。
3. **选项目 / 换页**（第 19 页）：指针移到所需菜单项目 → 按 → 显示该菜单最近查看的页面；换页 = 指针移到页码 → 按（指针变闪烁问号）→ 转旋钮换页 → 按（问号变回指针）。
4. **改值**（第 19 页）：指针移到项目 → 按（变闪烁问号）→ 转旋钮改值 → 按（问号变回指针，设定注册）；重复可改同页其它项。**判停**：改错了 → `CANCEL/ENTER` 杆 → `CANCEL` 位置 + 按 `CONTROL` → 恢复当前设定；想暂停 → `DISP/MENU` → `MENU` 位置退出，再回 `MENU` 位置可继续。
5. **字符串输入**（第 19 页，c16）：指针移到需字符串项 → 按（出现矩形光标与字符列表）→ 光标移到输入位置 → 按（出现第二光标）→ 转旋钮选字符 → 按；重复；`INS` 插空格、`DEL` 删字符、`RET` 退回步骤 1 不改；输入满到右边缘光标移到 `ESC`；移到 `END` → 按 → 注册。**判停**：想放弃 → 光标移到 `ESC` → 按。
6. **退出菜单**（第 19 页）：`DISP/MENU` 杆 → `MENU` 位置。
7. **可编配按钮**（第 77 页 M08）：`ASSIGNABLE SWITCH` 选 `NONE` / `BARS` / `CAM POWER` / `FORCE LEGACY` / `OPTICAL SIGNAL`；`SIGNAL BAR` 的 `DISPLAY` 选 `OFF`/`ON`、`READY COLOR` 选 `WHITE`/`GREEN`/`BARS`、`BRIGHTNESS` 选 `LOW`/`MIDDLE`/`HIGH`。
8. **菜单可用性检查**（第 76 页 M03、第 10 页 m）：若菜单按不动 → 先看 `CAMERA MENU CTRL` 是否为 `ON`（ON 时只有摄像机菜单可用、CCU 菜单不可操作，输出 SD 信号时不显示摄像机菜单），再查**菜单锁定开关**是否在 ON（ON 时前面板与 Web 均受限）。**POWER 开关**（第 10 页 l）关整个摄像机系统（本机 + 摄像机 + REMOTE 上的 RCP-3000/1000），`?` 开、`a` 关。

**判停分支**：菜单无法操作且 `CAMERA MENU CTRL=ON` → 关掉该项恢复 CCU 菜单；输出 SD 信号时看不到摄像机菜单 → 属正常；Web 能连但改不了 → 菜单锁定开关置 OFF。

**输出契约**：报告 = 操作序列（进入 → 定位 → 改值/输入 → 注册/退出）+ 每步物理动作与页码 + 菜单锁定/CAMERA MENU CTRL/POWER 作用域提示。

## B — 边界

- **不要用本卡**：具体参数取值与联动（ccu-audio-intercom、ccu-trunk-prompter 等）；状态画面判读与灯语（状态卡、led-diagnostics）；Web 菜单访问流程（网络卡）；接口规格速查（ccu-specs-reference）。
- **手册警告的失败模式**：`CAMERA MENU CTRL=ON` 时误以为 CCU 菜单坏了 → 实际只有摄像机菜单可用（ce24，第 76 页）；菜单锁定开关 ON 时用 Web 配置本机 → 无法配置（ce17/p38，第 21 页）；在 `SDI-OUT1/2` 上加菜单字符 → `MONITOR` 固定为 C（ce27，第 36 页）；`SDI-OUT4 MONITOR=C` 时找不到菜单 → 未用"按住 3 秒"（第 18 页）。
- **型号差异**：本卡操作通法与 M03/M08 对三型号一致；`POWER` 开关作用域含"连接至 REMOTE 接口的 RCP-3000/1000 系列"（第 10 页 l）。`CHARACTER/SYNC/AES/EBU` 共用接口在 HDCU5500/3500，HDCU5000 为独立 `CHARACTER/SYNC`（第 31 页）——影响"用哪个口接监视器看菜单"。
- **作者盲点（阶段 0 批判）**：手册以图为主讲面板布局，纯文本只保留可文字化动作；"按住 3 秒"的两个隐藏行为分写在前面板页与菜单操作页，需合并理解；`CAMERA MENU CTRL=ON` 时"如何切回 CCU 菜单"手册未给明确步骤（推断为设回 OFF，非原文）；Web 端完整操作链在 Web 菜单章节，本卡不展开。
