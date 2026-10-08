> 吸收单元: f11（反例 ce23；术语 g18, g21, g22, g23, g24, g25, g26, g27, g28；参考项 p09）

# HDR / LIVE HDR 配置 (HDCU5000/5500/3500)

## R — 原文

- HDR MODE：`OFF`、`LIVE HDR`——"OFF:正常拍摄操作。LIVE HDR:用于 LIVE HDR 拍摄。选择 LIVE HDR 时,摄像机绘制功能可用于 HDR 输出和 SDR 输出。但是, HDR 输出不支持某些绘制功能。" (第 35 页，S06)
- SDR GAIN：`–15 至 0.0`、`0 dB`——"仅在 LIVE HDR 模式下启用。增益设置适用于 SDR 输出" (第 35 页，S06)
- HDR CONTRAST：`100 至 560%`——"仅在 LIVE HDR 模式下启用。通过设置 SDR GAIN 维持 HDR 输出对比度 (仅显示)" (第 35 页，S06)
- HDR BLACK OFFSET：`–99 至 99`、`0`——"仅在 LIVE HDR 模式下启用。HDR 输出黑色偏移" (第 35 页，S06)
- HDR OETF：`S-Log3`、`HLG`——"设置视频输出 OETF。" (第 35 页，S06)
- HDR LOOK：`Natural`、`Mild`、`Live`——"设置视频输出 LOOK。" (第 35 页，S06)
- HDR COLOR SPACE：`BT709`、`BT2020`——"选择视频输出的颜色空间。BT709:将颜色输出格式设为 BT709。BT2020:将颜色输出格式设为 BT2020。" (第 35 页，S06)
- 4K COLOR SPACE：`BT709`、`BT2020`——"选择 4K 视频输出的颜色空间。当 HDR MODE 设为 LIVE HDR 时,设置与 HDR COLOR SPACE相同。" (第 35 页，S06)
- "对于带下划线的格式,可以根据所连接摄像机的 Live HDR 模式设置在 HDR 和 SDR 之间切换模式。" (第 54 页，输出格式表页眉)
- SDI-OUT / SDI-I/O / IP-OUT 的 OETF：`SDR`、`HDR OETF`——"设置视频输出的伽马曲线。" (第 36/45 页，S07/S11)
- UHD-SDI 各口的 OETF：`SDR`、`4K OETF`——"设置视频输出的伽马曲线。" (第 40 页，S09)
- CAMERA FORMAT 候选中的 HDR 标注：`UHD/59.94P (4K/HDR)`、`1080/59.94P (4K/HDR)`；ULTRA 档的 `3840×2160/59.94P(2×) (HDR/SDR)`、`1080/59.94P (HDR/SDR)`、`1080/59.94I(RGB444) (SDR)`。 (第 33/51/58 页)
- 状态画面实测示例：`*Multi Format1* 02/11 SDI-OUT 1:1080/59.94P/3G-A OETF:HLG_BT.2100 Color:BT.2020`。 (第 16 页)
- 返回表 720 前置："*3 当 CCU VIDEO CONVERT 设为 ENABLE 并且所连摄像机的 HDR 模式设为 OFF 时,可以选择 720 输入。" (第 52/53 页)

## I — 自述

**本卡管什么。** CCU 侧 HDR 输出的全部开关：HDR MODE、SDR GAIN、HDR CONTRAST、HDR BLACK OFFSET、HDR OETF、HDR LOOK、HDR COLOR SPACE、4K COLOR SPACE，以及各输出口 OETF/COLOR 的取值。核心口径：**LIVE HDR 不是"高动态范围"泛称，而是 Sony 的同步双输出机制**——同一台摄像机在 LIVE HDR 下同时输出 HDR 与 SDR 两路，本机对两路各自做设置。

**前置条件链（顺序不可颠倒）。**
1. **所连摄像机必须支持 Live HDR**。这是硬前提：手册明确"对于带下划线的格式,可以根据所连接摄像机的 Live HDR 模式设置在 HDR 和 SDR 之间切换模式"（第 54 页）——HDR/SDR 的切换是**由摄像机侧驱动**的，CCU 只是跟随。摄像机不支持，本卡全部设置无意义。
2. **4K HDR 还需选件**：要 4K 输出，须装 HZCU-UHD35（第 14 页，且该软件在 HDCU5000/5500 上受 HKCU-SM50 安装状态影响，第 3 页）；HDCU3500 还须先装 HKCU-FB50 才有 4K 传输能力。
3. **把 HDR MODE 设为 LIVE HDR**。这一步是使能闸门——SDR GAIN、HDR CONTRAST、HDR BLACK OFFSET 三项**仅在 LIVE HDR 模式下启用**（第 35 页）。HDR MODE=OFF 时，这三项不可用。
4. **再设 HDR 主参数**：HDR OETF（`S-Log3` 或 `HLG`）、HDR LOOK（`Natural`/`Mild`/`Live`）、HDR COLOR SPACE（`BT709`/`BT2020`）。
5. **最后设 4K COLOR SPACE**：它虽是与 HDR COLOR SPACE 并列的一项，但在 LIVE HDR 下被**强制跟随 HDR COLOR SPACE**（第 35 页"设置与 HDR COLOR SPACE相同"）——不要在 LIVE HDR 下试图把两者设成不同值。

**使能关系一：SDR GAIN 是"总闸"，HDR CONTRAST 是"读数"。** SDR GAIN（`–15 至 0.0`、`0 dB`）只作用于 LIVE HDR 下的 **SDR 那一路输出**；HDR CONTRAST（`100 至 560%`）标注"仅显示"，其值"通过设置 SDR GAIN 维持"——也就是说，HDR CONTRAST 不是独立可调项，你调的是 SDR GAIN，对比度读数随之变化。

**使能关系二：HDR BLACK OFFSET 只作用 HDR 支路。** `–99 至 99`、`0`，仅 LIVE HDR 下启用，是 **HDR 输出**的黑色偏移（与作用于 SDR 支路的 SDR GAIN 分属两路）。

**使能关系三：OETF 的取值集合随接口类型变化。** 这是最容易设错的地方：
- HDR OETF（S06）是"源头"设置，取 `S-Log3` 或 `HLG`；
- 各 **SDI-OUT / SDI-I/O / IP-OUT** 口的 OETF 取 `SDR` 或 `HDR OETF`；
- 各 **UHD-SDI** 口的 OETF 取 `SDR` 或 `4K OETF`。
即：UHD-SDI 上不出现 "HDR OETF" 这个选项，而是 "4K OETF"。不要把三者混为一谈。

**边界一：HDR 输出不支持某些绘制功能。** 第 35 页原文明确"选择 LIVE HDR 时,摄像机绘制功能可用于 HDR 输出和 SDR 输出。但是, HDR 输出不支持某些绘制功能"（ce23）。即"绘制功能两路都可用"是**有保留的**——HDR 那一路有功能缺口。手册**未列明**具体缺哪些绘制功能，本卡不得编造。

**边界二：HDR/SDR 切换由摄像机侧决定。** 带下划线的格式能在 HDR 与 SDR 间切换，前提是"所连接摄像机的 Live HDR 模式设置"（第 54 页）。这是 CCU 侧的跟随行为，不是 CCU 独立开关。

**边界三：720 返回要求摄像机 HDR 模式 OFF。** 返回格式表的 720 项脚注 `*3` 要求"CCU VIDEO CONVERT 设为 ENABLE 并且所连摄像机的 HDR 模式设为 OFF"（第 52/53 页）。也就是说，**想用 720 返回就得放弃 HDR**——这是 HDR 与 720 之间的硬互斥（输出侧 720 只需 CCU VIDEO CONVERT=ENABLE，见 ccu-system-format）。

**边界四：RGB444 一律 SDR。** 格式串中标注 `(RGB444)` 的项在返回表里一律标 `(SDR)`（第 51 页 `1080/59.94I(RGB444) (SDR)` 等），即 RGB444 与 HDR 不共存——这与 BIT DEPTH 只在 RGB444 下可选形成呼应。

**本卡与摄像机侧的分工。** HDR 制作是 CCU 与摄像机两侧共同完成的：**摄像机侧**决定是否进入 Live HDR、绘制功能如何叠加、以及"带下划线格式在 HDR/SDR 间如何切换"（第 54 页明确该切换依据"所连接摄像机的 Live HDR 模式设置"）；**CCU 侧**负责把接收到的信号按 SDR 支路 / HDR 支路分别做增益、黑电平、OETF、LOOK、色彩空间的处理与输出。因此本卡的所有设置都建立在"摄像机已按 Live HDR 工作"这一前提上——若摄像机侧未开 Live HDR，CCU 侧的 HDR 参数即使设了也不会产生预期的双路输出。现场遇到"HDR 参数设了但画面不对"，应先确认摄像机侧状态，再回查 CCU 侧参数，而不是只在 CCU 菜单里反复试。

## A1 — 书中配置示例

以下均为**书中自带表格/画面**（原书 S06 页与状态画面，非实际工程记录）：

1. **HDR 参数全表（S06）**（第 35 页）：原书逐项列出 HDR MODE（`OFF`/`LIVE HDR`）、SDR GAIN（`–15 至 0.0`、`0 dB`）、HDR CONTRAST（`100 至 560%`）、HDR BLACK OFFSET（`–99 至 99`、`0`）、HDR OETF（`S-Log3`/`HLG`）、HDR LOOK（`Natural`/`Mild`/`Live`）、HDR COLOR SPACE（`BT709`/`BT2020`）、4K COLOR SPACE（`BT709`/`BT2020`，LIVE HDR 时与 HDR COLOR SPACE 相同），并注明前四项的使能条件。
2. **状态画面 HDR 实测示例**（第 16 页，`*Multi Format1* 02/11`）：原书画面示例显示 SDI-OUT 1–4 均为 `1080/59.94P/3G-A`、`OETF:HLG_BT.2100`、`Color:BT.2020`——这是手册给出的真实画面文字，可据以核对"实际输出口的 OETF/Color 值长什么样"。
3. **UHD-SDI 状态画面示例**（第 17 页，`*Multi Format3* 04/11`）：UHD-SDI A/B/C/D 显示 `3840x2160/59.94P/12G`、`OETF:HLG_BT2100`、`COLOR:BT2020`（仅装 HKCU-SDI50 时该页显示）。
4. **CAMERA FORMAT 中的 HDR 标注**（第 33 页，S05）：HIGH 档列出 `UHD/59.94P (4K/HDR)`、`1080/59.94P (4K/HDR)`；ULTRA 档格式在返回/输出表里标 `(HDR/SDR)` 或 `(SDR)`。

**书中未给完整示例的部分**：手册未给出"从 HDR MODE 开启到各口 OETF/COLOR 全部设好"的端到端文字示例（S06 是参数表，不是操作演算）。以下为**合成演练（非原书内容）**，仅演示本卡配置链的用法：

> 合成演练：现场需同一摄像机同时输出 HDR 与 SDR，摄像机支持 Live HDR，系统为 ULTRA×1.001(525)，已装 HZCU-UHD35。① 确认摄像机支持 Live HDR；② HDR MODE=`LIVE HDR`；③ SDR GAIN 取 `–15 dB`（SDR 支路）；④ HDR BLACK OFFSET 取 `0`；⑤ HDR OETF=`HLG`；⑥ HDR LOOK=`Live`；⑦ HDR COLOR SPACE=`BT2020`；⑧ 4K COLOR SPACE 自动跟随为 `BT2020`（不可独立改）；⑨ 各 SDI-OUT 口 OETF 取 `HDR OETF`、UHD-SDI 口取 `4K OETF`，COLOR 取 `BT2020`；⑩ 若需 720 返回，须把摄像机 HDR 模式设为 OFF（与 HDR 互斥）。

## A2 — 未来触发

**情境**：

1. HDR 制作立项："怎么让这台摄像机同时出 HDR 和 SDR / 参数怎么设"。
2. 4K HDR 输出前：确认是否装了 HZCU-UHD35（及 HDCU3500 的 HKCU-FB50）。
3. HDR 画面色彩/观感不对：回查 HDR OETF（S-Log3/HLG）、HDR LOOK、HDR COLOR SPACE。
4. 发现某输出口 OETF 选项里没有 "HDR OETF" → 那是 UHD-SDI 口，只有 "4K OETF"。
5. 想用 720 返回却选不了 → 回查是否因摄像机 HDR 模式未 OFF。
6. 发现 HDR 输出缺某些叠加/绘制信息 → 属"HDR 输出不支持某些绘制功能"的既定边界。

**语言信号**：中文——"HDR / LIVE HDR / 同时出 HDR 和 SDR / OETF / S-Log3 / HLG / 色彩空间 / BT2020 / 4K OETF / 黑色偏移 / SDR 增益"；英文——"HDR / LIVE HDR / OETF / S-Log3 / HLG / HDR COLOR SPACE / 4K COLOR SPACE / SDR GAIN / HDR BLACK OFFSET / HDR LOOK"。

**相邻区分**：

- **ccu-system-format**：彼卡管 SYSTEM/CAMERA FORMAT/BIT DEPTH/延迟；本卡管 HDR 参数。CAMERA FORMAT 里带 `(4K/HDR)`、`(HDR/SDR)` 标注的项由彼卡选择，但 HDR MODE/OETF/COLOR 的设定归本卡。
- **ccu-format-lookup**：某输出口"能出什么格式串、MONITOR/OETF/COLOR 填什么值"归彼卡；本卡决定这些 OETF/COLOR 值**取 HDR 还是 SDR / 4K 还是 SDR** 的策略。
- **ccu-transport-setup**：4K/HDR 能力的选件门槛（FB50/SM50）与传输通路归彼卡。
- **规格速查（specs-reference）**：OETF 名称、色彩空间的纯定义查询归彼卡；用它们做 HDR 配置归本卡。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：① CCU 型号；② 摄像机型号及**是否支持 Live HDR**；③ 目标（HDR 与 SDR 同时输出？仅 HDR？仅 SDR？）；④ 是否 4K；⑤ 已装选件（HKCU-FB50 / SM50，HZCU-UHD35）；⑥ 目标色彩空间与观感倾向。任一缺失先询问。

1. **摄像机能力核对**（不满足即停）：确认所连摄像机支持 Live HDR；否则本卡不适用。
2. **4K 选件核对**（若需 4K HDR）：确认已装 HZCU-UHD35；HDCU3500 另需 HKCU-FB50。
3. **开启 HDR MODE**：`SYSTEM CONFIG t <HDR> t HDR MODE` 设为 `LIVE HDR`。
4. **设 SDR 支路**：SDR GAIN 取 `–15 至 0.0` 区间值（如 `–15 dB`）；HDR CONTRAST 观察其随 SDR GAIN 变化的读数（仅显示，不单独调）。
5. **设 HDR 支路**：HDR BLACK OFFSET 取 `–99 至 99`（如 `0`）。
6. **设 OETF 源头**：HDR OETF 取 `S-Log3` 或 `HLG`。
7. **设观感**：HDR LOOK 取 `Natural`/`Mild`/`Live`。
8. **设色彩空间**：HDR COLOR SPACE 取 `BT709` 或 `BT2020`；LIVE HDR 下 4K COLOR SPACE 自动跟随（不要试图设成不同值）。
9. **设各输出口 OETF/COLOR**：SDI-OUT/SDI-I/O/IP-OUT 的 OETF 取 `SDR` 或 `HDR OETF`；UHD-SDI 各口的 OETF 取 `SDR` 或 `4K OETF`；COLOR 取 `BT709`/`BT2020`。**注意 UHD-SDI 上没有 "HDR OETF" 选项。**
10. **核对格式切换**：确认带下划线的输出格式已按所连摄像机的 Live HDR 模式在 HDR/SDR 间正确切换。
11. **收尾核对**：若要 720 返回，须把所连摄像机 HDR 模式设为 OFF（`*3` 前置）；RGB444 格式一律为 SDR，与 HDR 不共存；核对系统配置设备的软件与 ROM 版本兼容。

**判停分支**：SDR GAIN / HDR BLACK OFFSET 改不动 → 确认 HDR MODE 是否已设 LIVE HDR；某口找不到 "HDR OETF" → 该口是 UHD-SDI，应选 "4K OETF"；HDR 输出出现绘制功能缺失 → 属既定边界（ce23），非故障；720 返回选不了 → 按第 11 步把摄像机 HDR 设为 OFF；色彩不一致 → 回查 HDR COLOR SPACE 与 4K COLOR SPACE 是否被强制一致。

**输出契约**：报告 = HDR MODE 取值 + SDR GAIN / HDR BLACK OFFSET 取值 + HDR OETF / HDR LOOK / HDR COLOR SPACE / 4K COLOR SPACE 取值 + 各输出口 OETF/COLOR 设定 + 格式切换核对结论 + 720/选件相关前置核对 + 未决项。

## B — 边界

- **不要用本卡**：SYSTEM/CAMERA FORMAT/BIT DEPTH（ccu-system-format）、输出/返回格式串查表（ccu-format-lookup）、传输通路与选件门槛（ccu-transport-setup）、规格数值速查（specs-reference）。
- **手册警告的失败模式**：
  - LIVE HDR 下 **HDR 输出不支持某些绘制功能**（ce23，第 35 页）——不要承诺 HDR 输出支持全部绘制/叠加功能；手册未列明具体缺哪些，本卡不臆造。
  - 720 返回要求"CCU VIDEO CONVERT=ENABLE **并且**所连摄像机 HDR 模式 OFF"（第 52/53 页）——HDR 与 720 返回互斥，配置时勿同时要求两者。
  - RGB444 格式一律标 `(SDR)`（第 51 页）——RGB444 与 HDR 不共存。
  - CCU VIDEO CONVERT 设 ENABLE 却不把 FRAME SYNCHRONIZER 设 ON，会引发同步异常（第 34 页）——HDR 若涉及转换项须一并核对。
- **型号差异**：
  - **HDCU5000 / HDCU5500**：原生具备 4K；4K HDR 输出需 HZCU-UHD35（该软件在 5000/5500 上受 HKCU-SM50 安装状态影响，第 3 页）。
  - **HDCU3500**：仅 HD；4K 传输需 HKCU-FB50（等同 HDCU5500），4K 输出需再装 HZCU-UHD35；`<OUTPUT FORMAT4>`（UHD-SDI E/F/G/H）仅 HDCU5000 装 HKCU-SDI50 时显示。
  - **选件依赖**：HDR/4K 相关的 UHD-SDI 各口（S09/S10）与 IP-OUT4 的可用性随 SDI50/SFP50/UHD35 变化——菜单项显隐先看选件。
- **作者盲点（阶段 0 批判）**：
  - "带下划线的格式可根据所连接摄像机的 Live HDR 模式设置在 HDR 和 SDR 之间切换"——**依赖摄像机侧配合**，手册未给出完整前置条件（BOOK_OVERVIEW 已列为"未被证明/需标注的假设"）。
  - "HDR 输出不支持某些绘制功能"——手册**未列明**具体是哪些绘制功能，属故意留白，本卡不编造清单。
  - HDR 与摄像机侧 Live HDR 的完整交互（何时切换、切换后各口表现）手册只给结果不给过程，现场须以摄像机说明书为准。
  - 手册多处写"有关设定的详细说明,请联系 Sony 维修代表或销售代表"，属**故意留白**。
  - 三型号共用同一套 <HDR> 菜单，但 4K 能力与选件依赖差异大，"能否出 4K HDR"须先回 ccu-transport-setup 核对选件，再回本卡设参数。
