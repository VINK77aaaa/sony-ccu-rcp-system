> 吸收单元: f25, p50

# DIAGNOSIS 硬件诊断 (HDCU5000/5500/3500)

## R — 原文

- "VIF：OK、POWER ERROR、PLD ERROR、TEMP WARNING（VIF 板自诊断结果）；TX：OK、POWER ERROR、PLD ERROR、TEMP WARNING（TX 板自诊断结果）；NET：OK、POWER ERROR、PLD ERROR、TEMP WARNING（HKCU-SFP50 板 (选件)自诊断结果）。POWER ON HOUR METER：99999 H 累计开机时间。HOUR METER：99999 H 累计开机时间。" (第 86 页，D01 BOARD STATUS)
- "MODEL NAME：本机型号名称；SERIAL NUMBER：序列号。" (第 86 页，D02 SERIAL NUMBER)
- "APPLICATION：本机软件版本；OS：本机软件版本；UPDATER：本机软件版本；SY：SY PLD 的 ROM 版本 (SY 板)；VIF：VIF PLD 的 ROM 版本 (VIF 板)；TX1(HIGH)/TX1(ULTRA)/TX2：TX1/TX2 PLD 的 ROM 版本 (HKCU-FB50 板选件)；NET1/NET2：NET1/NET2 PLD 的 ROM 版本 (HKCU-SFP50 板选件)。" (第 87 页，D03 VERSION)
- "NAME：已连接摄像机的型号名称；ROM VERSION：X.XX 摄像机的 ROM 版本。" (第 87 页，D04 CAMERA DIAGNOSIS)
- "CAM POWER SUPPLY：ON、OFF 显示摄像机的电源状态。CABLE OPEN：OK、OPEN 显示电缆的断路状态。CABLE SHORT：OK、SHORT 显示电缆的短路状态。RCP POWER：OK、ERROR 显示 RCP 的电源状态。" (第 87 页，D05 POWER UNIT STATUS)
- "PS FAN：OK、STOP 显示电源设备上风扇的运行状态 (仅限 HDCU5500/3500)。PS REAR FAN：OK、STOP 显示电源设备后部风扇的运行状态。FRONT FAN1/2、FRONT FAN4：显示前面板上风扇的运行状态 (仅限 HDCU5000)。REAR FAN：显示后面板上风扇的运行状态 (仅限 HDCU5500/3500)。REAR FAN1/2、REAR FAN4：显示后面板上风扇的运行状态 (仅限 HDCU5000)。" (第 87 页，D06 FAN STATUS)

## I — 自述

DIAGNOSIS 菜单是硬件级的"自检台"：当前面板 ALARM 点亮、或怀疑板卡/电源/风扇出问题时，用它把故障定位到具体硬件层级。它由六页组成（D01–D06），每页管一类硬件信息，判读方法是"按页读值 → 对照状态含义 → 定位到板卡/电源/风扇/摄像机"。

六页的职责：**D01 BOARD STATUS** 给出 VIF / TX / NET 三块板的**自诊断结果**（取值 OK / POWER ERROR / PLD ERROR / TEMP WARNING），并给出 POWER ON HOUR METER 与 HOUR METER（均为 `99999 H` 上限的累计开机时长）；**D02 SERIAL NUMBER** 读型号与序列号；**D03 VERSION** 读本机软件、OS、UPDATER 与各板 PLD 的 ROM 版本（含 HKCU-FB50 的 TX1(HIGH)/TX1(ULTRA)/TX2、HKCU-SFP50 的 NET1/NET2）；**D04 CAMERA DIAGNOSIS** 读所连摄像机的型号与 ROM 版本；**D05 POWER UNIT STATUS** 读摄像机供电、电缆开路/短路、RCP 电源状态；**D06 FAN STATUS** 读各风扇运行状态。

两个关键判读点：①**D05 与前面板灯语互补**——`CABLE OPEN：OK/OPEN` 与 `CABLE SHORT：OK/SHORT` 正是前面板 CABLE ALARM 的"内部复核"；`CAM POWER SUPPLY：ON/OFF` 对应摄像机供电。②**D06 的项随型号显隐**——`PS FAN`、`REAR FAN` 仅 HDCU5500/3500 显示；`FRONT FAN1/2`、`FRONT FAN4`、`REAR FAN1/2`、`REAR FAN4` 仅 HDCU5000 显示。**看不到某项往往是型号不同，不是故障**。

用途上，DIAGNOSIS 是"读"，不是"改"——它只提供诊断结果与版本/序列号，几乎所有项都是"仅显示"或状态读取。因此它的价值在于**把灯语/告警的现象收敛到硬件层级**，为更换风扇、板卡或联系 Sony 服务提供依据。手册明确指出选件安装/更换只能由经过培训的合格技术人员执行。

## A1 — 书中配置示例

**原书未提供 DIAGNOSIS 的操作实例**（手册为查阅型菜单表，D01–D06 只有"项目 + 显示/设置值 + 说明"，无现象→步骤的完整演算）。以下为**合成演练（非原书内容）**，按第 86-87 页规则可复算：

- 输入：前面板 ALARM 点亮，且 MAIN 灯闪烁（疑风扇错误）。
- 执行：进 DIAGNOSIS → D06 FAN STATUS 逐项读取；D01 BOARD STATUS 读 VIF/TX/NET 自诊断；D05 读 CAM POWER SUPPLY / CABLE OPEN / CABLE SHORT / RCP POWER。
- 预期：若某风扇项显示 `STOP` → 定位为该风扇故障（对照前面板 FAN STOP 灯）；若 D01 某板显示 `POWER ERROR` / `PLD ERROR` / `TEMP WARNING` → 定位到该板；若 D05 `CABLE OPEN:OPEN` / `CABLE SHORT:SHORT` → 与前面板 CABLE ALARM 一致。
- 型号差异复核（HDCU5000 读 D06）：含 `FRONT FAN1/2`、`FRONT FAN4`、`REAR FAN1/2`、`REAR FAN4`、`PS REAR FAN`，**不含** `PS FAN` 与 `REAR FAN`（此二项仅 HDCU5500/3500）。
- 反例推演：把"某项没显示"当故障 → 实为型号显隐差异（第 87 页）。

## A2 — 未来触发

**情境**：

1. ALARM 点亮后定位："到底是板卡、电源还是风扇的问题"。
2. 风扇异常："MAIN 灯在闪 / FAN STOP 亮 / 哪个风扇停了"。
3. 电缆异常复核："前面板 CABLE ALARM 亮，内部诊断怎么说"。
4. 版本/序列号查询："这台机什么版本 / ROM 版本 / 序列号是多少 / 报修要提供什么"。
5. 所连摄像机信息："接的是什么型号摄像机 / 摄像机 ROM 版本"。
6. 维护周期参考："累计开机多少小时了"。

**语言信号**：中文——"诊断 / DIAGNOSIS / BOARD STATUS / 板卡 / 自诊断 / 电源 / 风扇 / FAN STATUS / 版本 / VERSION / 序列号 / 开机小时 / HOUR METER / CABLE OPEN / CABLE SHORT / RCP POWER"；英文——"diagnosis / board status / fan status / power unit / version / serial number / hour meter / cable open / cable short"。

**相邻区分**：

- **ccu-panel-diagnostics**：本卡是"读硬件自诊断"，彼卡是"读前面板灯语"。灯先亮→彼卡分层；要确认到板卡/风扇/电源层级→本卡。
- **ccu-status-screen**：本卡读的是"硬件级自诊断（板/电源/风扇/版本）"，状态画面读的是"运行态（格式/音频/网络/告警）"。要"看板卡/风扇/版本"→本卡；要"逐页看系统状态"→彼卡。
- **ccu-file-log**：DIAGNOSIS 给出故障层级后，若需留证（日志导出）归彼卡。
- **RCP `specs-reference`**：型号规格、接口数量等纯数值速查归彼卡；本卡只读本机自诊断结果与版本串。
- **RCP `maintenance-correction`**：板卡/风扇的更换动作属服务范畴（ce40：仅合格技术人员执行），本卡只做诊断读值，不涉及拆装。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：①触发来源——前面板 ALARM / FAN STOP / MAIN 闪烁，或主动巡检；②本机型号（决定 D06 哪些风扇项存在、D03 哪些板版本项存在）；③是否装了 HKCU-FB50 / HKCU-SFP50（决定 TX/NET 相关项是否出现）；④目标——定位故障层级，还是读版本/序列号/开机小时。型号与选件不明先问，不臆测"项缺失=故障"。

1. **进菜单**：前面板 DISP/MENU 控制杆拨到 MENU → 选 DIAGNOSIS（需监视通路，接法见 ccu-status-screen）。
2. **按页读值**：
   - D01 BOARD STATUS：读 VIF / TX / NET 自诊断（OK / POWER ERROR / PLD ERROR / TEMP WARNING）；读 POWER ON HOUR METER、HOUR METER（上限 `99999 H`）。
   - D02 SERIAL NUMBER：读 MODEL NAME、SERIAL NUMBER。
   - D03 VERSION：读 APPLICATION / OS / UPDATER / SY / VIF / TX1(HIGH) / TX1(ULTRA) / TX2 / NET1 / NET2。
   - D04 CAMERA DIAGNOSIS：读 NAME、ROM VERSION（X.XX）。
   - D05 POWER UNIT STATUS：读 CAM POWER SUPPLY（ON/OFF）、CABLE OPEN（OK/OPEN）、CABLE SHORT（OK/SHORT）、RCP POWER（OK/ERROR）。
   - D06 FAN STATUS：读各风扇 OK/STOP。
3. **定位**：任一非 OK 值 → 定位到对应硬件层（板卡 / 电源 / 电缆 / 风扇），并与前面板灯语交叉确认。
4. **判停分支**：
   - 某诊断项"看不到" → 先核对型号与选件（如 D06 的 `PS FAN` 仅 HDCU5500/3500、`FRONT FAN1/2` 仅 HDCU5000），属显隐差异则非故障。
   - D05 `CABLE SHORT:SHORT` → 与前面板 CABLE ALARM SHORT 一致；**手册未给处置步骤**，如实说明（转 ccu-panel-diagnostics 的留白口径）。
   - D06 出现 `STOP` → 风扇故障，更换属服务范畴（ce40），本卡只报告。
   - D01 出现 POWER ERROR / PLD ERROR / TEMP WARNING → 板卡级故障，报 Sony 服务。
5. **验证**：诊断结论与前面板灯态/状态画面告警是否一致；不一致时以多处交叉为准。

**输出契约**：报告 = 触发来源 + 逐页读值（VIF/TX/NET、电源、电缆、风扇、版本、序列号原样）+ 定位层级 + 与灯语/告警的交叉结论 + 型号显隐说明 + 转介项（服务/日志留证）。

## B — 边界

- **不要用本卡**：灯语判读（ccu-panel-diagnostics）、状态画面逐页判读（ccu-status-screen）、日志处置（ccu-file-log）、规格速查（RCP `specs-reference`）、板卡/风扇更换动作（服务范畴，ce40）。
- **手册警告的失败模式**：
  - 把"型号显隐导致的项缺失"误判为故障（第 87 页，D06 型号限定）。
  - 把风扇/电池的"约 5 年更换周期"当作寿命保证（ce05，第 88 页）——手册明确"仅代表一般原则,不表示这些部件的寿命保证"。
  - D05 `CABLE SHORT:SHORT` 无处置步骤（与前面板 CABLE ALARM SHORT 同源留白）。
- **诚实留白（重点）**：DIAGNOSIS 只提供"诊断结果/版本/序列号"的**读取**，手册**未给出**任一非 OK 值的处置流程（如 POWER ERROR 后如何检修）；风扇/板卡的更换亦未给步骤（ce40：仅合格技术人员执行）。本卡不得为此类条目编造处置，只能给出"读值 → 定位层级 → 转服务/转留白"。
- **型号差异**：
  - D06：`PS FAN`、`REAR FAN` 仅 HDCU5500/3500；`FRONT FAN1/2`、`FRONT FAN4`、`REAR FAN1/2`、`REAR FAN4` 仅 HDCU5000；`PS REAR FAN` 无型号限定（第 87 页）。
  - D03：`TX1(HIGH)` / `TX1(ULTRA)` / `TX2` 为 HKCU-FB50 板项（HDCU3500 装 FB50 后）；`NET1` / `NET2` 为 HKCU-SFP50 板项（第 87 页）。
  - D01 的 `NET` 项为 HKCU-SFP50 板（选件）自诊断结果。
- **作者盲点（阶段 0 批判）**：DIAGNOSIS 是"查阅型"表，无"现象→原因→处置"决策树；`POWER ON HOUR METER` / `HOUR METER` 的 `99999 H` 为显示上限（单位 H 原样保留）；版本串 `X.XX`、`99999 H`、`CL108` 等须零改写。
