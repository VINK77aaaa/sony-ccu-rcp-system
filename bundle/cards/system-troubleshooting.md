> 吸收单元: [RCP] led-diagnostics, mcs-operations, network-setup, maintenance-correction（RCP 卡）; [CCU] f23, f24, f25, f30, f32, f35, p61, p65, p68, p69, p72, p76, ce13, ce14, ce28, ce34, ce35, ce36, g08, g29, g30, g31, g32, g35, g36, g65, g73, g74, g75, g76, g93（CCU verified id）

# 整系统联合排障（RCP 灯语 + CCU 灯语 + 状态画面 + 错误消息） (RCP-3500/3501 + HDCU5000/5500/3500)

## R — 原文

**RCP 手册（遥控面板侧）**

- NETWORK："亮起=与控制设备相连；闪烁=无法找到控制设备；熄灭=无法与摄像机网络相连。或者,模式为 LEGACY。"（RCP 第 15 页 c）
- ALARM："亮起 (红色)=本机控制的设备发生错误；亮起 (绿色)=本机正在启动；闪烁 (黄色)=本机发生错误/连接了不支持的 USB 设备/时间设置不正确；熄灭=本机运行正常。"（RCP 第 15 页 d）
- CABLE："亮起 (绿色)=接收状态良好；亮起 (黄色)=接收电平较低；亮起 (红色)=接收电平极低；熄灭=摄像机电源关闭。或者,发生通信故障。"（RCP 第 15 页 e）
- "当此按钮和 PARA 按钮的指示灯未亮起时,无法通过此控制面板控制摄像机。"（RCP 第 15 页 a PANEL ACTIVE）

**CCU 手册（摄像机控制单元侧）**

- "CABLE ALARM…OPEN:当未通过光纤电缆将摄像机连接到本机…CAMERA FIBER 接口时点亮…不会对摄像机供电。SHORT:当过电流流经光纤电缆时…不会对摄像机供电。"（CCU 第 10 页 f）
- "NETWORK:…低速闪烁:未检测到 PTP 主站；高速闪烁:正在锁定到 PTP 主站；点亮:已锁定到 PTP 主站；不点亮:禁用网络同步锁定设置。"（CCU 第 10 页 h）
- "ALARM:当发生各种错误时点亮。"；"FAN STOP:当风扇停止时点亮。"（CCU 第 10 页 h）
- "当本机或摄像机检测到错误时, ALARM 指示灯点亮,且本机上显示出错信息。"（CCU 第 88 页 错误消息）

## I — 自述

**两端各有一套观测面。** 面板侧看 5 个灯 + LCD；主机侧看前面板 7 组灯 + 状态画面 11 页 + 错误消息表。联合排障的本质是"在正确的观测面上读到正确的项，再判断故障落在链路哪一段"：面板↔CCU 是控制链，CCU↔摄像机是信号链，两端灯各管一段。

**同名不同义是最大陷阱。** 两端都有 NETWORK 与 ALARM 灯，判读体系却完全不同（取值见查表 1）：

- **NETWORK**：面板侧 = 本机与控制设备的连接；主机侧 = PTP 网络同步锁定。同一个"NETWORK 闪烁"，在面板上是控制链路问题，在主机上是 PTP 同步问题，排查方向完全相反。
- **ALARM**：面板侧 = 本机与受控设备的状态（红/绿/黄闪四态）；主机侧 = 发生各种错误时点亮（只有亮/灭），明细读状态画面 Alarm 页。

**主机侧观测面分三层。** ①前面板灯（见查表 1）；②状态画面 11 页（System Status / Multi Format1-4 / Multi Format IP / Audio / Intercom / Network / IP Stream / Alarm）；③错误消息表（第 88 页）。部分页只在装 HKCU-SDI50/SFP50 时显示——"看不到某一页"可能是选件缺失，不是故障。

**诚实边界。** 手册对多数错误消息**只给现象/含义，不给处置步骤**；两端都是。本卡只能给"下一步查哪里"与"转哪张卡"，绝不编造处置流程。

## A1 — 书中示例与合成演练

**书中画面示例**（CCU 第 18 页，c13）：状态画面 Alarm 页（11/11）显示 "CCU:PS FAN STOP" 与 "CCU:GENLOCK ERROR"——主机侧告警面读数样板。

**书中画面示例**（CCU 第 16/17 页，c07/c11）：System Status 页（01/11）示例含 "Cable Type :Fiber Camera Cable、Cable Length : 100m、Reference :Not Detected / Unlock、CCU No.:96"；Network 页（09/11）示例含 "PTP 1:Locked、Ref :1080/50I Locked"。

**原书未提供"现象→处置"完整案例**（两端灯语表均只给"状态→含义"）。以下为**合成演练（非原书内容）**：输入 = 面板 CABLE 红亮 + CAM PW 熄灭 + 主机 CABLE CONDITION 左侧红灯亮；判读 = 面板 CABLE 红=接收电平极低、CAM PW 灭=已断电，主机 CABLE CONDITION 红=接收状态最低 → 故障在摄像机↔CCU 光纤链路（两端一致）→ 查光纤端面/接头/线长，看 CABLE ALARM 是否 OPEN/SHORT → 转 system-integration / led-diagnostics。原书未交代处置结果（未说明）。

## A2 — 未来触发

**情境**：

1. "面板上灯在闪/亮红，是面板坏了还是 CCU 坏了。"
2. "画面没信号 / 摄像机没电。"
3. "两端看着都正常，但系统就是不同步。"
4. "面板拧不动"（控制权 vs 链路）。
5. "主机前面板 ALARM 亮了 / 状态画面 Alarm 页有消息。"

**语言信号**：中文——"灯语 / 两端 / 面板灯 / CCU 灯 / NETWORK / ALARM / CABLE / CABLE ALARM / CABLE CONDITION / FAN STOP / SIGNAL BAR / 状态画面 / 错误消息 / 没信号 / 不同步 / 拧不动"；英文——"indicator / LED / both ends / status screen / error message"。

**相邻区分**：

- **led-diagnostics（RCP 卡）**：只面板一侧 5 灯的判读归彼卡；**两端灯语对照、主机侧灯与状态画面、错误消息 → 才走本卡**。
- **ccu-panel-diagnostics / ccu-status-screen（CCU 卡）**：主机前面板灯或状态画面逐页判读归彼卡；本卡与面板侧对照。
- **ccu-network-setup / ccu-*（CCU 卡）与 network-setup（RCP 卡）**：单侧配置归各卡；本卡只做联合定位，不改配置。
- **mcs-operations / maintenance-correction（RCP 卡）**：抢控制权归前者、白点/RPN/Shading 校正归后者；本卡只判"该往哪转"。
- **system-integration**：本卡判出链路/配置一致性问题后，改配置与重启动作走彼卡。

## E — 执行步骤

**查表 1：两端灯语对照**（原样成对；逐字原文见 R 段）

| 同名/同功能 | 面板侧（RCP） | 主机侧（CCU） |
|---|---|---|
| NETWORK | 亮=与控制设备相连；闪=找不到控制设备；灭=不通或 LEGACY | 低速闪=未检测到 PTP 主站；高速闪=正在锁定；亮=已锁定；不亮=禁用 |
| ALARM | 红=受控设备错误；绿=本机启动；黄闪=本机错误/USB/时间；灭=正常 | 亮=发生各种错误（明细读状态画面） |
| 链路/供电 | CABLE：绿/黄/红=接收电平三级；灭=电源关或通信故障；CAM PW：亮=供电中、灭=已断电 | CABLE ALARM：OPEN=未接光纤、SHORT=过电流（两态均不供电）；CABLE CONDITION：右绿→左红=接收电平四级；POWER：CAM=供电中、MAIN 闪=风扇错误 |

各端独有项：面板侧 SELECT（黄亮=已启用菜单页面增加，非故障灯）；主机侧 FAN STOP（亮=风扇停止）、SIGNAL BAR（输出源指示）。

**同名不同义警示**：两端 NETWORK 与 ALARM 判读体系不同（见 I 段），判读前先确认灯在哪个设备上。

**查表 2：主机侧错误消息表**（CCU 第 88 页，原样收录）

- 板级：CCU:XXX POWER ERROR / PLD ERROR / TEMP WARNING（XXX 为板名称）。
- 光路：CCU:OPTICAL CONDITION OK/WARNING/CARE/ERROR（光传感器电平下降）；CCU:PS CABLE SHORT（光纤短路）、CCU:PS CABLE OPEN（光纤断路）。
- 电源/风扇：CCU:PS FAN STOP、CCU:FRONT FAN1 STOP、CCU:PS REAR FAN STOP、CCU:PS TEMP WARNING、CCU:PS POWER ERROR、CCU:PS POWER WARNING、CCU:PS RCP POWER SUPPLY ERROR（面板电源错误）。
- 同步：CCU:GENLOCK ERROR（外部参考同步错误）、CCU:10FIELD-ID ERROR（10F BB 为 On 未检测到 10 场 ID）。
- 网络/模式：CCU:LINK SPEED MISMATCH（LAN1/LAN2 速度不匹配）、CCU:FORCE LEGACY（CNS MODE 被强制为 LEGACY）。
- 其他：CCU:SET DATE&TIME（无效日期）。

**步骤**：

0. **输入契约**（缺失先问，不猜）：①现象（哪一端、哪个灯、什么颜色/亮闪灭，或哪条错误消息）；②当前 CNS 模式（LEGACY 下面板 NETWORK 熄灭属正常）；③单机还是 MCS（影响控制权判读）；④两端是否刚改过配置/重启过。

1. **定位观测面**：确定现象在哪一端——面板侧现象用面板侧表；主机侧现象（前面板灯/状态画面/错误消息）用主机侧表与错误消息表；两端都报异常 → 先用主机侧定位链路层，再用面板侧交叉验证。

2. **三类典型现象分诊（决策树）**：
   - **"面板拧不动 / 只能看数不能调"**：看面板 PANEL ACTIVE 与 PARA 双灯——双灯全灭=无控制权（权限态，非故障）；MCS 主设备断开 → 长按 PANEL ACTIVE 强制激活 → 转 mcs-operations。面板 NETWORK 闪/灭 → 才怀疑控制链路 → 转 network-setup / system-integration。
   - **"画面没信号 / 摄像机没电"**：看主机 CABLE ALARM/CONDITION + 面板 CABLE/CAM PW。CABLE ALARM=OPEN/SHORT → 光纤链路问题且不供电；CABLE CONDITION 黄/红 → 接收电平降级；面板 CAM PW 灭 → 摄像机已断电 → 查光纤端面/接头/线长（转 system-integration / led-diagnostics）。
   - **"两端都正常但不同步"**：看主机 NETWORK 灯（PTP）与状态画面 Network 页（09/11）的 PTP/Ref/LSM；非 IP 系统看 System Status 页 Reference 行与 CCU:GENLOCK ERROR / CCU:10FIELD-ID ERROR。ST2110 系统 GENLOCK MODE 必须为 NETWORK → 转 ccu-* 同步配置卡。

3. **主机侧告警分流**：ALARM 点亮 → 读状态画面 Alarm 页（11/11）与错误消息表，按前缀分流：板级→板卡；电源/风扇/电缆→电源风扇层；同步→同步层；网络（LINK SPEED MISMATCH、FORCE LEGACY）→网络层；日期→日志层。**判停**：分流到此为止——各层处置不在本卡，转对应卡。

4. **判停与转介**：错误消息表只给"含义"、不给处置 → 输出"已定位到哪一层 + 下一步查哪一项 + 转哪张卡"，不编造处置；灯态组合无对应 → 如实说明原书边界。

**输出契约**：结论="现象 → 所属端与观测面 → 含义 → 故障层级 → 下一步查哪里/转哪张卡"；每条判读标来源书与页码；凡"原书未给处置"的必须明示。

## B — 边界

- **不要用本卡**：单面板侧灯语判读（led-diagnostics）；单主机侧灯语与状态画面判读（ccu-panel-diagnostics / ccu-status-screen）；改配置（network-setup / ccu-network-setup / system-integration）；抢控制权（mcs-operations）；校正维护（maintenance-correction）。**单设备侧判读走各自卡；跨两端联合排障才走本卡。**
- **手册警告的失败模式**：把 LEGACY 下面板 NETWORK 熄灭当故障；把面板权限态（PANEL ACTIVE/PARA 双灯全灭）当设备故障；**把两端同名 NETWORK/ALARM 灯混为一谈**（本卡 I 段核心陷阱）；CABLE ALARM 点亮时仍以为摄像机该有电（OPEN/SHORT 两态均不供电）；把 CCU:FORCE LEGACY 当故障（它是"CNS MODE 被强制为 LEGACY"状态）；把状态画面未连接项 "-" 或"看不到 UHD-SDI/IP 页"当故障（多为未连接/选件缺失）。
- **型号差异**：面板侧 5 灯两型号通用。主机侧差异大：FAN STOP / POWER MAIN 闪烁的风扇项随型号（HDCU5000：FRONT/REAR FAN1/2/4；HDCU5500/3500：PS FAN、REAR FAN）；状态画面 UHD-SDI 页仅装 HKCU-SDI50、IP 页仅装 HKCU-SFP50 时显示。
- **作者盲点（阶段 0 批判）**：①两端手册都只给"状态→含义"，**不给"现象→原因→处置"完整决策树**——本卡决策树由两端定义拼合，处置一律标注来源或转介；②两端观测面**互不覆盖**：面板侧看不到主机侧状态画面/错误消息，主机侧看不到面板侧权限态，联合排障必须两侧同时观察；③RCP 手册无 CCU:XXX 错误消息表，CCU 手册无面板 PANEL ACTIVE/PARA 权限态——结构性缺口；④CCU:PS RCP POWER SUPPLY ERROR 指向 RCP 供电，但"RCP 从 CCU 取电还是自供电"两端手册未对齐（见 system-integration B 段）。
