> 吸收单元: f07, p09, p10, p11, p12, p13, p14, p20（反例 ce26, ce33；术语 g10, g11, g12, g18, g19, g20, g77, g82）

# 系统格式配置 (HDCU5000/5500/3500)

## R — 原文

- SYSTEM：`1.001(525)`、`1.000(625)`——"选择系统的工作频率。" (第 33 页，S05)
- CAMERA FORMAT 在 `FIBER TRANSMIT RATE=ULTRA` 且 `SYSTEM=1.001(525)` 时可选：`3840×2160/59.94P(2×)`、`3840×2160/59.94P`、`3840×2160/29.97P`、`3840×2160/23.98P`、`1080/59.94P`、`1080/29.97PsF`、`1080/23.98PsF`、`1080/59.94I (RGB444)`、`1080/29.97PsF (RGB444)`、`1080/23.98PsF (RGB444)`、`1080/59.94P(2×)`、`1080/59.94P(3×)`、`1080/59.94P(4×)`、`1080/59.94P(6×)`、`1080/59.94P(8×)`。 (第 33 页，S05)
- CAMERA FORMAT 在 `FIBER TRANSMIT RATE=HIGH` 且 `SYSTEM=1.001(525)` 时可选：`UHD/59.94P (4K/HDR)`、`1080/59.94P (4K/HDR)`、`1080/59.94P`、`1080/59.94I`、`1080/29.97PsF`、`1080/23.98PsF`、`720/59.94P`、`1080/59.94I (RGB444)`、`1080/29.97PsF (RGB444)`、`1080/23.98PsF (RGB444)`、`1080/59.94I(2×)`、`720/59.94P(2×)`。 (第 33 页，S05)
- "选择系统格式。可供选择的格式视连接的摄像机的有效格式而不同。" (第 33 页，S05)
- BIT DEPTH：`10BIT`、`12BIT`——"设置 RGB4:4:4 输出位长度,并更改 CCU 输出格式。仅当 CAMERA FORMAT 设为 1080/59.94I (RGB444)、1080/29.97PsF (RGB444)、1080/23.98PsF (RGB444)、1080/50I (RGB444)、1080/25PsF (RGB444) 或 1080/24PsF (RGB444) 时可以选择此项。" (第 34 页，S05)
- CCU VIDEO CONVERT：`DISABLE`、`ENABLE`——"当 CAMERA FORMAT 设置为以下项时,设置为 ENABLE。选择 ENABLE 时,将 FRAME SYNCHRONIZER 设为 ON。提示:当 CCU VIDEO CONVERT 设为 ENABLE 时, CCU 内的视频转换功能会引入延迟,可通过提前摄像机信号进行补偿。" (第 34 页，S05)
- FRAME CONVERT DELAY：`0.8`、`1.2`、`1.6 [F@23.98PsF]`——"设置 2-3 下拉的视频延迟时间。仅当 SYSTEM 为 1.001(525) 时启用此项。" (第 34 页，S05)
- HD-SD DELAY：`LINE`、`FRAME`——"当 CAMERA FORMAT 设为 1080 格式时,延迟时间显示如下。当选择 LINE 时:90H；当选择 FRAME 时:1F。当 CAMERA FORMAT 设为 720 格式时,延迟时间显示如下。当选择 LINE 时:120H；当选择 FRAME 时:2F。" (第 34 页，S05)
- "要进行 4K 输出,必须安装 HZCU-UHD35 4K/HDR 软件 (选件) 。" (第 14 页，HKCU-FB50)；HZCU-UHD35"支持将从摄像机传输的 HD 信号转换为 4K 信号。* 当安装了 HKCU-SM50 时,在 HDCU5000/5500 上支持此软件。" (第 3 页)
- "IP-OUT4 是专用 4K 输出的设置。当 HZCU-UHD35 选件启用时,HDCU3500 支持输出。" (第 45 页，S11)
- 格式表脚注："*3 当 CCU VIDEO CONVERT 设为 ENABLE 并且所连摄像机的 HDR 模式设为 OFF 时,可以选择 720 输入。" (第 52/53 页) / "*3 当 CCU VIDEO CONVERT 设为 ENABLE 时,可以选择 720 输出。" (第 55 页)
- "当 <CAMERA I/F> t FIBER TRANSMIT RATE 设为 ULTRA 时,将其设为 NETWORK+VIDEO (固定) 。" (第 75 页，M02)

## I — 自述

**本卡管什么。** 一台 CCU 的"信号能力源头"由四个开关共同决定：CABLE TYPE（在 ccu-transport-setup 里定）+ FIBER TRANSMIT RATE + SYSTEM + CAMERA FORMAT。本卡处理后三者，并覆盖它们派生的位深与延迟项。这四个开关不是自由设定，所有输出格式（OUTPUT FORMAT1-4 / OUTPUT FORMAT IP）与返回格式（RETURN FORMAT1-3 / RETURN FORMAT IP）都是它们的**派生查表结果**（查表动作见 ccu-format-lookup）。

**前置条件链（顺序不可颠倒）。**
1. **先判 4K 能力**：HDCU5000/5500 原生具备 4K；HDCU3500 仅 HD，要 4K 传输须先装 HKCU-FB50（等同 HDCU5500），要 4K **输出**还须再装 HZCU-UHD35（第 14 页）。IP-OUT4（专用 4K 输出）同样需 HZCU-UHD35（第 45 页）。注意 HZCU-UHD35 的适用范围受 HKCU-SM50 影响："当安装了 HKCU-SM50 时,在 HDCU5000/5500 上支持此软件"（第 3 页）。
2. **再定 SYSTEM**：`1.001(525)`（59.94 场频体系）或 `1.000(625)`（50 体系）。它决定后续 CAMERA FORMAT 候选集，也决定格式查表翻第 54/56 页（HIGH）还是第 58/63 页（ULTRA）。
3. **再定 FIBER TRANSMIT RATE**（本卡复用传输卡的结论）：`ULTRA`（连 HDC5000/5500 或装 HKC-FB50 的 HDC3500）或 `HIGH`（连 HDC3500（未装 HKC-FB50）/HDC3100/HDC2000 系列）。ULTRA 与 HIGH 的 CAMERA FORMAT 候选集**完全不同**：ULTRA 档能直接选 `3840×2160/59.94P` 等原生 4K 格式；HIGH 档只有 `UHD/59.94P (4K/HDR)` 与 `1080/59.94P (4K/HDR)` 这类由 HD 上转换的格式。
4. **再选 CAMERA FORMAT**：从 (FIBER TRANSMIT RATE × SYSTEM) 对应的那一套候选里选。手册明确"可供选择的格式视连接的摄像机的有效格式而不同"——候选表是**上限**，实际可用子集取决于所连摄像机。
5. **再设位深与延迟**：BIT DEPTH 只在 CAMERA FORMAT 为六个 `(RGB444)` 项时可选；CCU VIDEO CONVERT 与 FRAME SYNCHRONIZER 联动；FRAME CONVERT DELAY 只在 `SYSTEM=1.001(525)` 时启用；HD-SD DELAY 的换算值随 1080/720 而变。

**关键联动一：CCU VIDEO CONVERT ↔ FRAME SYNCHRONIZER。** 当 CAMERA FORMAT 设为需要转换的项时，CCU VIDEO CONVERT 必须设 ENABLE；一旦设 ENABLE，**必须**把返回信号的 FRAME SYNCHRONIZER 设为 ON（第 34 页，开关位置在 S12）。手册还提示：CCU 内视频转换会引入延迟，可通过提前摄像机信号补偿——这是现场对齐相位的依据。

**关键联动二：720 选项的分级前置（p20）。** 格式表里 720 相关项带脚注，分两档：`*3`（第 55 页输出侧）＝"CCU VIDEO CONVERT 设为 ENABLE 时,可以选择 720 输出"；`*3`（第 52/53 页返回侧）＝"CCU VIDEO CONVERT 设为 ENABLE **并且所连摄像机的 HDR 模式设为 OFF** 时,可以选择 720 输入"。也就是说，返回侧的 720 比输出侧多一道"HDR 模式 OFF"的闸门。若 CCU VIDEO CONVERT=DISABLE，标 `*3` 的 720 项根本不可选。

**关键联动三：ULTRA 锁定 NETWORK TRUNK。** 当 FIBER TRANSMIT RATE=ULTRA 时，`MAINTENANCE t <TRUNK/PROMPTER2> t NETWORK TRUNK` 被**固定**为 `NETWORK+VIDEO`（第 75 页，M02）。这不是可选项，而是 ULTRA 速率下的硬约束——配置干线模式时不要试图改成 NETWORK。相应地，DATA RATE（`100Mbps`/`1Gbps`）也只在 ULTRA 时可设。

**关键联动四：(FIBER TRANSMIT RATE, SYSTEM) 决定"去查哪一页"。** 这是本卡与 ccu-format-lookup 的分工接口。所有 FORMAT 项在 S07–S11 里都写成四条并列的指引：HIGH×1.001(525)→第 54 页；HIGH×1.000(625)→第 56 页；ULTRA×1.001(525)→第 58 页；ULTRA×1.000(625)→第 63 页。也就是说，本卡把 SYSTEM 与 FIBER TRANSMIT RATE 定死之后，输出/返回格式的候选集合页也就唯一确定了。若现场"按查表结果拿不到想要的格式串"，第一反应应是回本卡核对这两个开关是否设成了预期的组合，而不是去改查表方式。返回侧的页分流规则与输出侧完全一致（第 46 页 S12 给出同一组四页指引）。

**边界一：BIT DEPTH 的使能条件很窄。** 只有 CAMERA FORMAT 落在 `1080/59.94I (RGB444)`、`1080/29.97PsF (RGB444)`、`1080/23.98PsF (RGB444)`、`1080/50I (RGB444)`、`1080/25PsF (RGB444)`、`1080/24PsF (RGB444)` 这六项之内，BIT DEPTH 才出现/可选。选 `1080/59.94P` 等非 RGB444 格式时，该项无效。

**边界二：延迟项的值是"档位换算"而非自由填写。** FRAME CONVERT DELAY 的单位是 `[F@23.98PsF]`（帧数），只有 `0.8/1.2/1.6` 三档，且仅 525 系统可用；HD-SD DELAY 只让你选 `LINE` 或 `FRAME`，实际延迟被固定为 1080→90H/1F、720→120H/2F，不能任意填数。

**边界三：4K 能力分两层，别混。** "4K 传输"（HKCU-FB50 提供）与"4K 输出"（需 HZCU-UHD35）是两件事：只装 FB50 不等于能出 4K（第 14 页明确分层）。HDCU3500 的 IP-OUT4/IP-RET4 都需 HZCU-UHD35 才出现。

## A1 — 书中配置示例

以下均为**书中自带表格/画面**（原书 S05 页及格式表脚注，非实际工程记录）：

1. **CAMERA FORMAT 四套候选表**（第 33 页，S05）：原书按 (FIBER TRANSMIT RATE × SYSTEM) 给出四套完整清单——ULTRA×1.001(525)、ULTRA×1.000(625)、HIGH×1.001(525)、HIGH×1.000(625)。例：ULTRA×1.001 含 15 项（含 `3840×2160/59.94P` 等原生 4K 与 8 个 HFR 项）；HIGH×1.001 含 12 项（含 `UHD/59.94P (4K/HDR)`、`1080/59.94P (4K/HDR)` 与 3 个 `(RGB444)` 项）。
2. **CAMERA FORMAT → 转换输出对照表**（第 34 页，S05）：原书列出各 CAMERA FORMAT 对应的"转换输出"（如 `3840×2160/59.94P(2×)`→`3840×2160/59.94P`；`UHD/59.94P(4K/HDR)`/`1080/59.94P(4K/HDR)`→…；`1080/59.94P(2×)、(3×)、(4×)、(6×)、(8×)`；`720/59.94P`），并分 59.94 与 50 两组。
3. **BIT DEPTH 条件表**（第 34 页，S05）：原书明确六个可选项（前述六个 `(RGB444)` 格式）与取值 `10BIT`/`12BIT`。
4. **HD-SD DELAY 换算表**（第 34 页，S05）：原书给出 1080→`90H`/`1F`、720→`120H`/`2F`。

**书中未给完整示例的部分**：手册未给出"某现场从目标输出反推 SYSTEM/CAMERA FORMAT 并逐步演算"的端到端文字示例。以下为**合成演练（非原书内容）**，仅演示本卡决策链的用法：

> 合成演练：一台 HDCU3500，已装 HKCU-FB50，需输出 4K/HDR，SYSTEM=1.000(625)。① 4K 传输：FB50 已装，成立；② 4K 输出：须确认已装 HZCU-UHD35，否则 4K 输出不成立；③ FIBER TRANSMIT RATE=ULTRA（因 FB50 已装）；④ SYSTEM=1.000(625) 下，CAMERA FORMAT 候选为 `3840×2160/50P(2×)`…`1080/50P(8×)` 等 15 项；⑤ 若选 `1080/50P`，BIT DEPTH 不可选（非 RGB444）；⑥ 因 NETWORK TRUNK 在 ULTRA 下固定 `NETWORK+VIDEO`，不可改。结论：CAMERA FORMAT 在 ULTRA×1.000 清单内选，输出格式去 ccu-format-lookup 查第 63 页。

## A2 — 未来触发

**情境**：

1. 新系统联调："这台 CCU 设成什么系统频率和摄像机格式"。
2. 需要 4K / HDR / HFR 时：确认要不要装 FB50/UHD35，以及候选格式是否包含目标项。
3. 想选 720 输出或 720 返回，却发现菜单里没有该项 → 回查 CCU VIDEO CONVERT 与摄像机 HDR 模式。
4. 上下转换链相位对不齐 → 查 HD-SD DELAY / FRAME CONVERT DELAY / CCU VIDEO CONVERT 的延迟提示。
5. 配置干线（TRUNK/PROMPTER）时发现 NETWORK TRUNK 改不动 → 回查是否 ULTRA 锁定。

**语言信号**：中文——"系统频率 / 摄像机格式 / 传输速率 / 4K 输出 / 位深 / 720 选不了 / 格式候选 / 转换延迟 / 干线改不动"；英文——"SYSTEM / CAMERA FORMAT / FIBER TRANSMIT RATE / BIT DEPTH / CCU VIDEO CONVERT / frame convert delay / 4K output / HDR format"。

**相邻区分**：

- **ccu-transport-setup**：本卡管"通路建好后工作在哪一档频率/格式"；彼卡管"通路怎么建、CABLE TYPE 怎么定、要装什么选件、能拉多远"。FIBER TRANSMIT RATE 是交界项：彼卡判其取值依据，本卡用其取值结果派生 CAMERA FORMAT 候选集。
- **ccu-format-lookup**：本卡只负责"选定 SYSTEM/CAMERA FORMAT"这一步；"某接口最终能出什么格式串"归彼卡（第 54/56/58/63 页四页分流查表）。问"该选哪个 CAMERA FORMAT"归本卡，问"SDI-OUT3 能出什么"归彼卡。
- **ccu-hdr-setup**：CAMERA FORMAT 里带 `(4K/HDR)`、`(HDR/SDR)` 标注的项与 HDR 相关，但 HDR MODE / OETF / COLOR SPACE 的设定归彼卡。
- **规格速查（specs-reference）**：`90H`/`1F`/`120H`/`2F` 等数值的纯查询归彼卡；用这些值做延迟决策归本卡。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：① CCU 型号；② 摄像机型号；③ 目标输出分辨率/帧率（HD/4K、P/I、是否 HFR、是否 HDR）；④ 是否 IP 输出；⑤ 已装选件（HKCU-FB50 / SDI50 / SFP50 / SM50，HZCU-UHD35）；⑥ 系统频率体系（59.94 还是 50）。任一缺失先询问。

1. **4K 能力判定**（不满足即停）：要 4K 传输 → HDCU5000/5500 原生具备；HDCU3500 须装 HKCU-FB50。要 4K 输出 → 须装 HZCU-UHD35（第 14 页；第 45 页 IP-OUT4 同）。
2. **定 SYSTEM**：按现场场频体系选 `1.001(525)` 或 `1.000(625)`。
3. **定 FIBER TRANSMIT RATE**：由 ccu-transport-setup 的结论带入（`ULTRA` 或 `HIGH`；`COAX`/`COAX(HDCE)` 下为 `---`）。
4. **选 CAMERA FORMAT**：定位到 (FIBER TRANSMIT RATE × SYSTEM) 对应的第 33 页那一套清单，从清单内选目标格式；并**核对所连摄像机的有效格式**——候选表是上限，实际子集视摄像机而定。
5. **设 BIT DEPTH**（仅当上一步落在六个 `(RGB444)` 项时）：`10BIT` 或 `12BIT`。
6. **设 CCU VIDEO CONVERT 与 FRAME SYNCHRONIZER**：若 CAMERA FORMAT 为需转换项 → CCU VIDEO CONVERT=ENABLE；同时到 S12 把 FRAME SYNCHRONIZER 设为 ON。
7. **设延迟项**：`SYSTEM=1.001(525)` 时才可设 FRAME CONVERT DELAY（`0.8`/`1.2`/`1.6 [F@23.98PsF]`）；HD-SD DELAY 选 `LINE` 或 `FRAME`（值自动换算为 90H/1F 或 120H/2F）。
8. **720 前置检查**：若要选带 `*3` 的 720 输出项 → 确认 CCU VIDEO CONVERT=ENABLE；若要选带 `*3` 的 720 返回项 → 额外确认**所连摄像机 HDR 模式为 OFF**。
9. **收尾核对**：若 FIBER TRANSMIT RATE=ULTRA，确认 `NETWORK TRUNK=NETWORK+VIDEO`（固定，不可改）；核对系统配置设备的软件与 ROM 版本兼容（第 3 页）；把选定的 SYSTEM/CAMERA FORMAT 交给 ccu-format-lookup 去查实际接口格式。

**判停分支**：目标格式不在候选清单 → 回退检查 FIBER TRANSMIT RATE 与 SYSTEM 是否设错，或确认是否漏装 FB50/UHD35；720 项不可选 → 按第 8 步补前置；上下转换相位偏差 → 用第 7 步延迟项与"提前摄像机信号"补偿；格式派生结果异常 → 转 ccu-format-lookup。

**输出契约**：报告 = SYSTEM + FIBER TRANSMIT RATE + CAMERA FORMAT（原样格式串）+ BIT DEPTH（若适用）+ CCU VIDEO CONVERT/FRAME SYNCHRONIZER 状态 + 延迟项取值 + 720 前置核对结论 + 未决/需 Sony 确认项。

## B — 边界

- **不要用本卡**：CABLE TYPE 与传输通路决策（ccu-transport-setup）、某接口输出/返回格式串查表（ccu-format-lookup）、HDR MODE/OETF/COLOR SPACE（ccu-hdr-setup）、规格数值速查（specs-reference）。
- **手册警告的失败模式**：
  - FIBER TRANSMIT RATE=ULTRA 时 NETWORK TRUNK 被**固定**为 NETWORK+VIDEO，不可自由选（ce26，第 75 页）——试图强改会无效。
  - 操作前须核对本机与系统配置设备的软件和 ROM 版本兼容（ce33，第 3 页）——尤其换了 FB50/UHD35 之后。
  - CCU VIDEO CONVERT 设 ENABLE 却不把 FRAME SYNCHRONIZER 设 ON，会导致返回信号同步异常（第 34 页，p12）——这是最常见的联动漏配。
- **型号差异**：
  - **HDCU5000**：原生 4K；可装 HKCU-SDI50 解锁 UHD-SDI E/F/G/H（OUTPUT FORMAT4，S10 仅在装 SDI50 时显示）与 UHD-SDI G/H 返回（RETURN FORMAT3，S15）。
  - **HDCU5500**：1U 紧凑型，原生 4K；不能装 HKCU-SDI50（故无 UHD-SDI E/F/G/H）。
  - **HDCU3500**：仅 HD；须装 HKCU-FB50 才等同 HDCU5500（才有 4K 传输），须再装 HZCU-UHD35 才有 4K 输出（IP-OUT4/IP-RET4 同需 UHD35）。RETURN FORMAT3（UHD-SDI 返回）仅 HDCU5000/5500 或 HDCU3500（装 HZCU-UHD35）时显示（第 47 页，S15）。
  - **选件依赖**：`<OUTPUT FORMAT4>`（S10，UHD-SDI E/F/G/H）仅装 HKCU-SDI50 时显示；`<OUTPUT FORMAT IP>`/`<RETURN FORMAT IP>`（S11/S16）仅装 HKCU-SFP50 时显示；`BIT DEPTH` 仅在六个 RGB444 格式下出现。
- **作者盲点（阶段 0 批判）**：
  - "可供选择的格式视连接的摄像机的有效格式而不同"——手册未给出"哪台摄像机支持哪些格式"的完整对照表，实际可选子集依赖摄像机侧，本卡不臆造该对照。
  - 手册多处写"有关设定的详细说明,请联系 Sony 维修代表或销售代表"（如各接口设定），属**故意留白**，本卡不编造步骤。
  - 格式表脚注未穷举所有出现页（p20 已作边界），本卡引用的是典型页（52/53/55）。
  - SFP+/SFP28 模块兼容列表手册未给，须向 Sony 确认。
  - 三型号共用同一套菜单树，但"仅在…时显示/可选"的差异贯穿全表，阅读任一格式项时都要先确认当前型号与已装选件。
