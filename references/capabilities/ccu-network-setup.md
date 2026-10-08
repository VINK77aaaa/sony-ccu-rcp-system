> 吸收单元: f14, f15, f35

# 网络与 IP 配置（IP ADDRESS / CNS / PING） (HDCU5000/5500/3500)

## R — 原文

- `<IP ADDRESS>` N01: "PORT LAN-COM、 LAN1、 LAN2 选择要为其设置 IP 地址的端口。" (第 79 页)
- 自动 IP: "如果重启本机,此 IP 地址可能会更改,并且只能用于设置目的。'自动 IP'功能仅适用于 LAN COM 接口。它不适用于 HKCU-SFP50 的 LAN 1 和 LAN 2 接口。" (第 79 页)
- 链路速度: "LINK SPEED 10G、 25G 显示链接速度。仅当选择了 LAN1 或 LAN2 时显示。始终将 LAN1 和 LAN2 设为相同的链接速度。如果设置不同,则无法进行正常操作。" (第 79 页)
- 25G FEC: "OFF、 RS-FEC(CL108)、 FC-FEC(CL74) 为 25G 设置 FEC 模式。仅当选择了 LAN1 或 LAN2 时显示。设为要连接的 IP 交换机的端口设置。" (第 79 页)
- `<CNS SETTINGS>` N02: "CNS MODE LEGACY、 BRIDGE、 MCS 设定通信模式。"；"CCU NO 当在 CNS MODE 中选择 MCS 时:空白, 1 至 96；当在 CNS MODE 中选择 LEGACY 或 BRIDGE 时:空白, 1 至 96, A 至 Z" (第 79 页)
- `<CNS SETTINGS>` N02: "MCS MODE CLIENT 表示当选择 MCS 模式时,本机会作为客户端 (仅显示) 。"；"MASTER IP ADDRESS 0.0.0.0 至 255.255.255.255 设定主设备的 MCS 模式 IP 地址。" (第 79 页)
- `<PING>` N17: "PORT LAN-COM、 LAN1、 LAN2 设置 PING 传输目的地端口。LAN1 和 LAN2 仅在安装了 HKCU-SFP50 时可用。" (第 86 页)
- `<PING>` STATISTICS: "PACKET LOSS 0 至 100 %"；"ROUND-TRIP MIN 0.0 至 1000000.0 ms" (第 86 页)

## I — 自述

本卡覆盖 `NETWORK` 菜单中**与"编址与连通性"有关**的三页: `<IP ADDRESS>`（N01）、`<CNS SETTINGS>`（N02）、`<PING>`（N17，虽列在 DIAGNOSIS 菜单但属网络连通性自检）。它**不含** ST2110 协议栈与第三方协议（N06-N16，归 `ccu-ip-live`），也**不含** Web 界面本身（N03，归 `ccu-web-menu`）。这三页是全 IP 系统的地基: 地址错、链路速度不一致、编号冲突，都会让上层任何配置失效。

**先分清三个端口**（g04/g79）。`LAN-COM` 是 1G 级控制/管理口，用 5 类以上屏蔽型电缆连集线器（`10BASE-T/100BASE-TX/1000BASE-T`），RCP/MSU 设备连接与 IP 计数器输入也用它；Web 菜单、Ember+、SNMP、TSL UMD、NMOS 均走此口。`LAN1` / `LAN2` 是 HKCU-SFP50 网络接口板的媒体口（SFP+ / SFP28），承载 IP 视频/音频输入输出、内部通信与网络同步；**未装 SFP50 时这两项在菜单里根本选不到**。因此"给哪个口配 IP"这个问题本身要先用选件与用途判定。

**N01 的编址链**是有序的: `PORT`（`LAN-COM` / `LAN1` / `LAN2`）→ `DHCP`（`ON` / `OFF`）→ `IP ADDRESS` / `SUBNET MASK` / `DEFAULT GATEWAY`（各 `0.0.0.0 至 255.255.255.255`）→ `SET`（显示 `SET OK?`，**再次按 ENTER 确认更改**）→ 当 DHCP 设为 `OFF` 时可用 `COPY TO STATIC ADDRESS`（把 DHCP 为 ON 时获得的地址复制到静态设置）。另有 `MAC ADDRESS`（显示每口 MAC，`000000000000 至 ffffffffffff`）。**"自动 IP"是这里最容易误用的机制**: 当 DHCP 为 `ON` 而网络上无可用 DHCP 服务器时，本机在本地分配唯一的链路本地地址（`169.254.0.0/16`）；但手册明确 **"'自动 IP'功能仅适用于 LAN COM 接口。它不适用于 HKCU-SFP50 的 LAN 1 和 LAN 2 接口。"**（第 79 页）且该地址"如果重启本机…可能会更改，并且只能用于设置目的"。这一限制全手册只出现一次，极易漏读。

**链路速度与 FEC 只对 LAN1/LAN2 有意义**。`LINK SPEED` 取值 `10G` / `25G`，**仅当选择了 LAN1 或 LAN2 时显示**；手册用了最强措辞: "**始终将 LAN1 和 LAN2 设为相同的链接速度。如果设置不同,则无法进行正常操作。**"（第 79 页）——这是硬约束，没有容错分支。`25G FEC` 取值 `OFF` / `RS-FEC(CL108)` / `FC-FEC(CL74)`，同样仅在选 LAN1/LAN2 时显示，"**设为要连接的 IP 交换机的端口设置**"，即必须与对端交换机端口一致。二者共同决定 IP 链路能否起得来。

**N02 通信模式**决定本机在摄像机控制网中的角色。`CNS MODE` 三选一 `LEGACY` / `BRIDGE` / `MCS`；`MCS MODE` 固定 `CLIENT`（仅显示，不可改）；`CCU NO` 的**取值域随模式变化**——MCS 下为 `空白, 1 至 96`，LEGACY 或 BRIDGE 下为 `空白, 1 至 96, A 至 Z`（即**只有 LEGACY/BRIDGE 能用字母编号**）；`MASTER IP ADDRESS`（`0.0.0.0 至 255.255.255.255`）设定 MCS 模式下主设备的 IP；`SET` 需再按 ENTER 确认。前面板还有一条相关约定: 摄像机编号不为 0 时，把 DISP/MENU 控制杆按在 DISP 位置 3 秒，CCU 编号显示区会滚动显示 LAN COM 的 IP 地址和子网掩码（第 10 页）——这是没有监视器时取本机 IP 的快捷法。

**CNS 模式还决定系统级行为，不只是本机的一个下拉框**（g49/g50/g90）。选 `MCS` 时本机作为客户端（`MCS MODE` 固定 `CLIENT`，仅显示）去连 `MASTER IP ADDRESS` 指定的主设备（如 MSU-1000/1500 或 CNU-700）；`CCU NO` 在本体系里对应 MSU 的摄像机选择编号，**编号重复会导致设备无法正常工作**。选 `LEGACY` 或 `BRIDGE` 时 `CCU NO` 才允许用字母（`A 至 Z`）。前面板还有一个关联约定: **摄像机编号为 0 时**，LAN COM 接口的 IP 地址和子网掩码会定期滚动显示（与"编号不为 0 时按 DISP 杆 3 秒"是两条不同触发路径）。此外 `MASTER IP ADDRESS` 是"主设备"的地址（本机作为客户端去连的对端），**不是本机自身 IP**——本机 IP 在 N01 的 `IP ADDRESS` 设，两者极易填反。

**N17 PING 是本机侧连通性自检**。`PORT` 可选 `LAN-COM` / `LAN1` / `LAN2`（**后二者仅在安装 HKCU-SFP50 时可用**）；`IP ADDRESS` 设目标；`PING`（通过 EXEC 执行）；`STATISTICS` 读结果: `TRANSMITTED PACKETS`（`0 至 5`）、`RECEIVED PACKETS`（`0 至 5`）、`PACKET LOSS`（`0 至 100 %`）、`ROUND-TRIP MIN` / `AVERAGE` / `MAX`（`0.0 至 1000000.0 ms`）。注意样本数上限只有 5 个包，判断质量时不宜只看单次结果。

**这三页是下游全部网络功能的公共地基，口径要一次对齐**。`LAN-COM` 的 IP 是 Web 菜单（N03）、Ember+（N13，TCP 9000）、TSL UMD（N14，UDP 8900）、SNMP（N15）以及 NMOS（N07，`PORT`=`LAN-COM`）的寻址前提——LAN-COM 地址没配好，这些服务即使开关打开也接不通。`LAN1` / `LAN2` 的 IP 与链路速度则是 IP Live（N06）、PTP 同步（N04/N05）、IP 音视频流的物理前提。`CNS MODE` 与 `CCU NO` 又是 RCP/MSU 侧能否识别本机的前提。因此本卡应在**装选件之后、启用任何上层协议之前**完成；顺序颠倒会出现"协议已开但连不上"的假象，实际是地基没打。

## A1 — 书中配置示例

手册**没有**给出带具体 IP 数值的 N01 配置演算，但有三处可直接引用的真实示例:

1. **状态画面 Network 页（09/11，第 17 页，c11）** —— 真实画面示例，可逐字读出链路状态: `LAN 1:Link Up   2:Link Up`、`SPD 1:25G   2:25G`、`FEC 1:RS-FEC   2:RS-FEC`、`LSM 1:Disconnected   2:Disconnected`、`PTP 1:Locked   2:Locked`。这是核对 LAN1/LAN2 是否同速、FEC 是否一致的现场样板（该页仅在装 HKCU-SFP50 时显示）。
2. **错误消息表（第 88 页，f30）** —— 真实条目: `CCU:LINK SPEED MISMATCH` = "LAN1 和 LAN2 的链路速度不匹配。"，与 N01 的 `LINK SPEED` 规则互证。
3. **前面板取 IP（第 10 页）** —— 真实操作说明: "当摄像机编号不为 0 时,仅当 DISP/MENU 控制杆在 DISP 位置保持 3 秒钟时,LAN COM 接口的 IP 地址和子网掩码会在固定时间内滚动显示。"

以下为合成演练（非原书内容）—— 手册未提供完整编址演算，故补一段端到端走查供参照:

- **输入**: LAN-COM 接 RCP/MSU 与 Web PC；LAN1/LAN2 接 25G IP 交换机；需 MCS 多机系统，本机 CCU 编号 12，主设备 `192.168.0.201`。
- **输出**: N01 `PORT`=`LAN-COM` → `DHCP`=`OFF` → 填 `IP ADDRESS`/`SUBNET MASK`/`DEFAULT GATEWAY` → `SET` 并再按 ENTER 确认；LAN1/LAN2 均 `LINK SPEED`=`25G`（**两者必须相同**）、`25G FEC`=`RS-FEC`（与交换机端口一致）；N02 `CNS MODE`=`MCS`、`CCU NO`=`12`、`MASTER IP ADDRESS`=`192.168.0.201`；N17 `PORT`=`LAN1`、`IP ADDRESS`=交换机地址、`PING` 执行，读得 `PACKET LOSS`=`0 %`、`ROUND-TRIP` 三项读数。

## A2 — 未来触发

**情境**：

1. 新机接入多机系统，要规划并落地 IP、子网、网关与 CCU 编号。
2. Web 菜单打不开，先要拿到 LAN-COM 的 IP/掩码（无监视器时用前面板 3 秒法）。
3. IP 交换机链路起不来（Link Down、速度不符、FEC 不匹配）。
4. 改完 IP 或模式后系统异常，需定位是编址问题还是上层问题。
5. 排障时要用本机侧 PING 验证到交换机/对端的连通性与丢包。

**语言信号**：中文——"配 IP / 子网 / 网关 / DHCP / 自动 IP / 链路速度 / 10G / 25G / FEC / CNS / CCU 编号 / 主设备 IP / PING / 丢包 / 往返延迟"；英文——"IP address / subnet mask / gateway / DHCP / link speed / FEC / CNS / CCU number / master IP / ping / packet loss"。

**相邻区分**：

- **ccu-genlock-sync**：本卡管端口 IP、链路速度、CNS、PING；彼卡管同步来源与 PTP 域号/相位。PTP 用的 LAN 端口地址在本卡设——同步锁不上时先回来查本卡的 LAN1/LAN2 是否同速。
- **ccu-ip-live**：本卡管 N01/N02/N17（基础编址 + 通信模式 + 连通性自检）；彼卡管 N06-N16（ST2110 流、NMOS、Ember+、SNMP、TSL UMD）。IP Live / NMOS 的 `PORT` 与地址在彼卡 N06/N07。
- **ccu-web-menu**：本卡提供 Web 访问所需的 LAN-COM IP；彼卡管 Web 界面本身（N03）。
- **指示灯与诊断卡**：错误消息与灯语判读归彼卡；本卡负责把编址配对。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：①端口清单与用途（LAN-COM 接 RCP/MSU/Web；LAN1/LAN2 接 IP 交换机）；②是否装 HKCU-SFP50（决定 LAN1/LAN2 与 N17 的 LAN1/LAN2 是否可用）；③IP 规划（各口 IP / 子网掩码 / 网关、是否 DHCP）；④IP 交换机端口速率与 FEC 设置；⑤CNS 模式与 CCU 编号 / 主设备 IP；⑥PING 目标地址。缺任一 → 先询问。

1. **端口与寻址判定**：`LAN-COM` = 1G 管理口（Web / Ember+ / SNMP / TSL / NMOS，且**自动 IP 仅此口生效**）；`LAN1` / `LAN2` = 仅装 SFP50 才有的 10G/25G 媒体口（IP 视频/音频、网络同步）。
2. **设 IP**（`NETWORK` → `<IP ADDRESS>` N01）：
   a. `PORT` 选目标口。
   b. `DHCP` = `ON` 或 `OFF`；若 `ON` 且无 DHCP 服务器 → 自动 IP（`169.254.0.0/16`，**仅 LAN-COM**，重启后可能变，仅供设置）。
   c. 填 `IP ADDRESS` / `SUBNET MASK` / `DEFAULT GATEWAY`（各 `0.0.0.0 至 255.255.255.255`）。
   d. `SET` → 显示 `SET OK?` → **再按 ENTER 确认**（用 ENTER 执行）。
   e. 由 `ON` 改 `OFF` 时，可用 `COPY TO STATIC ADDRESS` 复制静态地址。
3. **链路速度与 FEC**（仅 LAN1/LAN2 显示）：
   a. `LINK SPEED` = `10G` 或 `25G`；**LAN1 与 LAN2 必须相同**。
   b. `25G FEC` = `OFF` / `RS-FEC(CL108)` / `FC-FEC(CL74)`，须与对端交换机端口一致。
   c. **判停**：若出现 `CCU:LINK SPEED MISMATCH` 或链路起不来 → 回改到两端一致后再继续。
4. **CNS**（`NETWORK` → `<CNS SETTINGS>` N02）：
   a. `CNS MODE` = `LEGACY` / `BRIDGE` / `MCS`。
   b. `MCS MODE` 固定 `CLIENT`（仅显示）。
   c. `CCU NO`：MCS 下 `空白, 1 至 96`；LEGACY 或 BRIDGE 下 `空白, 1 至 96, A 至 Z`。
   d. `MASTER IP ADDRESS`（MCS 主设备地址，`0.0.0.0 至 255.255.255.255`）。
   e. `SET` 并确认。
5. **连通性自检**（`DIAGNOSIS` → `<PING>` N17）：
   a. `PORT` 选 `LAN-COM` / `LAN1` / `LAN2`（后二者仅装 SFP50 可用）。
   b. `IP ADDRESS` = 目标。
   c. `PING`（EXEC）执行。
   d. 读 `STATISTICS`：`TRANSMITTED PACKETS` / `RECEIVED PACKETS`（`0 至 5`）、`PACKET LOSS`（`0 至 100 %`）、`ROUND-TRIP MIN` / `AVERAGE` / `MAX`（`0.0 至 1000000.0 ms`）。

**判停分支**：全丢包 → 查物理链路/交换机/对端 IP；部分丢包 → 查线缆质量与 FEC / 速度；`CCU:LINK SPEED MISMATCH` → 回步骤 3 同速；CCU 编号或 IP 与系统其他设备重叠 → 本卡只保证本机设置，系统级唯一性需另行核对。

**输出契约**：报告 = 各口 `PORT` / `DHCP` / `IP` / `SUBNET MASK` / `DEFAULT GATEWAY`（**原样保留**）+ `LINK SPEED` + `25G FEC` + `CNS MODE` / `CCU NO` / `MASTER IP ADDRESS` + PING 统计读数。

## B — 边界

- **不要用本卡**：PTP 同步参数（→ `ccu-genlock-sync`）；ST2110 / NMOS / Ember+ / SNMP / TSL UMD 协议配置（→ `ccu-ip-live`）；Web 界面操作（→ `ccu-web-menu`）；灯语与错误消息全表判读（→ 指示灯与诊断卡）。
- **手册警告的失败模式**：①**LAN1/LAN2 链路速度不一致 → "无法进行正常操作" / `CCU:LINK SPEED MISMATCH`**（ce14，第 79/88 页）；②在 LAN1/LAN2 上依赖"自动 IP" → 不生效（ce15，第 79 页，自动 IP 仅 LAN-COM）；③`RECALL` 不含 LAN COM 的 IP / 子网掩码 / 默认网关，换机恢复后网络设置不会回来，须单独重设（ce29，第 78 页）；④接入无安全保护的网络 → 未授权第三方可能访问本装置（ce32，第 94 页）。
- **型号差异**：`LINK SPEED`、`25G FEC` 与 N17 的 `LAN1` / `LAN2` 端口选项**仅在选择了 LAN1 或 LAN2 / 安装 HKCU-SFP50 时可用或显示**（第 79/86 页）；未装 SFP50 时只有 `LAN-COM` 可设。IP Live / NMOS 相关菜单同理不显示。
- **作者盲点（阶段 0 批判）**：①**"自动 IP 仅适用于 LAN COM"这一关键限制只在 N01 说明里出现一次**（BOOK_OVERVIEW §3），极易漏读；②LAN1/LAN2 同速要求无容错或告警恢复说明；③CCU 编号与 IP 的**系统级唯一性**手册只给取值域、不给核对表；④`PING` 统计样本数上限仅 5 个包（`0 至 5`），样本偏小，手册未说明可重复执行；⑤多处写"请联系 Sony 销售或服务代表"，SFP+ 模块兼容清单不在本手册。

## 补充: 字段速查与"改完不生效"的定位

**N01 字段与取值（原样保留）**: `PORT`=`LAN-COM`/`LAN1`/`LAN2`；`DHCP`=`ON`/`OFF`；`IP ADDRESS`、`SUBNET MASK`、`DEFAULT GATEWAY` 各 `0.0.0.0 至 255.255.255.255`；`MAC ADDRESS`=`000000000000 至 ffffffffffff`；`LINK SPEED`=`10G`/`25G`（仅 LAN1/LAN2）；`25G FEC`=`OFF`/`RS-FEC(CL108)`/`FC-FEC(CL74)`（仅 LAN1/LAN2）。`SET` 是**两段式执行**——先显示 `SET OK?`，再次按 ENTER 才生效；未做第二次确认，改动不会落地，这是"改完不生效"的第一嫌疑点。

**N02 字段与取值（原样保留）**: `CNS MODE`=`LEGACY`/`BRIDGE`/`MCS`；`MCS MODE`=`CLIENT`（仅显示）；`CCU NO`=MCS 下 `空白, 1 至 96`、LEGACY/BRIDGE 下 `空白, 1 至 96, A 至 Z`；`MASTER IP ADDRESS`=`0.0.0.0 至 255.255.255.255`；`SET` 同为两段式。

**N17 字段与取值（原样保留）**: `PORT`=`LAN-COM`/`LAN1`/`LAN2`（后二者需 HKCU-SFP50）；`IP ADDRESS`=`0.0.0.0 至 255.255.255.255`；`PING`（EXEC 执行）；`STATISTICS`=`TRANSMITTED PACKETS`/`RECEIVED PACKETS`（`0 至 5`）、`PACKET LOSS`（`0 至 100 %`）、`ROUND-TRIP MIN`/`AVERAGE`/`MAX`（`0.0 至 1000000.0 ms`）。

**"改完不生效"定位顺序**: ①确认 `SET OK?` 已第二次确认；②确认改的是**目标端口**（`PORT` 选错会把 LAN-COM 的地址写到 LAN1 上）；③确认 DHCP 与静态地址不冲突（`ON` 时静态值可能被覆盖）；④确认 LAN1/LAN2 同速、FEC 与对端一致；⑤若换机后 `RECALL` 恢复过设置，记住 **RECALL 不含 LAN COM 的 IP/子网/网关**，网络必须单独重设。
