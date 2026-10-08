> 吸收单元: f23, f30, p61

# 前面板灯语诊断（看灯识故障） (HDCU5000/5500/3500)

## R — 原文

- "CABLE ALARM 指示灯：OPEN:当未通过光纤电缆将摄像机连接到本机后面板上的 CAMERA FIBER 接口时点亮。 当此指示灯点亮时, 不会对摄像机供电。SHORT:当过电流流经光纤电缆时,此指示灯会点亮。 当此指示灯点亮时,不会对摄像机供电。" (第 10 页)
- "CABLE CONDITION (信号接收状态)指示灯：指示摄像机 (CAM) 和摄像机控制单元 (CCU) 的通信状态。当右侧两个指示灯 (绿色)点亮时:接收状态非常好。当右起第二个指示灯 (绿色)点亮时:接收状态良好。当左起第二个指示灯 (黄色)点亮时:接收状态水平低。当左侧指示灯 (红色)点亮时:接收状态处于最低水平。" (第 10 页)
- "NETWORK:显示使用 HKCU-SFP50 网络接口板时的网络同步锁定状态。低速闪烁:未检测到 PTP 主站；高速闪烁:正在锁定到 PTP 主站；点亮:已锁定到 PTP 主站；不点亮:禁用网络同步锁定设置。" (第 10 页)
- "ALARM:当发生各种错误时点亮。FAN STOP:当风扇停止时点亮。"；"REF IN (绿色):表示有 REFERENCE 输入信号。UNLOCK (红色):未锁定到 REFERENCE 输入信号。RCP/MSU:显示连接遥控面板时的状态。" (第 10 页)
- "POWER 指示灯：CAM:当正在向摄像机供电时点亮。MAIN:当本机打开时点亮。此外,如果风扇发生错误,此指示灯会闪烁。" (第 10 页)
- "SIGNAL BAR 指示灯：指示视频信号的输出状态。灰色信号输出期间:关闭；彩条输出期间:按照在 MAINTENANCE t <FRONT PANEL> t SIGNAL BAR t READY COLOR 菜单项目中指定的颜色点亮；摄像机视频输出期间:以白色流动方式点亮。" (第 10 页)
- 错误消息表：`CCU:XXX POWER ERROR`（板载电源错误，XXX 为板名称）、`CCU:XXX PLD ERROR`、`CCU:XXX TEMP WARNING`、`CCU:PS FAN STOP`（电源区块 FAN 错误）、`CCU:PS CABLE SHORT`（CAMERA 接口光纤电缆短路连接错误）、`CCU:PS CABLE OPEN`（CAMERA 接口光纤电缆断路连接错误）、`CCU:GENLOCK ERROR`（外部参考同步错误）、`CCU:FORCE LEGACY`、`CCU:10FIELD-ID ERROR`、`CCU:SET DATE&TIME`（无效日期）、`CCU:LINK SPEED MISMATCH`（LAN1 和 LAN2 的链路速度不匹配）。(第 88 页)

## I — 自述

CCU 主机前面板是排障的第一入口。判读方法同样是"先分层、再查表、后转介"：把观察到的灯态归属到某一层，再查该灯的状态→含义，最后把处置动作转给对应的能力卡。

灯的层级大致是：**供电/链路层**（CABLE ALARM 管"摄像机连没连上、有没有过流"；CABLE CONDITION 管光纤接收质量；POWER 的 CAM/MAIN 管摄像机供电与本机供电）→ **同步层**（NETWORK 管 PTP 网络同步四态；REF IN/UNLOCK 管外部参考锁定）→ **设备层**（ALARM 管各类错误；FAN STOP 管风扇；RCP/MSU 管外部控制设备连接）→ **输出层**（SIGNAL BAR 指示当前输出的是灰场/彩条/摄像机视频）。

三条必须记牢：①**CABLE ALARM 亮起（无论 OPEN 还是 SHORT）都不会对摄像机供电**——摄像机无电时先看这个灯，而不是先怀疑摄像机本身；②**NETWORK 灯只在装了 HKCU-SFP50 时才有意义**，且"不点亮"的含义是"禁用网络同步锁定设置"，不一定是故障；③**POWER 的 MAIN 灯闪烁 = 风扇错误**，是硬件级故障的早期信号，应转 DIAGNOSIS 的风扇项确认。

关于错误消息：ALARM 灯点亮时本机会显示 `CCU:` 前缀的错误消息（第 88 页）。这些消息给的是"现象/含义"（如 `CCU:PS CABLE SHORT` = 光纤电缆短路），**手册对绝大多数消息只给现象、不给处置步骤**。SIGNAL BAR 则是唯一一个"输出状态指示"性质的灯，其灯语直接对应 READY COLOR 与"白色流动"两种编码。

## A1 — 书中配置示例

以下为**书中给出的灯语对照示例**（原书第 9-10 页自带的状态→含义对照，即 c17，非作者经历案例）：

- CABLE CONDITION（第 10 页，四态）：右侧两个绿灯亮=接收状态非常好；右起第二个绿灯亮=接收状态良好；左起第二个黄灯亮=接收状态水平低；左侧红灯亮=接收状态处于最低水平。
- CABLE ALARM（第 10 页，两态）：OPEN=未通过光纤连到 CAMERA FIBER 接口；SHORT=过电流流经光纤电缆；两态均"不会对摄像机供电"。
- SIGNAL BAR（第 10 页，三态）：灰场=关闭；彩条=按 READY COLOR 指定颜色点亮；摄像机视频=白色流动点亮。

**原书未提供"现象→处置"的完整实例**（阶段 0 批判已标注：灯语表只给状态→含义，无决策树）。故以下为**合成演练（非原书内容）**：输入 = CABLE ALARM 亮起 + 摄像机无电 → 查表判读 = OPEN（未连光纤）或 SHORT（过流），两态均不供电 → 下一步转 ccu-diagnosis-menu 读 D05 `CABLE OPEN`/`CABLE SHORT` 复核，SHORT 情形手册未给处置，如实说明。

## A2 — 未来触发

**情境**：

1. 摄像机不上电/画面全黑："摄像机没电 / 是不是线的问题 / 前面板哪个灯亮着"。
2. 光纤链路质量下降："画面闪断 / 传输不稳 / CABLE CONDITION 是黄/红"。
3. IP/PTP 同步异常："NETWORK 灯一直闪 / 不同步 / 锁不上 PTP"。
4. 本机报错："ALARM 亮了 / 屏上出现 CCU:XXX 消息 / 是什么意思"。
5. 输出源判读："现在出来的是彩条还是摄像机信号 / SIGNAL BAR 在流动"。
6. 风扇/温度异常："MAIN 灯在闪 / 机器很烫"。

**语言信号**：中文——"灯语 / 指示灯 / 灯亮 / 闪烁 / CABLE ALARM / CABLE CONDITION / NETWORK / ALARM / FAN STOP / POWER 灯 / SIGNAL BAR / 彩条 / 摄像机没电 / 报错消息 / CCU: 开头"；英文——"indicator / LED / blinking / CABLE ALARM / cable condition / NETWORK light / ALARM / fan stop / signal bar / bars / error message"。

**相邻区分**：

- **RCP `led-diagnostics`（必须划清）**：彼卡是 **RCP 面板侧** 灯语（CAM PW / NETWORK / ALARM / CABLE 四张表）；本卡是 **CCU 主机侧** 灯语（CABLE ALARM / CABLE CONDITION / NETWORK / ALARM / FAN STOP / POWER / SIGNAL BAR）。同一个"NETWORK 灯"两处含义不同：RCP 侧指"与控制设备的连接"，CCU 侧指"PTP 网络同步锁定状态"。问"面板上的灯"→彼卡；问"CCU 机箱前面板的灯"→本卡。
- **ccu-status-screen**：本卡负责"看灯定位到某一层"，状态画面（尤其 Alarm 页 11/11）负责"把告警条目逐条读出"。灯亮→先本卡分层，再转彼卡读全量告警。
- **ccu-diagnosis-menu**：CABLE ALARM/CONDITION 与 MAIN 闪烁指向硬件级问题后，用 D05/D06 复核（电缆开路/短路、风扇停转）归彼卡。
- **ccu-file-log**：`CCU:SET DATE&TIME`、日志相关的告警，其处置（改日期前先导出日志）归彼卡。
- **ccu-network**（网络与 IP 配置，如有独立卡）：`CCU:LINK SPEED MISMATCH`、NETWORK 灯异常若定位为配置问题，改配置动作归彼卡。
- **RCP `specs-reference`**：光纤电缆长度/接口规格等纯数值速查归彼卡。

## E — 执行步骤

**查表**（状态→含义原样成对，禁止改写，均出自第 10 页）：

CABLE ALARM（第 10 页）：

| 状态 | 含义 |
|---|---|
| OPEN | 未通过光纤电缆将摄像机连接到 CAMERA FIBER 接口；**不对摄像机供电** |
| SHORT | 过电流流经光纤电缆；**不对摄像机供电** |

CABLE CONDITION（第 10 页）：

| 状态 | 含义 |
|---|---|
| 右侧两个绿灯亮 | 接收状态非常好 |
| 右起第二个绿灯亮 | 接收状态良好 |
| 左起第二个黄灯亮 | 接收状态水平低 |
| 左侧红灯亮 | 接收状态处于最低水平 |

NETWORK（第 10 页，仅装 HKCU-SFP50 时）：

| 状态 | 含义 |
|---|---|
| 低速闪烁 | 未检测到 PTP 主站 |
| 高速闪烁 | 正在锁定到 PTP 主站 |
| 点亮 | 已锁定到 PTP 主站 |
| 不点亮 | 禁用网络同步锁定设置 |

SIGNAL BAR（第 10 页）：

| 状态 | 含义 |
|---|---|
| 关闭 | 灰色信号输出期间 |
| 按 READY COLOR 指定颜色点亮 | 彩条输出期间 |
| 以白色流动方式点亮 | 摄像机视频输出期间 |

**步骤**：

0. **输入契约**（缺失先问，不猜）：①完整灯态观察（哪个灯 / 颜色 / 亮-闪-灭 / 快慢）；②是否装 HKCU-SFP50（决定 NETWORK 灯是否有意义）；③本机是否在报错（屏上是否出现 `CCU:` 消息）。灯态描述不全先补观察，不得臆测。
1. **分层定位**：供电/链路层（CABLE ALARM、CABLE CONDITION、POWER CAM）→ 同步层（NETWORK、REF IN/UNLOCK）→ 设备层（ALARM、FAN STOP、RCP/MSU）→ 输出层（SIGNAL BAR），逐灯查上表。
2. **处置分支**：
   - CABLE ALARM 亮 → 摄像机不供电；转 ccu-diagnosis-menu 读 D05 `CABLE OPEN`/`CABLE SHORT` 复核。**SHORT 情形手册未给处置步骤，如实告知，不编造**。
   - CABLE CONDITION 黄/红 → 光纤链路接收电平低，检查光纤端面与连接（端面污染边界见 ce13）。
   - NETWORK 闪烁（低速/高速）→ 定位为 PTP 未锁/正在锁；转 ccu-network 与 ccu-status-screen（Network 页 09/11）。
   - ALARM 亮 → 读出 `CCU:` 消息（转 ccu-status-screen Alarm 页），按消息现象定位层级；多数消息**只给现象无处置**。
   - FAN STOP 亮 / MAIN 闪烁 → 转 ccu-diagnosis-menu 读 D06 风扇项确认。
   - SIGNAL BAR 常亮彩条色 → 当前在输出彩条（READY COLOR），非故障。
3. **伪故障甄别**（报修前必过）：①NETWORK 不点亮 = 禁用网络同步锁定设置，若本就不用 PTP 属正常；②未装 SFP50 时 NETWORK 灯不参与判读；③摄像机未连接时状态画面显示 "-"，非故障（见 ccu-status-screen）。
4. **判停**：灯态组合在表中无对应，或表只给现象/含义而无处置（如 SHORT、多数 `CCU:` 消息）→ 如实说明原书边界，给出已排除项与转介建议，不编造处置。

**输出契约**：结论 = "灯态组合 → 各灯含义（标页码）→ 故障层级 → 转介能力"，逐条标页码；对无处置项明确标注"手册未给处置"。

## B — 边界

- **不要用本卡**：RCP 面板侧灯语（RCP `led-diagnostics`）、状态画面全量判读（ccu-status-screen）、硬件诊断项读取（ccu-diagnosis-menu）、日志处置（ccu-file-log）、网络配置改动（ccu-network）。
- **手册警告的失败模式**：
  - CABLE ALARM 亮起（OPEN/SHORT）→ 不对摄像机供电（ce28，第 10 页）；摄像机无电先查此灯。
  - MAIN 灯闪烁 = 风扇错误（ce36，第 10 页）——早期硬件故障信号。
  - 光纤接口不连接未盖防尘盖 → 灰尘导致传输错误，表现为 CABLE CONDITION 降级（ce13，第 12/14 页）。
  - `CCU:LINK SPEED MISMATCH` = LAN1 与 LAN2 链路速度不匹配，无法正常操作（第 79/88 页）。
- **诚实留白（重点）**：手册对**多数错误消息只给现象、不给处置步骤**；**CABLE ALARM 的 SHORT 态亦无处置**。本卡不得为此类条目编造处置流程，只能给出"读现象 → 转对应能力卡复核 → 如实说明留白"。
- **型号差异**：NETWORK 灯仅在装 HKCU-SFP50 时有意义（第 10 页），三型号均需 SFP50；CABLE ALARM/CONDITION 与 FAN STOP 与型号无强绑定；风扇具体项（PS FAN / FRONT FAN1/2/4 / REAR FAN 等）的型号显隐归 ccu-diagnosis-menu。
- **作者盲点（阶段 0 批判）**：灯语为"状态→含义"对照表，无完整"现象→原因→处置"决策树；灯态与错误消息的映射部分需交叉第 88 页表；处置动作手册普遍缺失，下游须显式保留该留白。
