> 吸收单元: f27（支撑：c05、c06、ce21、ce26、ce38、ce39、g05、g06、g07、g57、g58、g62、g63、g65）

# 干线 / 提示机配置（TRUNK/PROMPTER） (HDCU5000/5500/3500)

## R — 原文

- M01 TRUNK/PROMPTER："TRUNK LINE CHANNEL MODE 2CH(MAX 75Kbps)、1CH(MAX 150Kbps)"；"INTERFACE 232C、422A 设定通信线路模式"；"PROMPTER CH 2CH、1CH 设定提示机线路的编号。"(第 75 页)
- M02 TRUNK/PROMPTER2："NETWORK TRUNK OFF、NETWORK、NETWORK+VIDEO"；"当 <CAMERA I/F> t FIBER TRANSMIT RATE 设为 ULTRA 时,将其设为 NETWORK+VIDEO (固定)。"；"DATA RATE 100Mbps、1Gbps"；"HD PROMPTER … 当在 HDCU5000/5500 上使用 SDI-RET 时,固定为 DISABLE。"(第 75 页)
- M02 续："HD/UHD TRUNK ENABLE、DISABLE（仅显示）"；"DATA RATE 1.5G、12G"；"SOURCE SDI-I/O4、IP-RET3"；"UHD PROMPTER … DATA RATE 1.5G、3G、6G、12G"；"SOURCE UHD-SDI D"。(第 75 页)
- S02："UHD-SDI B … I/O OUT 输出 (固定) … UHD TRUNK 仅适用于 HDCU5000/5500"；"UHD-SDI D … IN … SDI-RET、UHD PROMPTER … UHD PROMPTER 仅适用于 HDCU5000/5500"。(第 30 页)
- S03："PROMPTER2/VBS-RET … 设为 ENABLE (固定)。"(第 31 页)

## I — 自述

本卡管两套东西，分在两个页面上：

- **M01 `<TRUNK/PROMPTER>`**：串行干线（TRUNK）与模拟提示机线路的基础设定——`TRUNK LINE CHANNEL MODE`（通道数与速率上限）、`INTERFACE`（232C/422A）、`PROMPTER CH`（提示机线路编号）。
- **M02 `<TRUNK/PROMPTER2>`**：网络干线（NETWORK TRUNK）与**视频**干线/提示机（HD/UHD TRUNK、HD/UHD PROMPTER）。

先分清三个易混概念（术语表已互链）：`TRUNK` 接口是 12 芯 **RS-232C/RS-422A 串行**干线（g07）；`NETWORK TRUNK` 接口是 RJ-45 8 芯**网络**干线（g05），其菜单项即 M02 的 `NETWORK TRUNK`（g06）；`HD/UHD TRUNK` 是**视频**干线（g62）。同样，`PROMPTER 1/2` 是 1.0 Vp-p、75 欧姆的**模拟**提示机接口（g57），`HD/UHD PROMPTER` 是走 SDI 的**数字**提示机（g63）——不可混配。

本卡的核心是**一串"固定值 / 显示项"约束**，也是最易踩坑处：

1. **速率锁定**：`FIBER TRANSMIT RATE=ULTRA` 时，`NETWORK TRUNK` 被强制为 `NETWORK+VIDEO`（固定），不可改；`DATA RATE`（100Mbps/1Gbps）也**仅 ULTRA 下可设**。
2. **SDI-RET 抢占**：在 HDCU5000/5500 上使用 `SDI-RET` 时，`HD PROMPTER` 固定为 `DISABLE`。
3. **型号与方向**：`UHD TRUNK` / `UHD PROMPTER` 仅 HDCU5000/5500 可用（HDCU3500 无）；`UHD-SDI B` 的 I/O 固定为 OUT；`HD PROMPTER` 只在 `SDI-I/O 4` 选 IN 时可选，`UHD PROMPTER` 只在 `UHD-SDI D` 选 IN 时可选。
4. **接口固定**：`PROMPTER2/VBS-RET` 固定为 `ENABLE`，不可关。

`HD/UHD TRUNK`、`CAMERA` 等为"仅显示"的回读项，反映当前是否启用，不是可设开关；`FRAME SYNC` 有 `OFF、ON、(ON)` 三态，括号 `(ON)` 表示默认值。

## A1 — 书中配置示例

以下均为**书中配置示例**（原书连接图脚注给出的必配项，非实际工程记录）：

1. 同轴电缆连接（c05，第 7 页）：同轴连接时必配 `CABLE TYPE=COAX`、`SDI-I/O 3 SIGNAL=HD TRUNK`、`SDI-I/O 4 SIGNAL=HD PROMPTER`——即视频干线走 SDI-I/O 3、提示机走 SDI-I/O 4。
2. 同轴（HDCE）连接（c06，第 8 页）：`CABLE TYPE=COAX(HDCE)`、`SDI-I/O 3=HD TRUNK`、`SDI-I/O 4=HD PROMPTER`，与普通 COAX 仅 `CABLE TYPE` 取值不同。
3. 固定值对照（ce38，第 31 页 S03、第 30 页 S02）：`PROMPTER2/VBS-RET` 设为 `ENABLE`（固定）；`UHD-SDI B` 的 `I/O` 固定 `OUT`（输出）。
4. 速率约束（ce26，第 75 页 M02）：`FIBER TRANSMIT RATE=ULTRA` 时 `NETWORK TRUNK` 显示为 `NETWORK+VIDEO (固定)`。

**手册未给出**"从零配一条 HD PROMPTER + NETWORK TRUNK 通道"的完整过程性算例；上述为原书真实配置项/固定值，其余组合（如"2CH(MAX 75Kbps) + 422A + IP-RET3 源"）属**合成演练（非原书内容）**。

## A2 — 未来触发

**情境**：

1. 提示机接线与设定："提词器信号从哪个口进 / PROMPTER 通道选 1CH 还是 2CH"。
2. 干线通道规划："TRUNK 走 1 通道还是 2 通道 / 速率上限多少 / 用 232C 还是 422A"。
3. 网络干线配置："NETWORK TRUNK 选 OFF / NETWORK / NETWORK+VIDEO / 为什么改不动"。
4. 视频干线/提示机："HD TRUNK 数据速率 / UHD PROMPTER 源怎么选 / 提示机没信号"。
5. 排查"菜单项固定/变灰"：`HD PROMPTER` 显示 DISABLE、`DATA RATE` 不可改。

**语言信号**：中文——"干线 / 提示机 / 提词器 / 通道模式 / 232C / 422A / 数据速率 / 网络干线 / 固定 / 改不了"；英文——"trunk / prompter / teleprompter / channel mode / data rate / network trunk / HD PROMPTER / fixed"。

**相邻区分**（初稿，阶段 3 回填）：

- **ccu-audio-intercom**：本卡管干线/提示机（M01/M02）；彼卡管音频/对讲（A01–A07）。`HD TRUNK AUDIO OUT` 的音频格式属彼卡 A06，本卡只管干线本身的通道与速率。
- **ccu-menu-operation**：本卡给"设什么值"；"怎么进 M01/M02、怎么改值"归彼卡。
- **ccu-specs-reference**：`TRUNK 12 芯`、`NETWORK TRUNK 8 芯`、`PROMPTER 1/2` 的电气规格（1.0 Vp-p、75 欧姆、5MHz）与固定项清单归彼卡；本卡只做配置。
- **led-diagnostics**：提示机/干线无信号的灯语排查归彼卡。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：①提示机类型——模拟（`PROMPTER 1/2`）还是数字（`HD/UHD PROMPTER`）；②提示机线路数——1CH 还是 2CH；③串行干线需求——通道数（2CH/1CH）与制式（232C/422A）；④是否需要网络干线；⑤当前 `FIBER TRANSMIT RATE` 与所用接口（`SDI-I/O 4` / `UHD-SDI D` / `IP-RET3`）是否满足；⑥机型。不明先问。

1. **M01 串行干线**（第 75 页）：`TRUNK LINE CHANNEL MODE` 选 `2CH(MAX 75Kbps)` 或 `1CH(MAX 150Kbps)`；`INTERFACE` 选 `232C` 或 `422A`；`PROMPTER CH` 选 `2CH` 或 `1CH`（线路数量随所连摄像机提示机线路编号变化）。**判停**：通道数与速率上限是绑定的——选 2CH 即上限 75Kbps、选 1CH 即上限 150Kbps，不可自定义。
2. **M02 网络干线**（第 75 页）：`NETWORK TRUNK` 选 `OFF` / `NETWORK` / `NETWORK+VIDEO`。**判停**：若 `FIBER TRANSMIT RATE=ULTRA` → 该项固定为 `NETWORK+VIDEO`，改不动属正常；`DATA RATE`（100Mbps/1Gbps）仅 ULTRA 下可设，否则为显示项。
3. **视频干线/提示机回读**（第 75 页）：`CAMERA`、`HD/UHD TRUNK`、`HD PROMPTER`、`UHD PROMPTER` 的 `ENABLE/DISABLE` 均为**仅显示**；`HD/UHD TRUNK DATA RATE` 显示 1.5G/12G。**判停**：在 HDCU5000/5500 上使用 `SDI-RET` 时 `HD PROMPTER` 固定 `DISABLE`——需 HD PROMPTER 就不能用 SDI-RET 抢占该通路。
4. **提示机源与帧同步**（第 75 页）：`HD PROMPTER` 的 `SOURCE` 选 `SDI-I/O4` 或 `IP-RET3`（`IP-RET3` 须装 HKCU-SFP50）；`UHD PROMPTER` 的 `SOURCE` 选 `UHD-SDI D`，`DATA RATE` 选 `1.5G、3G、6G、12G`；`FRAME SYNC` 选 `OFF` / `ON` / `(ON)`（默认 ON）。
5. **接口方向前置**（第 30 页 S02）：确认信号源口的 I/O 方向——`SDI-I/O 4` 须选 `IN` 才能出现 `HD PROMPTER`；`UHD-SDI D` 须选 `IN` 才能出现 `UHD PROMPTER`。**判停**：`UHD-SDI B` 的 I/O 固定 `OUT`，无法作为输入；`UHD TRUNK`/`UHD PROMPTER` 在 HDCU3500 上不存在。

**判停分支**：`HD PROMPTER` 变灰 → 检查是否 HDCU5000/5500 且启用了 SDI-RET；`NETWORK TRUNK` 改不动 → 检查 `FIBER TRANSMIT RATE` 是否 ULTRA；找不到 `UHD PROMPTER` → 机型为 HDCU3500 或 `UHD-SDI D` 未选 IN；提示机无信号 → 先核 `PROMPTER CH` 与接口方向，再转 led-diagnostics。

**输出契约**：报告 = 命中页（M01/M02）+ 逐项原样取值与单位 + 页码 + 前置条件（速率档、接口方向、机型、选件）与"固定/仅显示"标记。

## B — 边界

- **不要用本卡**：音频/对讲（ccu-audio-intercom）；菜单操作通法（ccu-menu-operation）；接口规格与固定项汇总速查（ccu-specs-reference）；连接方式与 CABLE TYPE 决策（连接类卡）。
- **手册警告的失败模式**：`FIBER TRANSMIT RATE=ULTRA` 下强改 `NETWORK TRUNK` → 固定为 `NETWORK+VIDEO`，改不动（ce26，第 75 页）；HDCU5000/5500 用 SDI-RET 时误以为 HD PROMPTER 坏掉 → 实际固定 DISABLE（第 75 页 M02）；把固定值 `PROMPTER2/VBS-RET=ENABLE`、`UHD-SDI B I/O=OUT` 当菜单卡死（ce38，第 31/30 页）；HDC5500 摄像机侧提示器误接 `PROMPTER2` → "PROMPTER2 接口不支持此信号"，须接 `PROMPTER1`（ce21，第 14 页）；Tally 输入固定 `CONTACT`，按针脚表盲接会失败（ce39，第 76 页）。
- **型号差异**：`UHD TRUNK`、`UHD PROMPTER` **仅 HDCU5000/5500** 可用（第 30 页 S02）；`HD/UHD PROMPTER` 的 SDI-RET 抢占固定规则明确写在"HDCU5000/5500"（第 75 页）；HDCU3500 无 UHD 提示机通路。
- **作者盲点（阶段 0 批判）**：手册对干线/提示机只给"设置值 + 说明"，无"提示机黑屏 → 查哪几步"的处置树；`PROMPTER CH` 的取值"随所连摄像机的提示机线路编号变化"，具体映射手册未给；`IP-RET3` 作为 HD PROMPTER 源时的完整前置（网络侧）依赖网络卡；`DATA RATE` 的可选性还受连接与摄像机能力影响，手册未穷举。
