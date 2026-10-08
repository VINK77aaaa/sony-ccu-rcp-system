> 吸收单元: f24, f36, p48, p75, p76

# 状态画面判读（11 页） (HDCU5000/5500/3500)

## R — 原文

- "可以使用连接到 CHARACTER、SDI OUT 3 或 SDI OUT 4 接口的视频监视器监视 CCU 系统状态。要使用 SDI OUT 3 或 SDI OUT 4 接口,请将设置菜单中的 SYSTEM CONFIG t <OUTPUT FORMAT1> t SDI-OUT3 或 SDI-OUT4 t MONITOR 设为 M。" (第 15 页)
- "若要显示状态画面：将 DISP/MENU 控制杆设定到 DISP 位置。将显示最近查看的状态屏幕页面 (首次打开电源时,将显示摄像机设置页面)。转动 CONTROL 旋钮更改显示的页面。若要退出状态画面显示：在状态画面显示模式,将 DISP/MENU 控制杆设定到 DISP 位置。" (第 15 页)
- "摄像机未连接时,各项目显示 "-"标记。"；"Reference:所用参考信号格式以及同步锁定状态 (未输入参考信号时会显示 "Not Detected")" (第 16 页)
- "UHD-SDI 接口：仅在已安装 HKCU-SDI50 时才会显示。"；"IP-OUT 接口：仅在已安装 HKCU-SFP50 时才会显示。"；"网络状态：仅在已安装 HKCU-SFP50 时才会显示。"；"IP 流状态：仅在已安装 HKCU-SFP50 时才会显示。" (第 17-18 页)
- "MESSAGE：ALL、WARNING、OFF 设置摄像机自动设置操作状态的消息显示、系统中发生的警告等。ALL:显示全部信息。WARNING:显示系统警告信息和菜单控制信息。OFF:仅显示菜单控制信息。" (第 71 页，V07 DISPLAY)
- "LEVEL GATE … (---):当摄像机未连接时显示 (仅显示)。"；"CAM MIC GAIN CH1 … (---):当摄像机未连接时显示 (仅显示)。" (第 70 页 V05 / 第 72 页 A01)
- "当 <OUTPUT FORMAT1> t SDI-OUT4 t MONITOR 设为 C (不添加字符)时,可以将DISP/MENU 杆保持在 MENU 位置 3 秒钟以强制显示 CCU MENU。" (第 18 页)

## I — 自述

状态画面是 CCU 的"体检面板"：把系统状态、各 SDI 接口的输入/输出信号格式、音频与对讲状态、网络状态、警告等集中显示在 11 页里，供现场巡检逐页翻看。进入方式是前面板 DISP/MENU 控制杆拨到 DISP 位置，转动 CONTROL 旋钮换页，再拨 DISP 退出。

**接监视器有前置条件**：状态画面必须经 CHARACTER、SDI OUT 3 或 SDI OUT 4 接口输出。若用 SDI OUT 3 或 SDI OUT 4，必须先把 `SYSTEM CONFIG → <OUTPUT FORMAT1> → SDI-OUT3 或 SDI-OUT4 → MONITOR` 设为 **M**（添加字符）；若监视器接的是 CHARACTER 接口，则无需改 SDI-OUT3/4 的 MONITOR。注意第 18 页的反向规则：当 SDI-OUT4 的 MONITOR 被设为 **C** 时，CCU MENU 不显示，需要把 DISP/MENU 杆**保持在 MENU 位置 3 秒钟**才能强制显示。

11 页有固定页序，且**部分页依赖选件才显示**：UHD-SDI 页（Multi Format3/4）仅装 HKCU-SDI50 时出现；Multi Format IP、Network、IP Stream 页仅装 HKCU-SFP50 时出现。巡检时"看不到某页"往往不是故障，而是选件未装。

判读的两个通用约定：①**摄像机未连接时各项目显示 "-"**，`Reference` 未输入参考信号时显示 "Not Detected"——这些是"未连接/未输入"约定，**不是故障**（p76/ce34）；②显示哪些摄像机设置项可在 `VIDEO/MONITOR <DISPLAY>` V07 里开关（MESSAGE 有 ALL/WARNING/OFF 三档）。

## A1 — 书中配置示例

以下为**书中给出的状态画面示例**（原书第 16-18 页自带 11 页画面文字，即 c07–c13，非作者经历案例）：

1. *System Status*（01/11，第 16 页）：`Camera Format :1080/59.94P`、`Camera Cable :Connected`、`Cable Type :Fiber Camera Cable`、`Power Supply :On`、`Cable Length : 100m`、`CAM OK`、`CCU OK`、`Reference :Not Detected / Unlock`、`CCU No.:96 RCP/MSU:Connected`。
2. *Multi Format1*（02/11，第 16 页）：`SDI-OUT 1:1080/59.94P/3G-A OETF:HLG_BT.2100 Color:BT.2020`（1-4 口同型）。
3. *Multi Format2*（03/11，第 16 页）：`SDI-I/O 1:1080/59.94P/3G-A`、`3:(HD Trunk)`、`4:(Disable)`。
4. *Multi Format3/4*（04–05/11，第 17 页，仅装 HKCU-SDI50）：`UHD-SDI A-H 3840x2160/59.94P/12G OETF:HLG_BT2100 COLOR: BT2020`。
5. *Multi Format IP*（06/11，第 17 页，仅装 HKCU-SFP50）：`IP-OUT 3:C 1080/59.94P/3G-A … SOURCE:HD TRUNK`。
6. *Audio*（07/11）/ *Intercom*（08/11，第 17 页）：`MIC Gain CH1 :60dB`、`AES/EBU Out :AES/EBU`；`Engineer :MIC On`、`Line :System`。
7. *Network*（09/11，第 17 页，仅装 HKCU-SFP50）：`LAN 1:Link Up 2:Link Up`、`SPD 1:25G`、`FEC 1:RS-FEC`、`LSM 1:Disconnected`、`PTP 1:Locked`、`Ref :1080/50I Locked`、`RDS :Connected`。
8. *IP Stream*（10/11，第 18 页，仅装 HKCU-SFP50）：OUT/IN 两列流清单，`-----:无传入/传出流`。
9. *Alarm*（11/11，第 18 页）：`CCU:PS FAN STOP`、`CCU:GENLOCK ERROR`（告警条目，处置见第 88 页错误消息表与 ccu-panel-diagnostics）。

## A2 — 未来触发

**情境**：

1. 现场巡检："这台 CCU 现在什么状态 / 逐页看一下"。
2. 接监视器无画面："接了监视器看不到菜单 / 状态画面 / 怎么调出来"。
3. 输出格式核对："某 SDI 口实际出的是什么格式 / OETF / 色彩空间对不对"。
4. 网络与同步核对："LAN1/LAN2 链接速度、PTP 锁没锁、LSM/RDS 状态"。
5. 告警读取："Alarm 页有哪些告警 / 对应什么意思"。
6. 界面信息过多或过少："状态画面显示项要精简/补全"。

**语言信号**：中文——"状态画面 / 状态显示 / 11 页 / 巡检 / 翻页 / System Status / Multi Format / Audio / Intercom / Network / IP Stream / Alarm / 接监视器 / 看不到菜单 / MONITOR / Not Detected / 显示 - / 显示项"；英文——"status screen / status display / page / multi format / alarm page / monitor out / not detected"。

**相邻区分**：

- **ccu-panel-diagnostics**：本卡负责"在状态画面上读全量信息"，灯语（看灯定位层级）归彼卡。灯先亮→彼卡分层，再回本卡读页。
- **ccu-diagnosis-menu**：状态画面显示的是"运行态"，DIAGNOSIS 菜单读的是"硬件级自诊断（板卡/电源/风扇/版本）"。要"逐页看系统状态"→本卡；要"查板卡/风扇/版本"→彼卡。
- **ccu-file-log**：Alarm 页把告警"读出来"，但日志的导出/清除/改日期风险归彼卡。
- **ccu-system-format / ccu-network**（输出格式配置 / 网络与 IP 配置，如有独立卡）：本卡只"核对"格式与网络状态；要"改"格式或 IP 归彼卡。问"实际出什么格式"→本卡；"怎么改成某格式"→彼卡。
- **RCP `led-diagnostics`**：RCP 面板侧灯语与状态判读归彼卡；本卡是 CCU 主机侧状态画面。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：①监视器接哪个口——CHARACTER / SDI OUT 3 / SDI OUT 4；②当前 SDI-OUT3/4 的 MONITOR 设定值（C 还是 M）；③要看哪一类信息（系统/格式/音频/对讲/网络/IP 流/告警）；④是否装了 HKCU-SDI50 / HKCU-SFP50（决定对应页是否存在）。接法与选件不明先问，不臆测页面缺失原因。

1. **接通监视通路**（前置）：
   - 接 CHARACTER 接口 → 可直接显示状态画面与菜单，无需改 SDI-OUT3/4。
   - 接 SDI OUT 3 或 SDI OUT 4 → 先设 `SYSTEM CONFIG → <OUTPUT FORMAT1> → SDI-OUT3 或 SDI-OUT4 → MONITOR = M`（第 15/18 页）。
2. **进入与翻页**：DISP/MENU 控制杆拨到 DISP → 显示最近查看的页（首次上电显示摄像机设置页）→ 转动 CONTROL 旋钮换页 → 再拨 DISP 退出（第 15 页）。
3. **逐页判读**（页序固定，共 11 页）：
   - 01/11 System Status；02/11 Multi Format1（SDI-OUT）；03/11 Multi Format2（SDI-I/O）；04/11 Multi Format3（UHD-SDI，需 SDI50）；05/11 Multi Format4（UHD-SDI，需 SDI50）；06/11 Multi Format IP（需 SFP50）；07/11 Audio；08/11 Intercom；09/11 Network（需 SFP50）；10/11 IP Stream（需 SFP50）；11/11 Alarm。
4. **按显示约定判读**：摄像机未连接 → 各项目显示 "-"；`Reference` 无输入 → "Not Detected"；音频 `(---)`/`(---)` → 未连接（仅显示）。以上均非故障。
5. **判停分支**：
   - 接了 SDI OUT4 却看不到菜单 → 检查 MONITOR 是否为 C；是则把 DISP/MENU 杆保持在 MENU 位置 3 秒强制显示（第 18 页）。
   - 找不到某页（如 Network / IP Stream）→ 先确认是否装 HKCU-SFP50 / HKCU-SDI50；未装即属正常，非故障。
   - Alarm 页有告警 → 转 ccu-panel-diagnostics / ccu-diagnosis-menu 定位层级。
   - 显示项过多/过少 → 到 `VIDEO/MONITOR <DISPLAY>` V07 调 MESSAGE（ALL/WARNING/OFF）与各 ON/OFF 项。
6. **验证**：核对目标页字段与预期一致；告警页清空或已转介。

**输出契约**：报告 = 监视通路（口 + MONITOR 设定）+ 已读页清单（页号/标题）+ 关键字段判读（格式串/OETF/色彩空间原样）+ 告警条目（原样）+ 转介项。

## B — 边界

- **不要用本卡**：灯语判读（ccu-panel-diagnostics）、硬件诊断菜单（ccu-diagnosis-menu）、日志导出/清除（ccu-file-log）、改输出格式或 IP（ccu-system-format / ccu-network）、RCP 面板侧判读（RCP `led-diagnostics`）。
- **手册警告的失败模式**：
  - 接 SDI OUT3/4 未设 MONITOR=M → 无画面（第 15 页）。
  - SDI-OUT4 MONITOR=C 时菜单不显示，需 3 秒强制显示（第 18 页）。
  - 把摄像机未连接时的 "-" / "Not Detected" / "(---)" 误判为故障（ce34，第 16/70/72 页）。
  - 把"未装选件所以没有该页"误判为故障（第 17-18 页显隐条件）。
- **诚实留白**：手册**未给出**"某字段出现异常值时应如何处置"的步骤，状态画面只提供"读值/读状态"；Alarm 页条目本身也无处置，须交叉第 88 页错误消息表。此外 IP Stream 页 `-----` 仅表示"无传入/传出流"，是否异常需结合业务判断，手册未展开。
- **型号差异**：UHD-SDI 页（Multi Format3/4）仅装 HKCU-SDI50（HDCU5000）时显示；IP-OUT / Network / IP Stream 页仅装 HKCU-SFP50 时显示；HDCU5500/3500 与 HDCU5000 的可装选件不同（SDI50 仅 5000）。字段示例中的 `3840x2160/59.94P/12G`、`1080/59.94P/3G-A`、`25G`、`RS-FEC` 等须原样保留，不得换算。
- **作者盲点（阶段 0 批判）**：状态画面大量内容依赖**截图**，纯文本提取会丢失版面；能力卡只保留可文字化的页序、字段名与显隐条件。字段释义（如 Reference、RDS、PTP）须与网络/同步卡交叉，避免重复定义。
