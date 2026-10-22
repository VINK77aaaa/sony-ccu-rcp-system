> 吸收单元: f08, f09, f10, f32, p17（案例素材 c14；反例 ce22, ce27, ce38；术语 g13†, g14†, g15, g16, g17, g18, g52, g53, g54, g55, g56, g64, g66；参考项 p19, p73；**缺口 f31**）

# 输出/返回格式派生与查表 (HDCU5000/5500/3500)

## R — 原文

- SDI-OUT1：MONITOR `C`——"C:不添加字符。此项固定为 C。"；FORMAT——"FIBER TRANSMIT RATE 为 HIGH 且 SYSTEM 为 1.001(525):请参阅第 54 页 …ULTRA 且 SYSTEM 为 1.000(625):请参阅第 63 页"。 (第 36 页，S07)
- SDI-OUT4：MONITOR `C`、`M`——"当此项设为 C (不添加字符)时,将不会显示 CCU MENU。若要显示,将 DISP/MENU 杆保持在 MENU 位置 3 秒钟。" (第 37 页，S07)
- UHD-SDI A：OETF `SDR`、`4K OETF`——"设置视频输出的伽马曲线。" (第 40 页，S09)
- IP-OUT3：MONITOR `C`、`M`——"当 SOURCE 设为 CAMERA 时固定为 M。当 SOURCE 设为 HD TRUNK 时固定为 C。"；OETF 仅 `SDR`；COLOR 仅 `BT709`；SOURCE `CAMERA`、`HD TRUNK`。 (第 45 页，S11)
- "IP-OUT4是专用 4K 输出的设置。当 HZCU-UHD35 选件启用时,HDCU3500 支持输出。" (第 45 页，S11)
- RETURN SELECT："设置要输入的返回信号的格式。"；"当安装了 HKCU-SFP50 时,可以在 HDCU5000/5500 上选择 IP-RET1、IP-RET2、IP-RET3 和 IP-RET4。"；"当安装了 HKCU-SDI50 时,可以在 HDCU5000 上选择 UHD-SDI G 和 UHD-SDI H。" (第 46 页，S12)
- RETURN FORMAT IP：IP-RET1/2＝`1080/59.94P`、`1080/50P`、`1080/59.94I`、`1080/50I`；IP-RET3＝`1080/59.94I(PsF)`、`1080/50I(PsF)`；IP-RET4＝`3840×2160/59.94P/12G`、`3840×2160/50P/12G`。 (第 47 页，S16)
- "UHD-SDI A 和 UHD-SDI B 是专用输出接口,无法配置返回格式。" (第 49 页，返回格式表页眉)
- "对于带下划线的格式,可以根据所连接摄像机的 Live HDR 模式设置在 HDR 和 SDR 之间切换模式。" (第 54 页，输出格式表页眉)
- "UHD-SDI B 、UHD-SDI C、UHD-SDI D、UHD-SDI E、UHD-SDI F、UHD-SDI G 和 UHD-SDI H 设置与 UHD SDI A 设置关联。"；"当 SDI-OUT1 设为 4K 输出时,格式设置链接到 SDI-OUT1 设置。" (第 54 页，S09 输出表)
- "HFR 输出 (1080/50) 与 SDI-OUT1、 SDI-OUT2、SDI-I/O1 和 SDI-I/O2 关联。" (第 65 页，S09 输出表)
- 2SI DIAMOND MARK：`ON`、`OFF`——"此功能用于在 4K 双样本交错输出期间在 4K 颜色条右下方区域中显示如下所示的测试图案。如果链路 1 到 4 的连接正确,则显示 OK,否则不显示 OK。此功能可用于检查连接。" (第 69 页，V01)
- SDI-I/O 3（OUT）SIGNAL 可选 `SDI-OUT`、`HD TRUNK`；SDI-I/O 4（IN）SIGNAL 可选 `SDI-RET`、`HD PROMPTER`。 (第 29-30 页，S02)

## I — 自述

**本卡管什么。** 给定 (FIBER TRANSMIT RATE × SYSTEM × CAMERA FORMAT)，回答"某接口能出什么格式串、怎么设 MONITOR/OETF/COLOR/SOURCE"，以及"返回信号怎么分配、某返回口能收什么格式"。核心口径：**格式不是自由设定的，是查表结果**——所有 FORMAT 项都只写"请参阅第 54/56/58/63 页"。

**第一步：分清两张独立矩阵。** 输出与返回是两套独立的表，不要混：
- **输出矩阵**在 S07–S11：OUTPUT FORMAT1（SDI-OUT1-4）、OUTPUT FORMAT2（SDI-I/O1-4）、OUTPUT FORMAT3（UHD-SDI A-D）、OUTPUT FORMAT4（UHD-SDI E-H，仅装 SDI50）、OUTPUT FORMAT IP（IP-OUT1-4，仅装 SFP50）。
- **返回矩阵**在 S12–S16：RETURN SELECT（RET1-8 的来源分配）→ RETURN FORMAT1（SDI-RET1-4）、RETURN FORMAT2（SDI-I/O1-4）、RETURN FORMAT3（UHD-SDI C/D/G/H）、RETURN FORMAT IP（IP-RET1-4）。

**第二步：按 (FIBER TRANSMIT RATE, SYSTEM) 选页。** HIGH×1.001(525)→第 54 页；HIGH×1.000(625)→第 56 页；ULTRA×1.001(525)→第 58 页；ULTRA×1.000(625)→第 63 页。输出表在第 54–67 页，返回表在第 49–53 页。页选错，读出来的格式串全错。

**第三步：在页内定位接口段。** 输出表按接口分列（UHD-SDI / SDI-OUT1-2 / SDI-OUT3-4 / SDI-I/O1-2 / SDI-I/O3-4 / IP-OUT1-2 / IP-OUT3 / IP-OUT4），同一 CAMERA FORMAT 行下不同接口列的可用格式可能不同。例：CAMERA FORMAT=`UHD/59.94P (4K/HDR)` 时，SDI-OUT3/4 列只有 `1080/59.94P/3G-A`、`1080/59.94P/3G-B`、`1080/59.94I`、`720/59.94P *3`、`525/59.94I`；而 SDI-OUT1/2 列还能出 4K 的 `3840×2160/59.94P/SQD/3G-A` 等（第 54 页）。

**第四步：设好伴随项。**
- MONITOR：`C`＝不加字符、`M`＝加字符。**多数口固定 C**（SDI-OUT1/2、SDI-I/O1-4、UHD-SDI A-H、IP-OUT1、IP-OUT4）；只有 SDI-OUT3/4、IP-OUT2/3 可选；IP-OUT3 还随 SOURCE 固定（CAMERA→M、HD TRUNK→C）。
- OETF：SDI-OUT/SDI-I/O/IP-OUT 取 `SDR`、`HDR OETF`；**UHD-SDI 各口取 `SDR`、`4K OETF`**（取值集合随接口类型变化，不要一律写 SDR/HDR）。
- COLOR：`BT709`、`BT2020`；IP-OUT3 固定 `BT709`。
- SOURCE：仅 IP-OUT 有，取 `CAMERA`、`HD TRUNK`（IP-OUT1/2 固定 `CAMERA`）。

**返回侧的顺序不同：先分配、再查表。** 必须先在 S12 RETURN SELECT 把 RET1-8 各自指定到某个物理返回口（`SDI-RET1-4`、`SDI-I/O1-4`、`UHD-SDI C/D/G/H`、`VBS-RET`、`IP-RET1-4`），再到对应的 RETURN FORMAT 项设该口的格式。返回口的选择本身受选件限制：IP-RET1-4 需 HKCU-SFP50（HDCU3500 上 IP-RET4 另需 HZCU-UHD35）；UHD-SDI G/H 需 HKCU-SDI50（仅 HDCU5000）。返回侧还有 FRAME SYNCHRONIZER（`OFF`/`ON`，与 CCU VIDEO CONVERT 联动）与 VBS ASPECT（`SQUEEZE`/`LETTER BOX`/`EDGE CROP`）。

**关联链（一处设置牵动多处）。** ① UHD-SDI B/C/D/E/F/G/H 的格式**与 UHD-SDI A 关联**（第 54 页）——只设 A 即可，其余跟随。② 当 SDI-OUT1 设为 4K 输出时，SDI-I/O1/2 的格式设置**链接到 SDI-OUT1**（第 54 页）。③ HFR 输出与 SDI-OUT1、SDI-OUT2、SDI-I/O1、SDI-I/O2 关联（第 65 页）——HFR 只走这四口。④ 带下划线的格式随所连摄像机的 Live HDR 模式在 HDR/SDR 间切换（第 54 页）。

**边界一：UHD-SDI A/B 是专用输出。** 四张返回表页眉均注"UHD-SDI A 和 UHD-SDI B 是专用输出接口,无法配置返回格式"，RETURN SELECT 清单里也确实不含 A/B（第 49–53/46 页）。想把返送接到 A/B 是无效的。

**边界二：MONITOR 多数口固定。** SDI-OUT1/2 的 MONITOR 固定 C，不可加字符（ce27）；SDI-I/O1-4、UHD-SDI A-H、IP-OUT1、IP-OUT4 同样固定 C；IP-OUT3 随 SOURCE 固定。只有 SDI-OUT3/4 与 IP-OUT2/3 是可选 C/M 的。

**边界三：720 项分级前置。** 输出表 720 项带 `*3`＝"CCU VIDEO CONVERT 设为 ENABLE 时,可以选择 720 输出"（第 55 页）；返回表 720 项带 `*2`/`*3`＝需 CCU VIDEO CONVERT=ENABLE（`*3` 还须所连摄像机 HDR 模式 OFF）（第 52/53 页）。未满足前置，720 项不可选（详见 ccu-system-format）。

**边界四：4K 有 SQD / 2SI 两种链路编配。** 4K 格式串如 `3840×2160/59.94P/SQD/3G-A`、`3840×2160/59.94P/2SI/3G-A`——SQD（Square Division）与 2SI（2 Sample Interleave）是四链路（Link-1..4）的像素切分方式，直接决定线缆/链路编配。手册给的**接线自检手段**是 V01 的 2SI DIAMOND MARK：开启后，若链路 1–4 连接正确，4K 颜色条右下角会显示 `OK`，否则不显示 OK（第 69 页）。

**为什么不能"直接填格式值"。** 格式项在菜单里是**选择项**，候选集合由 (FIBER TRANSMIT RATE × SYSTEM × CAMERA FORMAT) 唯一确定；你不能手输一个表外的格式串。举例：CAMERA FORMAT=`1080/59.94I(2×)` 在 HIGH×1.001(525) 下，SDI-OUT1 列给的是 `1080/59.94I(2×)/Link1`（分链路），SDI-OUT2 列给的是 `1080/59.94I(2×)/Link2`（第 55 页）——同一格式在相邻两个口上被拆成不同 Link，这是表结构决定的，不是可自由指定。理解了这一点，就不会在"某口出不了目标格式"时误以为是菜单故障，而会先回上游核对三个开关。

## A1 — 书中配置示例

以下均为**书中自带表格/画面**（原书 S07–S16 与格式表、V01，非实际工程记录）：

1. **SDI-OUT3/4 列（HIGH×1.001(525) 输出表）**（第 54 页）：CAMERA FORMAT=`1080/59.94P` 时，SDI-OUT3/4 段读得 `1080/59.94P/3G-A`、`1080/59.94P/3G-B`、`1080/59.94I`、`720/59.94P *3`、`525/59.94I`。
2. **ULTRA×1.001(525) 输出表**（第 58 页）：原书给出各 CAMERA FORMAT 行 × 各接口列的完整格式串（含 `3840×2160/59.94P/12G`、`3840×2160/59.94P/SQD/3G-A`、`3840×2160/59.94P/2SI/3G-A`、`3840×2160/29.97PsF/SQD/1.5G` 等），并注明"4K 输出设置与 SDI-OUT1 设置关联"。
3. **RETURN FORMAT IP**（第 47 页，S16）：IP-RET1/2＝`1080/59.94P`、`1080/50P`、`1080/59.94I`、`1080/50I`；IP-RET3＝`1080/59.94I(PsF)`、`1080/50I(PsF)`；IP-RET4＝`3840×2160/59.94P/12G`、`3840×2160/50P/12G`。
4. **2SI DIAMOND MARK 自检**（c14，第 69 页）：V01 的 `2SI DIAMOND MARK` 设为 ON 后，原书配两张对照图——"正确的连接"（链路 1–4 正确→显示 OK）与"交换链路 1 和链路 2 时"（不显示 OK）。
5. **接口→信号功能随方向变化**（第 29–30 页，S02）：SDI-I/O 3 在 OUT 时 SIGNAL 可选 `SDI-OUT`/`HD TRUNK`；SDI-I/O 4 在 IN 时可选 `SDI-RET`/`HD PROMPTER`；UHD-SDI B 的 I/O 固定 `OUT`。

**书中未给完整示例的部分**：手册未给出"某现场从 CAMERA FORMAT 出发、逐接口列出全部输出/返回格式串"的端到端文字演算（格式表是图形化密集表格）。以下为**合成演练（非原书内容）**，仅演示本卡查表链的用法：

> 合成演练：FIBER TRANSMIT RATE=ULTRA，SYSTEM=1.001(525)，CAMERA FORMAT=`1080/59.94P(HDR/SDR)`。要查 SDI-OUT3 可用格式：① 方向=输出；② (ULTRA,1.001)→第 58 页；③ 定位 SDI-OUT3/4 段；④ 读得 `1080/59.94P/3G-A`、`1080/59.94P/3G-B`、`1080/59.94I`、`720/59.94P *3`、`525/59.94I`；⑤ 因 MONITOR 可选，按是否需要叠加字符选 C/M；OETF 取 SDR/HDR OETF。若目标 720，须先确认 CCU VIDEO CONVERT=ENABLE。

## A2 — 未来触发

**情境**：

1. 施工接线前："SDI-OUT3 / UHD-SDI A / IP-OUT1 能出什么格式"。
2. 返送配置："RET1 该接哪个口、能收什么格式、SD 要不要设纵横比"。
3. 4K 四链路接线后自检：用 2SI DIAMOND MARK 确认链路 1–4 是否接对。
4. 想给某口加菜单字符，却发现 MONITOR 改不动 → 回查是否固定 C。
5. 发现某接口格式与预期不符 → 回查 (FIBER TRANSMIT RATE, SYSTEM, CAMERA FORMAT) 是否设错。

**语言信号**：中文——"输出格式 / 返回格式 / 这个口能出什么 / 查表 / 第几页 / MONITOR / OETF / 色彩空间 / 返送口 / 4K 链路 / 2SI / SQD / 菱形标记"；英文——"output format / return format / lookup table / MONITOR / OETF / color space / RETURN SELECT / link mapping / 2SI diamond mark"。

**相邻区分**：

- **ccu-system-format**：彼卡管"选哪个 SYSTEM/CAMERA FORMAT"；本卡管"选好之后某接口出什么格式串"。问"该设什么格式"归彼卡，问"这个口出什么"归本卡。
- **ccu-transport-setup**：传输通路与 CABLE TYPE 归彼卡；本卡不回答"怎么接"。
- **ccu-hdr-setup**：OETF/COLOR SPACE 的取值随接口变化（UHD-SDI 为 `SDR`/`4K OETF`），但 HDR MODE/OETF 体系的设定归彼卡；本卡只管"在输出项上填哪个 OETF 值"。
- **干线/提示机卡**：SDI-I/O 3/4 的 HD TRUNK / HD PROMPTER 信号功能选择归干线卡；本卡只管这些口的**格式**。
- **规格速查（specs-reference）**：`12G`/`6G`/`3G-A`/`3G-B` 的标准号与速率纯查询归彼卡；本卡用这些格式串做输出配置。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：① 已确定的 FIBER TRANSMIT RATE 与 SYSTEM；② 已确定的 CAMERA FORMAT；③ 目标接口（具体到 SDI-OUTn / SDI-I/On / UHD-SDI X / IP-OUTn / IP-RETn）；④ 方向（输出还是返回）；⑤ 已装选件（HKCU-SDI50 / SFP50 / HZCU-UHD35）；⑥ 是否需要菜单字符、是否 4K 2SI、是否 HFR。任一缺失先询问。

1. **定方向**：输出 → 走 S07–S11 输出矩阵；返回 → 走 S12–S16 返回矩阵。
2. **选页**：按 (FIBER TRANSMIT RATE, SYSTEM) 四选一——54（HIGH,525）/56（HIGH,625）/58（ULTRA,525）/63（ULTRA,625）。返回表对应 49–53 页。
3. **定位接口段**：在页内找到目标接口所在的列（输出表按接口分列；返回表按 RETURN FORMAT1-3/IP 分段）。
4. **读格式串**：在 CAMERA FORMAT 对应行与该接口列的交点读出可用格式串（原样保留，如 `3840×2160/59.94P/SQD/3G-A`）。
5. **设伴随项**：MONITOR（注意多数口固定 C；仅 SDI-OUT3/4、IP-OUT2/3 可选）、OETF（SDI/IP 为 `SDR`/`HDR OETF`，UHD-SDI 为 `SDR`/`4K OETF`）、COLOR（`BT709`/`BT2020`；IP-OUT3 固定 `BT709`）、SOURCE（IP-OUT 取 `CAMERA`/`HD TRUNK`）。
6. **返回侧先分配**：到 S12 RETURN SELECT 把 RET1-8 指定到物理返回口（受选件限制），再到 RETURN FORMAT1-3/IP 设该口格式；SD 信号须设纵横比；确认 FRAME SYNCHRONIZER 状态与 CCU VIDEO CONVERT 一致。
7. **关联链核对**：若目标是 UHD-SDI B/C/D/E/F/G/H，确认只需设 A（其余跟随）；若 SDI-OUT1 为 4K，确认 SDI-I/O1/2 已链接；若为 HFR，确认只走 SDI-OUT1/2、SDI-I/O1/2。
8. **4K 2SI 自检**：4K 2SI 输出时开 V01 `2SI DIAMOND MARK`，观察 4K 颜色条右下角是否显示 `OK`；不显示即链路接错。
9. **收尾核对**：带下划线格式按所连摄像机 Live HDR 模式确认 HDR/SDR；720 项按 `*2`/`*3` 前置核对。

**判停分支**：读不到目标格式 → 回 ccu-system-format 核对三个上游开关；720 项不可选 → 按前置补 CCU VIDEO CONVERT / 摄像机 HDR OFF；接口想加字符但改不动 → 该口 MONITOR 固定 C（正常）；4K 显示不了 OK → 检查链路 1–4 接线顺序；**HFR 施工接线** → 依据不完整，见 B 段 f31 缺口，须回查原 PDF 图形或联系 Sony。

**输出契约**：报告 = 方向 + 查表页 + 接口 + 读出格式串（原样）+ MONITOR/OETF/COLOR/SOURCE 设定 + 返回分配 + 关联链核对 + 自检结论 + 未决项（含 HFR Link 编配）。

## B — 边界

- **不要用本卡**：SYSTEM/CAMERA FORMAT 的选择（ccu-system-format）、传输通路与 CABLE TYPE（ccu-transport-setup）、HDR MODE/OETF 体系设定（ccu-hdr-setup）、标准号与速率数值速查（specs-reference）、干线/提示机的信号功能选择（干线卡）。
- **手册警告的失败模式**：
  - UHD-SDI A/B 是专用输出，**无法配置返回格式**（ce22，第 49–53 页）——返送不要接 A/B。
  - SDI-OUT1/2 的 MONITOR **固定为 C**，不可加字符（ce27，第 36 页）——不要在固定项上反复尝试。
  - PROMPTER2/VBS-RET 被固定为 `ENABLE`，UHD-SDI B 的 I/O 被固定为 `OUT`（ce38，第 30/31 页）——固定值不是菜单卡死。
- **型号差异**：
  - **HDCU5000**：可装 HKCU-SDI50，解锁 `<OUTPUT FORMAT4>`（S10，UHD-SDI E/F/G/H）与 RETURN SELECT 里的 `UHD-SDI G`/`UHD-SDI H`（S15 注明"仅当在 HDCU5000 上安装了 HKCU-SDI50 时才会显示"）。
  - **HDCU5500**：不能装 HKCU-SDI50，故无 UHD-SDI E/F/G/H。
  - **HDCU3500**：`<OUTPUT FORMAT3>`/`<RETURN FORMAT3>`（UHD-SDI 返回）仅 HDCU5000/5500 或 HDCU3500（装 HZCU-UHD35）时显示；IP-RET4 在 HDCU3500 上需 HZCU-UHD35。
  - **选件依赖**：`<OUTPUT FORMAT4>` 仅装 HKCU-SDI50；`<OUTPUT FORMAT IP>`/`<RETURN FORMAT IP>` 仅装 HKCU-SFP50；RETURN SELECT 中 IP-RET1-4 需 SFP50、UHD-SDI G/H 需 SDI50。
- **作者盲点（阶段 0 批判）**：
  - **f31 缺口（必须标注）**：第 67 页"输出接口和 BNC 接口编配之间的关系"表（表头 HFR / UHD SDI A/E*1 B/F*1 C/G*1 D/H*1 / SDI OUT 1 2 / SDI I/O 1 2）在纯文本提取后**列对齐丢失**（原文出现 `4 K 2 × 1 2 G 2 1 6 0 P L i n k - 1 L i n k - 2 …`、`Li nk-3/4` 等断裂串），3×/6× 行与 3G-B 半链路"Link-1/2、Link-3/4…"形式的接口↔Link 对应关系**无法确证**，已判 `needs_review`（见 needs-review.md，被合并项 p21）。因此**HFR 施工接线的 Link 分配依据不完整**：本卡只能给出"2×/4×/8× 行的 Link-1..8 可读、HFR 只走 SDI-OUT1/2 与 SDI-I/O1/2"这类可确证结论；**6× 及 3G-B 半链路的完整 Link 映射须回查原 PDF 第 67 页图形（表格 OCR）或向 Sony 服务/销售代表确认**，不得凭文本臆断。
  - 手册多处写"有关设定的详细说明,请联系 Sony 维修代表或销售代表"（如 SDI 接口设定），属**故意留白**，本卡不编造步骤。
  - PsF（g13†）与 SQD/2SI（g14†）手册**只使用、未定义**，释义含行业常识，已列 needs-review；引用这些格式串时**必须原样保留**，不得改写或当逐行 P 处理。
  - 格式表是图形化密集表格，纯文本提取会丢失部分列对齐（尤其第 67 页），本卡只保留可文字化的映射规则。
  - 三型号共用同一套 FORMAT 项，但"仅在…时显示/可选"的差异贯穿全表，读任一格式项前先确认型号与已装选件。
