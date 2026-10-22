> 吸收单元: f16, f17, f18, p35

# IP Live / NMOS / 第三方协议配置 (HDCU5000/5500/3500)

## R — 原文

- `<IP LIVE>` N06: "IP LIVE SYSTEM MANAGER PORT DISABLE、 LAN1&LAN2 … DISABLE:不与 LSM 通信。LAN1&LAN2:使用 LAN1 和 LAN2 与 LSM 通信 (用于实现冗余) 。更改 PORT 设置后重启本机。" (第 81 页)
- N06 MULTICAST ADDRESS: "当 PORT 设为 LAN1&LAN2 时固定为 AUTO,且使用从 LSM 配置的多播地址。当 PORT 设为 DISABLE 时固定为 MANUAL,且使用通过 MULTICAST ADDRESS 1 至 5 页手动设置的地址。" (第 81 页)
- `<NMOS>` N07 PORT: "DISABLE、 LAN-COM … 仅当 <IP LIVE> t IP LIVE SYSTEM MANAGER t PORT 设为 DISABLE 时才能选择。" (第 82 页)
- N07: "PORT NUMBER (IS-04 NODE) 100 至 65535、 3001"；"PORT NUMBER (IS-05 CONNECTION) 100 至 65535、 3002"；"RDS PORT NUMBER 100 至 65535、 18235" (第 82 页)
- N07 RDS DISCOVERY: "如果 RDS 在同一子网内不可用,请禁用此设置并手动设置 IP 地址。" (第 82 页)
- `<EMBER+>` N13: "EMBER+ DISABLE、 ENABLE … 可以通过安装 HZCU-CNFG50 摄像机升级软件 (选件)来启用。"；"PORT NUMBER 9000 显示 Ember+ 连接的 TCP 端口号。" (第 84 页)
- `<TSL UMD>` N14: "使用 TSL UMD V5.0 启用 / 禁用 IP 计数器。"；"PORT NUMBER 8900 显示 TSL UMD 连接的 UDP 端口号。" (第 84 页)
- `<SNMP>` N15: "可以通过安装 HZCU-SNMP50 摄像机升级软件 (选项)来启用。"；"NAME 显示系统名称 (ASCII 代码,最多 32 个字符) 。"；"RO COMMUNITY sony" (第 85 页)
- `<SNMP TRAP>` N16: "当启用 SNMP 时可选。当禁用 SNMP 时固定为 DISABLE。" (第 85 页)

## I — 自述

本卡覆盖 `NETWORK` 菜单中的 **ST2110 协议栈与第三方集成**部分: `<IP LIVE>`（N06）、`<NMOS>`（N07）、`<MULTICAST ADDRESS 1>`~`<MULTICAST ADDRESS 5>`（N08-N12）、`<EMBER+>`（N13）、`<TSL UMD>`（N14）、`<SNMP>`（N15）、`<SNMP TRAP>`（N16）。它与 `ccu-network-setup`（N01/N02/N17，编址与连通性）和 `ccu-web-menu`（N03，Web 界面）严格分工: **本卡只管"协议与流"**，不碰基础编址，也不碰 Web 界面。

**第一层前提是选件**。N06-N12 全部**仅在安装 HKCU-SFP50 时显示**（第 81-84 页）；N13 需 HZCU-CNFG50，N15/N16 需 HZCU-SNMP50（均为软件升级选件，通过 USB 密钥安装）；N14 无需额外选件但走 LAN-COM。因此"菜单里没有这一项"往往不是故障，而是选件未装。

**IP Live（LSM）是 ST2110 系统的中枢**。`IP LIVE SYSTEM MANAGER` 的 `PORT` 只有 `DISABLE`（不与 LSM 通信）与 `LAN1&LAN2`（用 LAN1 和 LAN2 与 LSM 通信，用于冗余）两个取值，且手册用加粗提示 **"更改 PORT 设置后重启本机。"**（第 81 页）——这是本卡最硬的约束之一。`DHCP` 固定 `OFF`；`PRIMARY IP ADDRESS` / `SECONDARY IP ADDRESS`（各 `0.0.0.0 至 255.255.255.255`）分别设 LSM1/LSM2 地址；`PRIMARY CONNECTION STATUS` / `SECONDARY CONNECTION STATUS` 读 `DISCONNECTED` / `CONNECTING` / `CONNECTED`；`HITLESS FAILOVER`（`ON` / `OFF`）启用 IP 流冗余。**多播地址被 PORT 锁定**: PORT 为 `LAN1&LAN2` 时 `MULTICAST ADDRESS` 固定 `AUTO`（用从 LSM 配置的地址），为 `DISABLE` 时固定 `MANUAL`（用 N08-N12 手动设的地址）——即"谁配多播地址"取决于 LSM 是否接管。

**NMOS 与 IP Live 互斥**，这是全卡最容易踩的顺序坑。N07 的 `PORT`（`DISABLE` / `LAN-COM`）**仅当 `<IP LIVE> t IP LIVE SYSTEM MANAGER t PORT 设为 DISABLE 时才能选择**（第 82 页）。也就是说: 想用 NMOS，必须先把 LSM 关掉（PORT=DISABLE）；两者不能同时启用。NMOS 的端口号: `PORT NUMBER (IS-04 NODE)`（Node API，发现/注册）范围 `100 至 65535`、默认 `3001`；`PORT NUMBER (IS-05 CONNECTION)`（Connection API，连接管理）范围 `100 至 65535`、默认 `3002`。`RDS DISCOVERY`（注册和发现系统）`ON` 时在同一子网内自动发现；**"如果 RDS 在同一子网内不可用,请禁用此设置并手动设置 IP 地址。"**，手动时填 `RDS IP ADDRESS` 与 `RDS PORT NUMBER`（范围 `100 至 65535`、默认 `18235`），并可读 `RDS CONNECTION STATUS`。注意此处的 RDS ≠ 调频广播的 Radio Data System，而是 NMOS 的 Registration & Discovery System（g40）。

**第三方协议三件套走 LAN-COM，各有独立端口与选件门槛**。`Ember+`（N13）: `DISABLE` / `ENABLE`，需 HZCU-CNFG50；`PORT` = `LAN-COM`；`PORT NUMBER` = `9000`（TCP）；读 `CONNECTION STATUS`。`TSL UMD`（N14）: `DISABLE` / `ENABLE`，用 **TSL UMD V5.0** 启用/禁用 IP 计数器；`PORT` = `LAN-COM`；`PORT NUMBER` = `8900`（**UDP** 端口）；`PACKET STATUS` 读 `NOT RECEIVED` / `RECEIVED`，收到时还显示 ID 与红/绿/黄计数器开/关状态，最多显示五个 ID，超过则显示 `AND MORE`。`SNMP`（N15）: `ENABLE` / `DISABLE`，需 HZCU-SNMP50；`PORT` = `LAN-COM`；`NAME` / `CONTACT` / `LOCATION` 各为 ASCII 最多 32 字符；`V1 ENABLE` / `V2C ENABLE` 分别开关 SNMP V1 与 V2C；`V1/V2C RO COMMUNITY` 默认 `sony`（ReadOnly 社区名，ASCII 最多 32 字符）；`ALLOW HOST` = `ANY`（允许所有 IP）或 `SPECIFIC`（仅允许 HOST1-3 IP ADDRESS 中配置的地址）。

**多播地址共 5 页（N08-N12），是 MANUAL 模式下的地址总账**，其页内结构固定、便于逐项核对: `<MULTICAST ADDRESS 1>`（N08）为 `VIDEO OUT`，含 `LAN1-1`~`LAN1-4` 与 `LAN2-1`~`LAN2-4` 共 8 组，每组含 `IP ADDRESS`（`224.0.0.1 至 239.255.255.255`，显示**传输**目的地）与 `PORT`（`100 至 65535`）；`<MULTICAST ADDRESS 2-1>`（N09）为 `RETURN LAN1-1`~`LAN1-4`，`<MULTICAST ADDRESS 2-2>`（N09）为 `RETURN LAN2-1`~`LAN2-4`，两者每组除 `IP ADDRESS` / `PORT` 外还含 `SRC IP`（`0.0.0.0 至 255.255.255.255`，显示流传输源，且此处的 `IP ADDRESS` 为**接收**目的地）；`<MULTICAST ADDRESS 3>`（N10）为 `AUDIO OUT LAN1` / `LAN2`、`HD TRUNK AUDIO OUT LAN1` / `LAN2`（传输向）与 `PGM IN LAN1` / `LAN2`（接收向，含 `SRC IP`）；`<MULTICAST ADDRESS 4>`（N11）为 `INTERCOM OUT LAN1` / `LAN2`（传输向）与 `INTERCOM IN LAN1` / `LAN2`（接收向，含 `SRC IP`）；`<MULTICAST ADDRESS 5>`（N12）为 `META OUT LAN1-1`~`LAN1-3` 与 `LAN2-1`~`LAN2-3`（共 6 组，传输向）。每页页首都有一条 `MULTICAST ADDRESS`（`AUTO` / `MANUAL`），用于**显示**当前模式——它随 N06 的 `PORT` 被锁定，不能在本页单独改。**方向是关键读法**: `VIDEO OUT` / `AUDIO OUT` / `HD TRUNK AUDIO OUT` / `INTERCOM OUT` / `META OUT` 是"显示传输目的地"，`RETURN` / `PGM IN` / `INTERCOM IN` 是"显示接收目的地"并多出 `SRC IP` 源地址项——配错方向会把收发地址填反。

**SNMP TRAP 是 SNMP 的子开关**（N16）: **"当启用 SNMP 时可选。当禁用 SNMP 时固定为 DISABLE。"** 即不能单独开启自陷。其字段包括 `COMMUNITY`（自陷社区名，ASCII 最多 32 字符）、`HOST1` / `HOST2` / `HOST3`（各含 `IP ADDRESS` 与 `VERSION`）、`VERSION`（`V1` / `V2C`）、`SEND TEST TRAP`（EXEC，发送测试自陷）。这里补上 p35 的字段规范要点: 所有社区名/主机名/位置均为 **ASCII 最多 32 字符**；`ALLOW HOST` 为 `SPECIFIC` 时授权地址落在 HOST1-3（仅允许列表内地址访问）。

## A1 — 书中配置示例

1. **连接示例（IP 连接，第 6 页，c03）** —— 真实书中示例。拓扑为: HDCU5000 / HDCU5500 装 **HKCU-SFP50**（脚注 c），其 **LAN 1 / LAN 2 接口接 IP 交换机**（脚注 d），**LAN-COM 接口接 RCP/MSU 与 IP 计数器**（脚注 e）；图中同时列出 **IP Live System Manager × 2、PTP 主站 × 2、IP 对讲机、IP 计数系统、多视图查看器、视频服务器、混音器**；并注明"要支持 SNMP 监视功能,请安装 HZCU-SNMP50"（脚注 f）、"要支持 Ember+ 控制,请安装 HZCU-CNFG50"（脚注 g）；交换机速率标注 `10G/25G`、`1G`、`10G/1G`。此例即"选件 ↔ 协议 ↔ 端口"的对照样板。
2. **状态画面 Multi Format IP（06/11，第 17 页，c09）** —— 真实画面示例，可读出 IP-OUT 各流格式与来源，例如 `3:C 1080/59.94P/3G-A … SOURCE:HD TRUNK`（流 3 来源为 HD TRUNK）；该页仅在装 HKCU-SFP50 时显示。
3. **状态画面 IP Stream（10/11，第 18 页，c12）** —— 真实画面示例，OUT / IN 两列流清单，`-----` 表示无流；同样仅在装 HKCU-SFP50 时显示。

以下为合成演练（非原书内容）—— 手册未提供完整协议配置演算，故补一段端到端走查供参照:

- **输入**: 装 HKCU-SFP50 与 HZCU-SNMP50、HZCU-CNFG50；LAN1/LAN2 接 10G/25G 交换机；LSM 主备地址已知；需 SNMP 网管与 Ember+ 控制；不需 NMOS。
- **输出**: N06 `PORT`=`LAN1&LAN2` → **重启本机** → 填 `PRIMARY IP ADDRESS` / `SECONDARY IP ADDRESS` → 观察 `PRIMARY/SECONDARY CONNECTION STATUS` 到 `CONNECTED`；`MULTICAST ADDRESS` 随 PORT 固定为 `AUTO`；`HITLESS FAILOVER`=`ON`；N13 `EMBER+`=`ENABLE`（`9000` TCP）；N14 `TSL UMD`=`ENABLE`（`8900` UDP）；N15 `SNMP`=`ENABLE`、`NAME`/`CONTACT`/`LOCATION` 各 ≤32 ASCII、`V1 ENABLE`+`V2C ENABLE`、`RO COMMUNITY`=`sony`、`ALLOW HOST`=`SPECIFIC` 且 HOST1 填网管地址；N16 `SNMP TRAP`=`ENABLE`（依赖 SNMP）、`VERSION`=`V2C`。

**对照的 NMOS 分支（同样为合成演练，非原书内容）**: 若现场不用 LSM 而用 NMOS 控制器，则必须先把 N06 `PORT` 设为 `DISABLE`（此时 `MULTICAST ADDRESS` 转为 `MANUAL`，需在 N08-N12 逐页手填地址），再把 N07 `PORT` 设为 `LAN-COM`，`PORT NUMBER (IS-04 NODE)`=`3001`、`PORT NUMBER (IS-05 CONNECTION)`=`3002`，并按 RDS 是否可用决定 `RDS DISCOVERY`=`ON` 或 `OFF`（`OFF` 时手填 `RDS IP ADDRESS` 与 `RDS PORT NUMBER`=`18235`）。两个分支互斥，**不能既开 LSM 又开 NMOS**。

## A2 — 未来触发

**情境**：

1. 全 IP / ST2110 演播室上电要接 LSM（IP Live System Manager），需配主备地址与冗余。
2. 要接 NMOS 控制器（IS-04/IS-05）或第三方网管/控制系统。
3. IP 计数器 / Tally 要走 TSL UMD，或要接 Ember+ 控制软件。
4. 要求 IP 流级无中断倒换（HITLESS FAILOVER）。
5. 改了 IP Live `PORT` 后配置"不生效"，怀疑漏了重启。
6. SNMP 自陷（Trap）开不起来。

**语言信号**：中文——"IP Live / LSM / ST2110 / NMOS / IS-04 / IS-05 / RDS / Ember+ / SNMP / SNMP TRAP / TSL / Tally / 多播 / 组播 / HITLESS FAILOVER / 冗余 / 改完不生效"；英文——"IP Live / LSM / ST2110 / NMOS / Ember+ / SNMP / TSL UMD / multicast / hitless failover"。

**相邻区分**：

- **ccu-network-setup**：本卡管 N06-N16 协议栈与多播地址；彼卡管 N01/N02/N17 端口编址、链路速度、CNS、PING。IP Live 用的 LAN1&LAN2 物理链路速度与 IP 在彼卡设——协议不通时先查彼卡的链路速度是否同速。
- **ccu-genlock-sync**：本卡管 IP 流与协议；彼卡管 PTP 同步（N04/N05）。"ST2110 系统必须把 GENLOCK MODE 设为 NETWORK"是两卡交界点。
- **ccu-web-menu**：本卡管协议配置项；彼卡管 N03 Web 界面与服务发现。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：①是否装 HKCU-SFP50（无则 N06-N12 全不显示）；②是否用 LSM（决定 IP Live `PORT` 与 NMOS 的互斥取舍）；③LSM 主备 IP（`PRIMARY` / `SECONDARY`）；④是否需要 NMOS 及 RDS 地址/端口；⑤第三方协议需求（Ember+ / SNMP / TSL）及对应软件选件（HZCU-CNFG50 / HZCU-SNMP50）；⑥多播地址规划（`AUTO` 由 LSM 给 / `MANUAL` 手填）。缺任一 → 先询问。

1. **前置**：确认 HKCU-SFP50 已装（否则本节菜单不出现）；确认 LAN1/LAN2 已按 `ccu-network-setup` 设好 IP 与**同速链路**。若本节菜单项缺失，先按选件清单核对（HKCU-SFP50 / HZCU-CNFG50 / HZCU-SNMP50），不要先怀疑软件故障。
2. **IP Live（N06）**：`PORT` = `DISABLE` 或 `LAN1&LAN2`；**改 `PORT` 后重启本机**；`DHCP` 固定 `OFF`（LSM 地址必须静态，不接受自动分配）；填 `PRIMARY` / `SECONDARY IP ADDRESS`（分别对应 LSM1 / LSM2，范围 `0.0.0.0 至 255.255.255.255`）；观察 `PRIMARY` / `SECONDARY CONNECTION STATUS` 至 `CONNECTED`；`MULTICAST ADDRESS` 随 PORT 锁定（`LAN1&LAN2`→`AUTO` / `DISABLE`→`MANUAL`）；`HITLESS FAILOVER` = `ON` / `OFF`（IP 流级无中断倒换，配合双 LSM / 双 LAN 使用）。**注意 `PORT`=`LAN1&LAN2` 意味着同时占用 LAN1 与 LAN2 两条链路，这要求两链路已按 `ccu-network-setup` 设成同一速度**——否则 LSM 冗余根本建立不起来。
3. **判停（互斥）**：若需启用 NMOS，**必须先把 IP Live `PORT` 设为 `DISABLE`**，否则 N07 的 `PORT` 不可选。二者不可同时启用。
4. **NMOS（N07，仅 LSM `PORT`=`DISABLE` 时）**：`PORT` = `LAN-COM`；`PORT NUMBER (IS-04 NODE)` = `3001`（可 `100 至 65535`）；`PORT NUMBER (IS-05 CONNECTION)` = `3002`（可 `100 至 65535`）；`RDS DISCOVERY` = `ON`（同子网自动发现）或 `OFF`（手动填 `RDS IP ADDRESS` 与 `RDS PORT NUMBER`，默认 `18235`）。
5. **第三方协议（N13-N16）**：
   a. Ember+：需 HZCU-CNFG50；`EMBER+` = `ENABLE`；`PORT` `LAN-COM`；`PORT NUMBER` `9000`（TCP）；读 `CONNECTION STATUS`。
   b. TSL UMD：`TSL UMD` = `ENABLE`（V5.0）；`PORT` `LAN-COM`；`PORT NUMBER` `8900`（UDP）；读 `PACKET STATUS`（`NOT RECEIVED` / `RECEIVED`）。
   c. SNMP：需 HZCU-SNMP50；`SNMP` = `ENABLE`；`PORT` `LAN-COM`；`NAME` / `CONTACT` / `LOCATION` ≤32 ASCII；`V1` / `V2C` `ENABLE`；`RO COMMUNITY`（默认 `sony`）；`ALLOW HOST` = `ANY` 或 `SPECIFIC`（`SPECIFIC` 时填 `HOST1` / `HOST2` / `HOST3 IP ADDRESS`）。
   d. SNMP TRAP：仅在 `SNMP` 启用时可选；`COMMUNITY` / `HOST1`-`HOST3`（含 `VERSION`，`V1` / `V2C`）/ `SEND TEST TRAP`（EXEC）。
   e. **判停**：`SNMP` = `DISABLE` 时 `SNMP TRAP` 固定 `DISABLE`，无法单独开启。
6. **多播地址（N08-N12，`MANUAL` 时）**：逐页填 `VIDEO OUT` / `RETURN` / `AUDIO OUT` / `HD TRUNK AUDIO OUT` / `PGM IN` / `INTERCOM OUT` / `INTERCOM IN` / `META OUT` 的 `IP ADDRESS`（`224.0.0.1 至 239.255.255.255`）与 `PORT`（`100 至 65535`）。

**判停分支**：改 `PORT` 后未生效 → 回步骤 2 重启本机；NMOS `PORT` 灰显不可选 → 回步骤 3 先关 LSM；协议连通但流不通 → 转 `ccu-network-setup` 查链路/PING，转 `ccu-genlock-sync` 查 PTP；无 RDS 现场空等 → 禁用 RDS 改手动设址。

**输出契约**：报告 = IP Live `PORT` + 主备 LSM IP + 连接状态 + NMOS `PORT` / 端口号 + RDS 地址端口 + 各第三方协议开关与端口/社区/主机 + 多播地址模式与（`MANUAL` 时）地址表。所有数值/端口号**原样保留**。

## B — 边界

- **不要用本卡**：端口 IP 编址 / 链路速度 / CNS / PING（→ `ccu-network-setup`）；PTP 同步（→ `ccu-genlock-sync`）；Web 界面（→ `ccu-web-menu`）。
- **手册警告的失败模式**：①**改 IP Live `PORT` 后不重启 → 配置不生效**（ce16，第 81 页）；②已启用 LSM 时强开 NMOS → 不可选（**IP Live 与 NMOS 互斥**，第 82 页）；③SNMP 未启用却开 SNMP TRAP → 固定 `DISABLE`（第 85 页）；④RDS 在同子网不可用时空等自动发现 → 应禁用 RDS 并手动设 IP（ce30，第 82 页）；⑤接入无安全保护的网络 → 未授权第三方可能访问本装置（ce32，第 94 页）。
- **型号差异**：N06-N12 全部**仅在安装 HKCU-SFP50 时显示**（第 81-84 页）；`MULTICAST ADDRESS 1` / `2-1` 中的 `VIDEO OUT LAN1-1` 与 `RETURN LAN1-1` 项"**仅当启用了 HZCU-UHD35 选件时才会在 HDCU3500 上显示**"（第 82-83 页）。Ember+ 需 HZCU-CNFG50、SNMP 需 HZCU-SNMP50（均为软件升级选件）。三个型号（HDCU5000 / 5500 / 3500）在本卡协议配置上**规则一致**，差异只体现在"是否装了上述选件"与"菜单项是否因此显示"，而非协议行为本身不同。
- **作者盲点（阶段 0 批判）**：①手册多处写"请联系 Sony 维修代表或销售代表"，SFP+ / SFP28 模块兼容清单（如 OTM-10GSR1）不在本手册；②`HITLESS FAILOVER` 只给 `ON` / `OFF`，未给触发条件与倒换时延；③SNMP 仅 V1/V2C（**无 V3**），`RO COMMUNITY` 默认 `sony` 为明文社区名，安全性依赖网络隔离（与 ce32 一致）；④多播地址 `MANUAL` 模式需自行规划，手册未给规划方法；⑤N08-N12 共 5 页、每页多组流，逐项设置繁琐，手册未给批量导入手段。

## 补充: 连接状态语义与常见"协议开着却不通"的定位顺序

三个 `CONNECTION STATUS` 字段（N06 的 `PRIMARY` / `SECONDARY`、N07 的 `RDS`、N13 的 `CONNECTION STATUS`）取值体系一致，都是 `DISCONNECTED`（已断开连接）/ `CONNECTING`（正在建立通信）/ `CONNECTED`（已建立通信）。这条三态语义是判读协议是否真正生效的核心: **`CONNECTING` 长期停留等于没通**，不能当成"正在工作"。定位顺序建议由下至上: ①先看物理与编址（转 `ccu-network-setup`: LAN1/LAN2 是否同速、IP 是否可达、PING 是否丢包）；②再看同步（转 `ccu-genlock-sync`: ST2110 系统 `GENLOCK MODE` 是否 `NETWORK`、PTP 是否 `LOCKED`）；③再看协议开关与端口（本卡: 选件是否装、`PORT` 是否正确、端口号是否与对端一致）；④最后看流级（状态画面 `Multi Format IP` 06/11 与 `IP Stream` 10/11 是否显示预期流，`-----` 表示无流）。这一顺序能避免把"地基问题"误判为"协议配置问题"而反复改协议参数。

**端口号与地址速记（原样保留）**: Ember+ = TCP `9000`；TSL UMD = UDP `8900`；NMOS IS-04 Node API = `3001`（范围 `100 至 65535`）；NMOS IS-05 Connection API = `3002`（范围 `100 至 65535`）；RDS = `18235`（范围 `100 至 65535`）；多播地址范围 `224.0.0.1 至 239.255.255.255`；流端口范围 `100 至 65535`。所有协议走 `LAN-COM`（1G 管理口），IP 流与 PTP 走 `LAN1` / `LAN2`（SFP+ / SFP28）——**两类流量分属不同物理口，排查时不可混为一谈**。
