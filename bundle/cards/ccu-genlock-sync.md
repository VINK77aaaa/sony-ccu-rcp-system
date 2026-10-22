> 吸收单元: f12, f13

# 同步配置（GENLOCK HD/SD/NETWORK + PTP ST2059-2） (HDCU5000/5500/3500)

## R — 原文

- GENLOCK MODE: "HD、 SD、 NETWORK 设置外部参考信号的锁定模式。仅在安装了 HKCU-SFP50 网络接口板时才会显示 NETWORK。如果在 SMPTE ST 2110 兼容系统中运行, 则设置为 NETWORK。设为 NETWORK 时, 不需要REFERENCE IN 接口的外部参考输入,且使用 HKCU-SFP50 的 LAN 1 和 LAN 2 接口进行网络同步操作。" (第 32 页)
- 10F BB: "设置是否使用添加到外部参考信号的 10 场 ID。当 GENLOCK MODE 为 SD 且 <MULTI FORMAT> 页面 t SYSTEM 为 1.001(525) 时,可以选择此项。" (第 32 页)
- H-PHASE STEP: "当在 GENLOCK MODE 中选择 HD 时: –3.01 至 3.45 微秒 0.00；当在 GENLOCK MODE 中选择 SD 时: –8.29 至 9.48 微秒 0.00" (第 32 页)
- LOCK STATUS（GENLOCK 选 HD/SD 时）: "LOCKED、 NOT LOCKED 外部参考信号的锁定状态 (仅显示) 。" (第 32 页)
- NETWORK GENLOCK: "PROFILE ST2059-2 显示支持的配置文件。仅支持 ST2059-2 配置文件。"；"DOMAIN NUMBER 0 至 127、 127 设置域地址。设为要连接的主站设备的域编号。"；"DELAY REQUEST INTERVAL –7 至 –1、 –3 显示 PTP 主站的响应延迟。" (第 80 页)
- LOCK STATUS（N04）: "NOT IN USE、 NO MASTER、 LOCKING、 LOCKED"（NOT IN USE:PTP 操作停止；NO MASTER:找不到 PTP 主站；LOCKING:正在同步；LOCKED:已同步）(第 80 页)
- 前面板 NETWORK 灯: "低速闪烁:未检测到 PTP 主站；高速闪烁:正在锁定到 PTP 主站；点亮:已锁定到 PTP 主站；不点亮:禁用网络同步锁定设置" (第 10 页)

## I — 自述

本卡只解决一件事: 本机的**时间基准从哪来、相位怎么对齐**。手册把同步来源做成 `GENLOCK MODE` 的三选一 —— `HD`、`SD`、`NETWORK`，这三者互斥，选错就是"锁不上"或"整系统不同步"。它与端口 IP 编址（N01）、ST2110 流与第三方协议（N06-N16）、Web 界面（N03）是四件不同的事，本卡不碰后三者。

**前置条件链**决定了你能选哪一项，顺序不能颠倒。第一层是选件: `NETWORK` 这一项**仅在安装了 HKCU-SFP50 网络接口板时才会显示**（第 32 页），没有 SFP50 的机器菜单里根本看不到 NETWORK，只剩 HD/SD 两项。第二层是系统形态: **在 SMPTE ST 2110 兼容系统中运行时必须设为 NETWORK**（第 32 页）——这不是"可选优化"，而是全 IP 系统能否上锁的前提。第三层是外部参考信号类型: 接 HD 三电平就选 `HD`，接 SD 黑场就选 `SD`；`REFERENCE` 菜单项本身只是"REFERENCE IN 接口的信号输入（仅显示）"，取值 `NOT DETECTED`、`EXT IN`、`1080/59.94I`、`1080/23.98PsF`、`720/59.94P`、`1080/50I`、`1080/24PsF`、`720/50P`，它是**检测结果，不是你可以设的参考源类型**（第 32 页）。第四层是 SYSTEM 频率体系（`1.001(525)` / `1.000(625)`），它决定 `10F BB` 等项是否可选。

**HD/SD 路径**的完整参数集是: `GENLOCK MODE`、`10F BB`、`H-PHASE STEP`、`H-PHASE COARSE`、`V-PHASE`、`SYNC OUT SELECT`，观测项是 `LOCK STATUS`（`LOCKED` / `NOT LOCKED`）。其中有两个容易踩的坑: ①`10F BB`（是否使用添加到外部参考信号的 10 场 ID）**只有 GENLOCK MODE 为 SD 且 SYSTEM 为 1.001(525) 时才可选**（第 32 页）；②`H-PHASE STEP` 的范围**随 GENLOCK MODE 变化** —— HD 时 `–3.01 至 3.45 微秒`、SD 时 `–8.29 至 9.48 微秒`（默认均为 `0.00`）。相位调整有三层: `H-PHASE STEP`（手册称"步长"）、`H-PHASE COARSE`（`–99 至 99`，手册称"精细调整"）、`V-PHASE`（`0 至 7`，垂直锁定相位，单位行）。注意手册的命名与直觉相反（STEP 是粗档、COARSE 是精调），见 g33。

**NETWORK 路径（PTP）**在 `NETWORK` 菜单的 `<NETWORK GENLOCK>`（N04）与 `<PTP STATUS>`（N05）两页，**二者仅在安装 HKCU-SFP50 时显示**（第 80-81 页）。配置项是: `PORT`（`LAN1` / `LAN2`）、`NETWORK GENLOCK`（`DISABLE` / `ENABLE`）、`PROFILE`（**仅支持 ST2059-2 配置文件**）、`DOMAIN NUMBER`（`0 至 127`，默认 `127`，**设为要连接的主站设备的域编号**）、`COMMUNICATION MODE`（`MULTICAST MODE` 组播回复主站 / `MIXED MODE` 单播回复主站）、`DELAY REQUEST INTERVAL`（`–7 至 –1`，默认 `–3`）。N05 是监视页，额外给出 `PTP NIC`、`UTC Time`、`MasterID`、`GMClockID`（祖父时钟 ID）、`Sync` / `FollowUp` / `DelayReq` / `DelayResp` 报文速率、`Network Status`（`UNAVAILABLE` / `NOT GOOD` / `GOOD` / `VERY GOOD`）、`Delay`、`Jitter`。

**PTP 的锁定判读有两套同名但不同取值的东西**（g32，不可混用）: `GENLOCK MODE` 选 HD/SD 时，`LOCK STATUS` 只有 `LOCKED` / `NOT LOCKED`；而 N04 的 PTP `LOCK STATUS` 是四态 `NOT IN USE`（PTP 操作停止）/ `NO MASTER`（找不到 PTP 主站）/ `LOCKING`（正在同步）/ `LOCKED`（已同步）。前面板 `NETWORK` 灯用四态编码同一件事: 低速闪烁=未检测到 PTP 主站、高速闪烁=正在锁定、点亮=已锁定、不点亮=禁用网络同步锁定设置（第 10 页）。

**外部参考接口本身的规格也构成前置条件**（g30）。`REFERENCE IN` 接口接收 HD 三电平同步或 SD 参考信号（黑场/带 10 场 ID 的黑场）；`REFERENCE OUT` **原样输出输入信号（环路）**，不使用环路输出时须在 `75 欧姆` 端接——端接缺失会破坏参考信号质量，是"锁不上"的常见物理原因。HD 参考的电气规格为 SMPTE ST274、3 电平同步、`0.6 Vp-p`、`75 欧姆`。`SYNC OUT SELECT`（`SD SYNC` / `HD SYNC`）决定 REFERENCE OUT 口的输出类型，因此本机可作参考源向下游输出——这意味着同步链可能是**级联**的: 上游 CCU 的 SYNC OUT 成为下游 CCU 的 REFERENCE IN，此时两台的 `SYNC OUT SELECT` 与 `GENLOCK MODE` 必须匹配。

**观测面有三处，判读顺序建议由粗到细**。①前面板指示灯: `REF IN`（绿色，表示有 REFERENCE 输入信号）、`UNLOCK`（红色，未锁定到 REFERENCE 输入信号）、`NETWORK`（四态 PTP 灯语，见 R 段第 10 页引文）——这是最快的第一入口；②状态画面 `Network` 页（09/11，第 17 页，仅装 HKCU-SFP50 时显示）可读 `Ref`（使用的参考格式设置和同步锁定状态，如 `1080/50I` / `Locked`）与 `PTP 1` / `PTP 2` 的锁定状态；③菜单层 N04 `LOCK STATUS` 与 N05 `PTP STATUS` 给出最细的报文速率、主站 ID、祖父时钟 ID、网络状态、延迟与抖动。三处必须口径一致，若前面板 `NETWORK` 灯点亮而状态画面 `PTP` 仍为 `Locking`，以菜单页 N05 的 `STATUS` 为准。

**关键边界**: 设为 `NETWORK` 时**不需要 REFERENCE IN 接口的外部参考输入**，同步改由 HKCU-SFP50 的 LAN 1 和 LAN 2 接口承载（第 32 页）。这带来一个直接推论: PTP 依赖 LAN1/LAN2 链路，而 LAN1 与 LAN2 的链路速度**必须相同**（第 79 页），否则"无法进行正常操作"——同步问题因此可能实际是链路速度问题，需回 `ccu-network-setup` 核对。

## A1 — 书中配置示例

手册**没有**给出带具体数值的 GENLOCK 配置演算，但它给出了两处可直接引用的真实画面与状态示例:

1. **状态画面 Network 页（09/11，第 17 页，c11）** —— 真实画面示例，可读出同步已锁: `Ref :1080/50I`、下一行 `Locked`；同时 `PTP 1:Locked 2:Locked`。这是"外部参考 + PTP 均已锁定"的现场读法样板（该页仅在装 HKCU-SFP50 时显示）。
2. **状态画面 Alarm 页（11/11，第 18 页，c13）** —— 真实画面示例，逐字列出 `CCU:GENLOCK ERROR` 与 `CCU:PS FAN STOP` 两条告警，对应第 88 页错误消息表（`CCU:GENLOCK ERROR` = "外部参考同步错误"）。

以下为合成演练（非原书内容）—— 手册未提供完整配置演算，故补一段端到端走查供参照:

- **输入**: 外部 HD 三电平参考已接 REFERENCE IN（`SYSTEM` = `1.001(525)`），不接 PTP，需要微调水平相位。
- **输出**: `GENLOCK MODE` = `HD`；`H-PHASE STEP` 取 `–3.01 至 3.45 微秒` 区间内某值（默认 `0.00`）；`10F BB` **不可选**（本例非 SD 模式，不满足"GENLOCK MODE=SD 且 SYSTEM=1.001(525)"）；`SYNC OUT SELECT` 按下游需要取 `SD SYNC` 或 `HD SYNC`；观察 `LOCK STATUS` 直到 `LOCKED`，前面板 `UNLOCK` 灯应灭、`REF IN` 灯亮。

## A2 — 未来触发

**情境**：

1. 全 IP / ST2110 演播室上电后画面不同步、PTP 锁不上，需要确认同步模式与 PTP 参数。
2. 多机位系统要做相位对齐（行/微秒级），或外部参考切换后出现 `UNLOCK`。
3. 接了外部 REF（HD 三电平或 SD 黑场）后本机锁不上，怀疑参考源类型选错。
4. 出现 `CCU:GENLOCK ERROR` 或 `CCU:10FIELD-ID ERROR`，要定位是参考信号、10F BB 还是模式问题。
5. 需要在 SD 模式下启用 10 场 ID（`10F BB`）。

**语言信号**：中文——"同步 / 锁相 / GENLOCK / REF / 黑场 / 三电平 / PTP / 相位 / 行相位 / UNLOCK / 锁不上 / 同步不上 / 域编号"；英文——"genlock / reference / tri-level sync / black burst / PTP / ST2059-2 / phase / locked / unlock / domain number"。

**相邻区分**：

- **ccu-network-setup**：本卡管同步来源与相位（`GENLOCK MODE`、PTP 域编号/通信模式/延迟请求间隔）；彼卡管端口 IP 编址、CNS、链路速度、PING。PTP 走哪条 LAN 端口由本卡 N04 `PORT` 选，但该端口的 IP 与链路速度在彼卡 N01 设——同步锁不上时先查彼卡的 LAN1/LAN2 是否同速。
- **ccu-ip-live**：本卡管 PTP 同步（N04/N05）；彼卡管 ST2110 流与第三方协议（N06-N16）。"ST2110 系统必须把 GENLOCK MODE 设为 NETWORK"是两卡的交界点。
- **ccu-web-menu**：远程修改同步参数时，界面操作归彼卡，参数取值归本卡。
- **指示灯与诊断卡**：`NETWORK` 灯、`UNLOCK` 灯、状态画面 `Ref`/`PTP` 行、`CCU:GENLOCK ERROR` 的**判读**归彼卡；本卡负责把同步**配对上锁**。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：①系统是否 ST2110 / 全 IP（决定是否**必须**用 NETWORK）；②是否已装 HKCU-SFP50（决定 `NETWORK` 是否可选、N04/N05 是否显示）；③外部参考信号类型（HD 三电平 / SD 黑场 / 带 10 场 ID 的黑场 / 无）；④`SYSTEM` 取值（`1.001(525)` / `1.000(625)`）；⑤是否需相位微调及目标（微秒/行）；⑥PTP 场景下主站的域编号、通信模式、延迟请求间隔。任一不明 → 先询问。

1. **判定同步来源（三选一，先做互斥归类）**：
   - 系统为 ST2110 / IP Live → **必须** `NETWORK`，跳至步骤 3；
   - 有外部 HD 三电平参考 → `HD`，跳至步骤 2；
   - 有外部 SD 黑场参考 → `SD`，跳至步骤 2；
   - 无外部参考 → 本机内部同步（本卡不覆盖"自由运行"的显式菜单项，手册未单列）。
   **判停**：若需要 NETWORK 但未装 HKCU-SFP50 → 停止，先装选件（菜单项不存在，无法继续）。
2. **HD/SD 路径**（`SYSTEM CONFIG` → `<GENLOCK>` S04）：
   a. 接 REFERENCE IN（HD 三电平 `0.6 Vp-p`、`75 欧姆`；SD 黑场/带 10 场 ID 黑场）；不使用的 REFERENCE OUT 环路输出须 `75 欧姆` 端接。
   b. `GENLOCK MODE` = `HD` 或 `SD`。
   c. `10F BB`：仅当 `GENLOCK MODE` = `SD` 且 `SYSTEM` = `1.001(525)` 时可 `ON`；否则该项不可选。
   d. 相位: `H-PHASE STEP`（HD `–3.01 至 3.45 微秒` / SD `–8.29 至 9.48 微秒`）、`H-PHASE COARSE`（`–99 至 99`）、`V-PHASE`（`0 至 7`）。
   e. `SYNC OUT SELECT` = `SD SYNC` 或 `HD SYNC`（决定 REFERENCE OUT 输出信号）。
   f. **判停**：观察 `LOCK STATUS` 直到 `LOCKED`；前面板 `REF IN` 灯亮、`UNLOCK` 灯灭。停在 `NOT LOCKED` → 查参考信号类型/接线/端接，勿改相位掩盖。
3. **NETWORK 路径（PTP，`NETWORK` 菜单）**：
   a. 打开 `<NETWORK GENLOCK>`（N04，仅装 HKCU-SFP50 显示）。
   b. `PORT` = `LAN1` 或 `LAN2`；`NETWORK GENLOCK` = `ENABLE`。
   c. `PROFILE` 固定 `ST2059-2`（唯一支持，不可改）。
   d. `DOMAIN NUMBER` = 主站域编号（`0 至 127`，默认 `127`）；`COMMUNICATION MODE` = `MULTICAST MODE` 或 `MIXED MODE`（`MIXED MODE` 单播回复主站）；`DELAY REQUEST INTERVAL`（`–7 至 –1`，默认 `–3`）。
   e. **判停**：在 N04 `LOCK STATUS` 或 N05 `PTP STATUS` 观察状态迁移 `NOT IN USE` → `NO MASTER` → `LOCKING` → `LOCKED`。若长时间停在 `NO MASTER` → 域编号不一致 / 网络不通 / 主站未起，转 `ccu-network-setup` 用 PING（N17）查链路，并核对 LAN1/LAN2 链路速度是否相同。
   f. 用 N05 辅助确认: `PTP NIC`、`MasterID`、`GMClockID`、`Network Status`（期望 `GOOD` / `VERY GOOD`）、`Delay`、`Jitter`。

**判停分支**：PTP 上锁后若画面仍不同步 → 检查 ST2110 系统其他设备是否同一 PTP 域/主站；`GENLOCK ERROR` 持续 → 回查参考源与模式匹配；LAN1/LAN2 速度不一致引发的异常 → 转 `ccu-network-setup`。

**输出契约**：报告 = 选定 `GENLOCK MODE` + 参考源类型（或 PTP 主站）+ 关键参数（`DOMAIN NUMBER` / `COMMUNICATION MODE` / `DELAY REQUEST INTERVAL` / 相位值，**原样保留**）+ `LOCK STATUS` 终值 + 观察到的前面板灯态。

## B — 边界

- **不要用本卡**：端口 IP/子网/网关、CNS 编号、链路速度、PING（→ `ccu-network-setup`）；ST2110 流与 NMOS / Ember+ / SNMP / TSL UMD（→ `ccu-ip-live`）；Web 界面操作（→ `ccu-web-menu`）；灯语与错误消息全表判读（→ 指示灯与诊断卡）。
- **手册警告的失败模式**：①`10F BB` 设为 `On` 却未检测到 10 场 ID → `CCU:10FIELD-ID ERROR`（ce35，第 88 页；条件见第 32 页）；②外部参考同步失败 → `CCU:GENLOCK ERROR`（第 88 页）；③**LAN1/LAN2 链路速度不一致 → "无法进行正常操作"，并可能报 `CCU:LINK SPEED MISMATCH`**（ce14，第 79/88 页）——PTP 走 LAN1/LAN2，此约束直接作用于本卡；④ST2110 系统未设 `NETWORK` → 同步不上锁（第 32 页）。
- **型号差异**：`NETWORK` 选项与 `<NETWORK GENLOCK>` N04、`<PTP STATUS>` N05 页**仅在安装了 HKCU-SFP50 时显示**（第 32/80/81 页）；未装 SFP50 的机器只有 `HD` / `SD` 两选一，`NETWORK` 与 PTP 相关项均不存在。IP 输出还需 OTM-10GSR1 或其他 SFP+ / SFP28 模块。
- **作者盲点（阶段 0 批判）**：①手册把"步长"命名为 `STEP`、把"精细调整"命名为 `COARSE`，**命名与直觉相反**（g33），易误读；②`H-PHASE STEP` 范围随 `GENLOCK MODE` 变化，但手册未说明切换模式时旧相位值如何处理；③手册未给出"无外部参考（自由运行）"的显式菜单项说明；④`LOCK STATUS` 同名项在 GENLOCK（`LOCKED`/`NOT LOCKED`）与 PTP（四态）两处取值体系不同（g32），不可混用；⑤SFP+ 模块兼容清单不在本手册（多处写"请联系 Sony 销售或服务代表"）。
