> 吸收单元: f26, p52, p53, p54, p55（支撑：c10、c16、ce11、ce39、g59、g61）

# 音频 / 对讲配置 (HDCU5000/5500/3500)

## R — 原文

- A01 MIC GAIN："CAM MIC GAIN CH1 (---)、20、30、40、50、60 dB"；"(---)：当摄像机未连接时显示 (仅显示)。"(第 72 页)
- A02 AUDIO OUT："DELAY 0、5、11、16、21、27、32、37、43、48、53、59、64、69、75、80 ms 设定摄像机的麦克风输出相位。"；"CH1 : LEVEL –20、0、+4 dBu"；"CH1 : ADJUST –99 至 99、0"。(第 72 页)
- A03 INTERCOM："PRODUCER INTERFACE CLEAR COM、4WIRE、RTS"；"SIDE TONE CANCEL –99 至 99 0 设定侧音取消电平。(当选中 CLEAR COM 或 RTS 时可以设置)"；"TERMINATION OFF、ON 设置终端电阻 (200 欧姆)。(当选中 CLEAR COM 或 RTS 时可以设置)"；"PGM1 INPUT LEVEL –20、0、+4 dBu"。(第 72 页)
- A04 FRONT INTERCOM："INTERCOM MIC DYNAMIC、ECM、CARBON"；"CARBON：碳素麦克风 (电源, 20 dB 增益)"；"ECM：驻极式电容麦克风 (电源, 40 dB 增益)"；"DYNAMIC：动圈式麦克风 (无电源, 60 dB 增益)"；"INTERCOM MIC GAIN –6、0、+6 dB"；"PGM MIX MODE OFF、INCOM+PGM、L-INCOM/R-PGM"。(第 73 页)
- A05 TEST TONE / A06 IP AUDIO / A07 IP INTERCOM（第 73-74 页）："SOURCE 1kHz"；"LEVEL 0、–10、–20、–30、–40、–50、–60、–70 [dB]"；IP 两页"仅在已安装 HKCU-SFP50 时才会显示"，"FORMAT L24/48kHz/1ms/2ch、…、L24/48kHz/0.125ms/16ch"。

## I — 自述

音频/对讲不是一页菜单，而是 AUDIO/INTERCOM 菜单下的**七个页面 A01–A07**，各管一段链路：

- **A01 MIC GAIN**：摄像机侧麦克风放大增益（CH1/CH2），是"送进来的"电平；
- **A02 AUDIO OUT**：CCU 侧输出的相位与格式——`DELAY` 16 档相位对齐、AES/EBU OUT、ANALOG OUT、CH1/CH2 的 LEVEL 与 ADJUST；
- **A03 INTERCOM**：**线路侧**——生产商线路（PRODUCER）与工程师线路（ENGINEER）各选 CLEAR COM / 4WIRE / RTS，通道数 1CH(PROD) 或 2CH(PROD&ENG)，外加 PGM1–3 输入电平；
- **A04 FRONT INTERCOM**：**面板侧**——前面板 INTERCOM 接口（XLR 5 芯）的耳机麦克风类型、增益、侧音、PGM 混合方式、PRIVATE 开关三态；
- **A05 TEST TONE**：1kHz 校准音源与送出通道；
- **A06 IP AUDIO / A07 IP INTERCOM**：IP 化后的音频/对讲格式串与通道顺序，**必须装 HKCU-SFP50 才出现**。

三条联动规律必须记住：①**麦克风类型绑定固定增益**——CARBON 电源 20 dB、ECM 电源 40 dB、DYNAMIC 无电源 60 dB；②`SIDE TONE CANCEL` 与 `TERMINATION` **仅当线路选 CLEAR COM 或 RTS 时可设**，选 4WIRE 时 TERMINATION 只剩"OFF 仅显示"；③`DELAY` 只能取 16 个离散档位之一，不能写任意毫秒数。

`(---)` 与"仅显示"两类标记最易误判为故障：摄像机未连接时 CAM MIC GAIN 显示 `(---)`；FRONT INTERCOM 的 MIC/PGM、I/F 项为"仅显示"回读项，不可编辑。

## A1 — 书中配置示例

手册**未给出**"从零配一条对讲线路"的过程性案例；以下均为**书中真实给出的示例值**：

1. 状态画面 *Audio*（07/11）示例值（第 17 页）：`Camera MIC Gain CH1 :60dB`、`CH2 :60dB`；`CCU AES/EBU Out :AES/EBU`；`CCU Analog Out :AES/EBU`。对照 A01 取值域（20/30/40/50/60 dB）可判定该示例取 60 dB 档。
2. 状态画面 *Intercom*（08/11）示例值（第 17 页）：`Camera Engineer :MIC On`、`Camera Producer :MIC Off`；`CCU MIC/PGM :MIC Off`、`CCU Line :System`。可直接核对面板 MIC/PGM 开关状态与线路连接状态。

以上 2 条为原书自带示例，非实际工程记录。**其余组合（如"RTS 线路 + TERMINATION ON + 侧音取消"）手册无现成算例，属合成演练（非原书内容）**，须按取值域逐项自证。

## A2 — 未来触发

**情境**：

1. 现场通信配置："对讲耳机说话对方听不到 / 侧音太大 / 生产商线路怎么选"。
2. 麦克风更换后电平不对："换了支动圈麦，增益怎么设 / 电容麦要不要供电"。
3. 音频相位对齐与校准："AUDIO OUT DELAY 取哪档 / 1kHz 测试音送哪个通道"。
4. IP 制作音频对接："IP 音频格式串填什么 / 为什么找不到 A06/A07"。

**语言信号**：中文——"对讲 / 内通 / 侧音 / 麦克风 / 增益 / 测试音 / 1kHz / 延迟 / 相位 / PGM / 生产商线路 / 工程师线路"；英文——"intercom / sidetone / mic gain / test tone / audio delay / PGM / 4-wire / CLEAR COM / RTS"。

**相邻区分**（初稿，阶段 3 回填）：

- **ccu-trunk-prompter**：本卡管音频/对讲（A01–A07）；彼卡管干线/提示机（M01/M02）。
- **ccu-menu-operation**：本卡给"设什么值"；"怎么进菜单、改值、输字符串"归彼卡。
- **ccu-specs-reference**：接口电气规格（INTERCOM/TALLY/IO PORT 的 0 dBu/–14 dBu、TALLY 固定 CONTACT）归彼卡。
- **led-diagnostics**：对讲异常的灯语判读归彼卡；本卡负责把配置改对。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：①用途——现场对讲 / 节目声 PGM / 校准测试音；②麦克风类型与接线方式——动圈 / 驻极（ECM）/ 碳素，平衡或非平衡（BALANCED/UNBALANCED）；③对讲线路制式——CLEAR COM / 4WIRE / RTS，1CH(PROD) 或 2CH(PROD&ENG)；④是否装 HKCU-SFP50；⑤相位对齐目标毫秒数。不明先问，不猜。

1. **前面板物理设定**（第 10 页）：`INTERCOM` 开关选 PROD/PRIV/ENG；`MIC/PGM` 开关选 ON/OFF/PGM；转动 `INTERCOM` 旋钮调耳机电平。**判停**：PRIVATE 开关设为 DISABLE 时，PRIV 位置会落到 ENG 或 PROD（见 A04 `PRIVATE SW` 三态）。
2. **A01 摄像机麦克风增益**：`CAM MIC GAIN CH1` / `CH2` 取 20、30、40、50、60 dB。**判停**：显示 `(---)` = 摄像机未连接（仅显示），非故障。
3. **A02 音频输出**（第 72 页）：`DELAY` 从 `0、5、11、16、21、27、32、37、43、48、53、59、64、69、75、80 ms` 中取**最近档**（不得写入区间外数值）；`AES/EBU OUT` 选 MIC1/2 或 AES/EBU；`ANALOG OUT` 选 MIC1/2 或 AES/EBU；`CH1/CH2 : LEVEL` 取 –20、0、+4 dBu，`CH1/CH2 : ADJUST` 取 –99 至 99。
4. **A03 对讲线路**（第 72 页）：`INTERCOM CH` 选 1CH(PROD) 或 2CH(PROD&ENG)；`PRODUCER INTERFACE` 与 `ENGINEER INTERFACE` 各选 CLEAR COM / 4WIRE / RTS；`SIDE TONE CANCEL`（PROD：–99 至 99；ENG：0 至 99）与 `TERMINATION`（200 欧姆）**仅 CLEAR COM / RTS 可设**；`PGM1/2/3 INPUT LEVEL` 各取 –20、0、+4 dBu。**判停**：若 `SIDE TONE CANCEL` / `TERMINATION` 不可设 → 当前选的是 4WIRE，回改线路制式后再设。
5. **A04 前面板对讲**（第 73 页）：`INTERCOM MIC` 按麦克风类型选——CARBON（电源 20 dB）/ ECM（电源 40 dB）/ DYNAMIC（无电源 60 dB），**类型与增益口径绑定，不得错配**；`INTERCOM MIC TYPE` 选 BALANCED / UNBALANCED；`INTERCOM MIC GAIN` 取 –6、0、+6 dB；`SIDE TONE LEVEL` 0 至 99；`PRIVATE SW` 三态按需选 ENABLE / DISABLE(SET TO ENG) / DISABLE(SET TO PROD)；`PGM MIX MODE` 选 OFF / INCOM+PGM / L-INCOM/R-PGM；`PGM SELECT` 选 PGM1 / PGM2 / PGM3 / PGM1+PGM2+PGM3；`PGM1/2/3 LEVEL` 0 至 99。
6. **A05 测试音**（第 73 页）：`SOURCE`=1kHz；`LEVEL` 取 0、–10、–20、–30、–40、–50、–60、–70 [dB]；`ANALOG OUT CH` / `IP OUT CH` 各取 NONE、ALL、MIC1、MIC2、AES/EBU1、AES/EBU2、INTERCOM ENG、INTERCOM PROD。
7. **A06/A07 IP 音频/对讲**（第 74 页，须装 HKCU-SFP50）：`FORMAT` 从 `L24/48kHz/1ms/2ch、L24/48kHz/1ms/4ch、L24/48kHz/1ms/8ch、L24/48kHz/0.125ms/2ch、L24/48kHz/0.125ms/4ch、L24/48kHz/0.125ms/8ch、L24/48kHz/0.125ms/16ch` 中选；`CH ORDER`——AUDIO OUT 为 MIC1/MIC2/AES/EBU1/AES/EBU2，HD TRUNK AUDIO OUT 为 THROUGH，PGM IN 为 PGM1/PGM2/PGM3，IP INTERCOM 收发均为 ENG/PROD。

**判停分支**：A06/A07 菜单不可见 → 未装 HKCU-SFP50；`AES/EBU` 相关项在 HDCU5000 上不可选（第 31 页，AES/EBU 仅 HDCU5500/3500）；出现不明音视频滚纹 → 先排查附近便携通信设备干扰（ce11）。

**输出契约**：报告 = 逐页（A01–A07）命中项 + 原样取值与单位 + 页码 + 前置条件（SFP50、线路制式、摄像机连接状态）。

## B — 边界

- **不要用本卡**：干线/提示机配置（ccu-trunk-prompter）；菜单操作通法（ccu-menu-operation）；接口规格速查（ccu-specs-reference）；灯语/状态画面判读（led-diagnostics）。
- **手册警告的失败模式**：附近用便携通信设备 → "造成故障并干扰音频和视频信号"（ce11，第 88 页）；`TERMINATION`/`SIDE TONE CANCEL` 在 4WIRE 下不可设，误以为卡死（第 72 页 A03）；麦克风类型与固定增益错配 → 电平口径全错（p52）；把 `CAM MIC GAIN` 的 `(---)` 误读为故障（p76）。
- **型号差异**：AES/EBU 输出——HDCU5000 有独立 `AES/EBU` 接口（BNC 型 1），HDCU5500/3500 为 `CHARACTER / SYNC / AES/EBU` 共用 BNC 接口，且"`AES/EBU` 仅适用于 HDCU5500/3500"（第 31 页、第 89-92 页）；A01–A05 对三型号一致，A06/A07 仅取决于是否装 HKCU-SFP50。
- **作者盲点（阶段 0 批判）**：手册对音频/对讲只给"设置值 + 说明"，无"现象 → 原因 → 处置"决策树；对讲线路物理接线（`INTERCOM/TALLY/IO PORT` D-Sub 50 芯引脚、`MIC/WF REMOTE` 第 36–43 芯）在接口页与 S03，本卡不展开；IP AUDIO/INTERCOM 的对接端要求、PGM 电平与侧音推荐值手册均未给。

