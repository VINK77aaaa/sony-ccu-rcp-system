> 吸收单元: [RCP] network-setup, mcs-operations, specs-reference, engineer-mode-security（RCP 卡）; [CCU] f01, f02, f03, f04, f07, f12, f14, f15, p09, p10, p68, ce12, ce14, ce15, ce16, ce33, g01, g02, g04, g08, g09, g77, g78, g79, g80, g81, g82, g85（CCU verified id）

# 整系统组网与联调（RCP 面板 + CCU 主机 + 摄像机） (RCP-3500/3501 + HDCU5000/5500/3500)

## R — 原文

**RCP 手册（遥控面板侧）**

- "更改连接模式 (CNS) 后,需重启所有摄像机系统。"（RCP 第 5 页）
- "此接口用于连接 CCU 的 RCP/CNU 接口或 CNU 的 RCP 接口。"（RCP 第 15 页，CCU/CNU REMOTE 接口 8 芯母式多接口）
- "使用 CCA-5 电缆从 CCU 到本机的最大连接长度为 200 m。"（RCP 第 16 页）
- "如果 RCP 编号重复, 则设备无法正常工作。"（RCP 第 19 页）

**CCU 手册（摄像机控制单元侧）**

- "用于通过 CCA-5 连接电缆连接到 MSU-1000 系列主设置装置、CNU-700 摄像机指令网络装置或 RCP-3000/1000 系列遥控面板。…使用 RCP-3000/1000 系列设备时, 还提供电源。"（CCU 第 12/13 页，RCP/CNU 接口 圆形 8 芯）
- "CNS MODE LEGACY、 BRIDGE、 MCS 设定通信模式。"；"CCU NO 当在 CNS MODE 中选择 MCS 时:空白, 1 至 96；当在 CNS MODE 中选择 LEGACY 或 BRIDGE 时:空白, 1 至 96, A 至 Z"（CCU 第 79 页 N02 <CNS SETTINGS>）
- "FIBER TRANSMIT RATE HIGH、 ULTRA、 --- … ULTRA:当已连接 HDC5000/5500 或 HDC3500 (安装有 HKC-FB50)时"（CCU 第 29 页 S01 <CAMERA I/F>）
- "当 <CAMERA I/F> t FIBER TRANSMIT RATE 设为 ULTRA 时,将其设为 NETWORK+VIDEO (固定) 。"（CCU 第 75 页 M02）
- "始终将 LAN1 和 LAN2 设为相同的链接速度。如果设置不同,则无法进行正常操作。"（CCU 第 79 页 N01）
- "更改 PORT 设置后重启本机。"（CCU 第 81 页 N06 <IP LIVE>）
- "显示在 CCU 菜单中设置的摄像机编号。当摄像机编号为 0 时,LAN COM 接口的 IP 地址和子网掩码会定期滚动显示。"（CCU 第 9 页 d CCU 编号显示屏）

## I — 自述

**一条控制链的两半。** RCP 只管"操作界面"，CCU 只管"信号处理与接口"，摄像机才是被控对象。面板手册写"怎么接、怎么编号、怎么配 IP"，主机手册写"这条链的另一端长什么样"。任何"整系统能不能通"的问题都必须同时核对两端——本卡就是这条接缝。

**物理连接的两端。** 控制信号走 CCA-5 专线：RCP 侧 CCU/CNU REMOTE 接口（8 芯母式多接口，第 15 页）↔ CCU 侧 RCP/CNU 接口（圆形 8 芯，第 12/13 页）。CCU 侧 LAN COM 接口（RJ-45 8 芯，10BASE-T/100BASE-TX/1000BASE-T）用于"RCP/MSU 设备连接和 IP 计数器输入"（第 15 页）——BRIDGE/MCS 面板可走这条网口。CCU 侧另有两个易混"干线"：NETWORK TRUNK 接口（RJ-45 8 芯，把摄像机侧 NETWORK TRUNK 设备旁路到网络）与 TRUNK 接口（圆形 12 芯，RS-232C/RS-422A 串行，最多 2 频道）——与菜单项 M02 的 NETWORK TRUNK 是三回事。

**编号与 IP 的一致性。** RCP 侧 CNS MODE ↔ CCU 侧 CNS SETTINGS 的 CNS MODE 必须同值；RCP 侧"主机 IP 地址"就是 CCU 侧 MASTER IP ADDRESS；RCP 编号与 CCU NO 必须全系统唯一且对应。CCU 前面板"CCU 编号显示屏"显示的就是 CCU NO（第 9 页）。取值域不同：CCU NO 在 MCS 下只能 1 至 96，LEGACY/BRIDGE 下可 1 至 96 或 A 至 Z；CCU 侧 MCS MODE 固定为 CLIENT（仅显示），主设备由 RCP 侧"主机 IP"指认。

**传输方式决定面板可用功能。** 整系统格式集由 CCU 侧 CABLE TYPE + FIBER TRANSMIT RATE + SYSTEM + CAMERA FORMAT 四开关派生；面板侧没有 CABLE TYPE 概念，但面板上一切"能不能调"都受所连 CCU/摄像机能力约束（RCP 手册反复写"因所连设备而异"）。两条硬联动：ULTRA 时 CCU 把 NETWORK TRUNK 固定为 NETWORK+VIDEO；LAN1/LAN2 必须同速，否则报 CCU:LINK SPEED MISMATCH。

**投运顺序与重启范围。** 先物理（线、供电、接地）→ 再 CCU 侧系统配置 → 再面板侧 CNS/IP/编号 → 最后统一重启。重启范围要分清：RCP 侧改 CNS 要求"重启所有摄像机系统"；CCU 侧改 IP Live 的 PORT 要求"重启本机"。两端都改过就按整系统重启执行——就大不就小。面板侧"看不到某功能"往往是选件缺失的下游结果（映射表见 B 段）。

## A1 — 书中配置示例

以下均为**书中配置示例**（原书自带拓扑/画面示例值，非实际工程记录）：

1. **LEGACY**（RCP 第 5 页）：CCU（HDCU5000/5500/3500）CNS:Legacy、CCU 编号 (1–96、A–Z)，与 RCP-3500/3501（CNS:Legacy）用 CCA-5 直连；该模式"TCP/IP 和 RCP 编号无需设定"（RCP 第 18 页）。
2. **MCS**（RCP 第 7 页）：MSU-1500 = 192.168.0.201（Master）；CCU n = 192.168.0.n（主机 IP 192.168.0.201、CCU 编号 n）；RCP m = 192.168.0.(100+m)（主机 IP 192.168.0.201、RCP 编号 m）。
3. **IP 连接**（CCU 第 6 页，c03）：装 HKCU-SFP50；LAN1/LAN2 接 10G/25G IP 交换机；LAN-COM 接 RCP/MSU 与 IP 计数器；系统含 IP Live System Manager × 2、PTP 主站 × 2、SNMP 管理器（需 HZCU-SNMP50）、Ember+ 软件（需 HZCU-CNFG50）。

**原书未提供"两端同时配置"的完整联调案例**（两本手册各自只写自己那一端）；上述拓扑是拼合两端示例值得到的端到端画面。

## A2 — 未来触发

**情境**：

1. 新装/搬迁整机位："面板、CCU、摄像机刚上架，怎么把它调通。"
2. 组网变更后整系统行为异常：加机位、Legacy 改 LAN、换主设备。
3. 两端编号/IP 对不上："面板连不上 CCU / CCU 前面板编号和面板上填的不一样。"
4. 换 CCU 或换摄像机型号后："为什么面板上某些项不见了 / 调不了。"

**语言信号**：中文——"整系统 / 联调 / 投运 / 两端 / 面板连 CCU / CNS / 编号 / 主机 IP / CCA-5 / LAN-COM / 重启所有摄像机系统 / 选件"；英文——"system integration / commissioning / CNS / CCU number / master IP / CCA-5 / LAN COM"。

**相邻区分**：

- **network-setup（RCP 卡）**：只面板一侧的 CNS/IP/编号配置归彼卡；**跨两端的 CNS↔CNS SETTINGS 一致性、编号↔CCU NO 对应、投运顺序 → 才走本卡**。
- **mcs-operations（RCP 卡）**：系统建好后的控制权仲裁归彼卡；本卡只管把系统配通。
- **led-diagnostics（RCP 卡）**：单面板侧灯语判读归彼卡；**两端灯语对照与联合排障 → 走 system-troubleshooting**。
- **specs-reference（RCP 卡）**：线材/长度/电压/针脚纯数值速查归彼卡（禁止换算）；本卡用这些数值做联调决策。
- **ccu-network-setup / ccu-*（CCU 卡）**：只主机一侧的 IP/CNS/PTP/格式/同步配置归各卡；本卡负责它与面板侧的对应关系。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：①物理连线——面板↔CCU 走 CCA-5 还是 LAN，摄像机↔CCU 走哪种传输（FIBER / COAX / COAX(HDCE) / SINGLE-MODE FIBER）；②系统规模——单机还是多机，有无 MSU/CNA-1；③两端编号与 IP 规划；④所连摄像机型号与两端选件清单；⑤两端固件/软件版本是否兼容（CCU 第 3 页）。任一不明先问，不得静默猜值。

1. **物理层核对**：CCA-5 ≤200 m；LAN ≤100 m、屏蔽型 5e 类线、IEEE802.3af PoE 集线器；纯 LAN 连接必须接地（RCP 第 16 页）；CCU 侧光纤接口不接时盖防尘盖。
2. **摄像机侧传输方式（CCU 侧）**：CABLE TYPE → FIBER TRANSMIT RATE → SYSTEM → CAMERA FORMAT。判据：连 HDC5000/5500 或装 HKCU-FB50 的 HDC3500 → ULTRA；连 HDC3500（未装 FB50）/HDC3100/HDC2000 系列 → HIGH；COAX/COAX(HDCE) → ---。
3. **同步与网络（CCU 侧）**：非 IP 系统设 GENLOCK MODE=HD/SD；ST2110 系统必须设 NETWORK（需 HKCU-SFP50，免外部参考）。IP 系统再设 LAN1/LAN2 同速、25G FEC 与对端交换机一致。
4. **两端 CNS 一致性核对**：两侧 CNS MODE 必须同值；LEGACY 无需 IP/编号，BRIDGE 需目标 IP，MCS 需主机 IP + RCP 编号。
5. **编号与 IP 唯一性复查（两端一起看）**：RCP 编号、CCU NO、各 IP 全系统无重叠；CCU NO 取值域随 CNS MODE。
6. **选件与能力核对**：按 B 段映射表逐项确认两端能力一致；缺件项不得承诺可用。
7. **投运顺序与重启**：CCU 侧 → RCP 侧 → 统一重启。**判停**：RCP 侧改了 CNS → "重启所有摄像机系统"；CCU 侧改了 IP Live 的 PORT → "重启本机"；两者都改 → 按整系统重启，重启后复查两端编号/IP。
8. **验收清单**：线长/线材达标；接地完成（纯 LAN）；CCU 编号显示屏与面板 RCP 编号对应无重叠；面板 NETWORK 灯亮、CCU 前面板 RCP/MSU 灯亮；状态画面 System Status 页（01/11）的 Reference / CCU No. / RCP/MSU 符合预期；改过的项已重启。

**判停分支**：物理层不通（CCU 侧 CABLE ALARM 亮、CABLE CONDITION 降级）→ 先查线缆与端面（转 system-troubleshooting / led-diagnostics）；编号/IP 冲突 → 本卡内改正并重启；面板可操作但某功能调不动 → 查所连设备支持范围与选件。

**输出契约**：报告 = 选定传输方式 + 两端 CNS 模式 + 编号/IP 对照表（原样）+ 选件清单 + 已执行的重启项 + 验收清单勾选结果。

## B — 边界

- **不要用本卡**：单面板侧 CNS/IP 配置（network-setup）；单主机侧网络/格式/同步配置（ccu-* 各卡）；控制权仲裁（mcs-operations）；灯语判读（led-diagnostics / ccu-panel-diagnostics）；数值速查（specs-reference）；两端灯语对照排障（system-troubleshooting）。**单设备侧配置 → 走各自卡；跨两端的联调与一致性检查 → 才走本卡。**
- **手册警告的失败模式**：改 CNS 后不重启所有摄像机系统（RCP 第 5 页）；RCP 编号/IP 重叠 → 设备无法正常工作（RCP 第 19 页）；LAN1/LAN2 异速 → CCU:LINK SPEED MISMATCH（CCU 第 79 页）；ULTRA 下强改 NETWORK TRUNK（CCU 第 75 页固定值）；单模光纤误接 HDC5000/5500（CCU 第 15 页）；未核对版本即投运（CCU 第 3 页）；接入无安全保护的网络（RCP 第 3 页）。
- **选件 ↔ 两端能力映射表**：HKCU-SFP50 → LAN1/LAN2 + IP Live/NMOS/PTP；HKCU-SDI50 → UHD-SDI E–H（仅 HDCU5000）；HKCU-SM50 → 单模光纤（仅连 HDC3500/3100、HDC2000 系列）；HZCU-UHD35 → 4K 输出；HZCU-CNFG50 → Ember+；HZCU-SNMP50 → SNMP。
- **型号差异**：RCP-3500/3501 组网规则完全一致。CCU 侧：HDCU5000 双 CAMERA FIBER、支持 HKCU-SDI50、4 km；HDCU5500/3500 单 CAMERA FIBER、2 km；HDCU3500 入门仅 HD，连 HDC5000/5500 需 HKCU-FB50。选件安装仅限受训技术人员（CCU 第 14 页）。
- **作者盲点（阶段 0 批判）**：①两本手册各自只写自己那一端，**没有"两端编号↔机位"的统一对照表**，本卡一致性规则由两端定义拼合而成；②"重启所有摄像机系统"的具体范围未明示；③CCU 侧 RCP/CNU 接口只写"使用 RCP-3000/1000 系列设备时提供电源"，未提 RCP-3500/3501 是否也从该口取电（后者另有 EXT I/O POWER IN 10.5 V 至 17 V 与 PoE 两种口径），两端未对齐，供电方案须按实机确认。