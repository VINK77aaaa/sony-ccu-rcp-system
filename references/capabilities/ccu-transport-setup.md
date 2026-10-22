> 吸收单元: f01, f02, f03, f04, f05, f06, p72（案例素材 c01, c02, c03, c04, c05, c06；反例 ce12, ce13, ce28, ce33, ce40；术语 g01, g02, g03, g09, g77, g78, g79, g80, g85, g86, g87, g88, g89, g91）

# 传输方式决策与连接配置 (HDCU5000/5500/3500)

## R — 原文

- "使用以下菜单项目设置要连接的摄像机的信号类型和信号传输速率。SYSTEM CONFIG t <CAMERA I/F> t CABLE TYPE t FIBER CAMERA CABLE；SYSTEM CONFIG t <CAMERA I/F> t FIBER TRANSMIT RATE" (第 4 页，脚注 a)
- "当使用 HDCU5000 时,信号传输最大可达 4k m,当使用 HDCU5500 时,最大可达 2k m。但是,实际传输距离和拍摄格式可能视摄像机的系统配置和使用的光纤电缆的类型而不同。" (第 4 页，脚注 b)
- "HDCU5000 有两个 FIBER CABLE 接口。一个接口可与 HDC5000/5500 连接。另一个接口可与 HDC3500 和 HDC2000 系列摄像机连接。HDCU5500 可与 HDC5000/5500 连接。" (第 4 页，脚注 c)
- "当 HDCU3500 连接到 HDC5000/5500 高清彩色摄像机时,如需进行光纤传输,请安装 HKCU-FB50 光纤接口套件。" (第 5 页，脚注 e)
- "安装 HKCU-SFP50 网络接口板。""连接到 HKCU-SFP50 网络接口板的 LAN 1 和 LAN 2 接口。""连接到 HDCU5000/5500/3500 的 LAN COM 接口。" (第 6 页，脚注 c/d/e)
- "SYSTEM CONFIG t <CAMERA I/F> t CABLE TYPE t SINGLE-MODE FIBER"；"信号传输最长可达 10 km。但是,实际传输距离可能视摄像机的系统配置和使用的单模光纤电缆的类型而不同。" (第 7 页)
- "将 SYSTEM CONFIG t <CAMERA I/F> t CABLE TYPE 设为 COAX。将 SYSTEM CONFIG t <VIDEO I/O> t SDI-I/O 3 t SIGNAL 设为 HD TRUNK。将 SYSTEM CONFIG t <VIDEO I/O> t SDI-I/O 4 t SIGNAL 设为 HD PROMPTER。" (第 7 页，脚注 b)
- "需要适合摄像机的专用电源 (外部直流电源) 。摄像机控制单元不提供电源。" (第 7 页，脚注 a)
- "将 SYSTEM CONFIG t <CAMERA I/F> t CABLE TYPE 设为 COAX(HDCE)。将 SYSTEM CONFIG t <VIDEO I/O> t SDI-I/O 3 t SIGNAL 设为 HD TRUNK。将 SYSTEM CONFIG t <VIDEO I/O> t SDI-I/O 4 t SIGNAL 设为 HD PROMPTER。" (第 8 页，脚注 a)
- CABLE TYPE：`FIBER CAMERA CABLE`、`COAX`、`COAX(HDCE)`、`SINGLE-MODE FIBER`，"SINGLE-MODE FIBER:仅当已安装 HKCU-SM50 时可选"；FIBER TRANSMIT RATE：`HIGH`、`ULTRA`、`---`。 (第 29 页，S01)
- "只能用于连接 HDC3500/3100 和 HDC2000 系列摄像机。 不能连接 HDC5000/5500。" (第 15 页，HKCU-SM50)
- OPTICAL SIGNAL BACKUP：`ENABLE`、`DISABLE`，"设置是否在 SYSTEM CONFIG 菜单的 <CAMERA I/F> 页面上保存 OPTICAL SIGNAL 设置状态以用于下次启动。" (第 77 页，M10)

## I — 自述

**本卡管什么。** CCU 与摄像机之间的物理通路怎么选、怎么接、要装哪些选件、要配哪些菜单项。这是整个系统的"第一道开关"：它一旦选错，后面所有格式配置都会建在错误的前提上。

**传输方式是五选一，不是"线缆型号"。** CABLE TYPE 只有四个取值（`FIBER CAMERA CABLE`、`COAX`、`COAX(HDCE)`、`SINGLE-MODE FIBER`），但连接示例共五种——因为 `FIBER CAMERA CABLE` 这一档在 HDCU5000/5500（连 HDC5000/5500）与 HDCU3500（连 HDC3500/3100/HDC2000）上是两套不同的拓扑。CABLE TYPE 是**系统模式开关**，不是物理线缆名：它决定 FIBER TRANSMIT RATE 是否可选（选 `COAX`/`COAX(HDCE)` 时该速率固定显示 `---`），进而派生后续全部输出/返回格式。

**前置条件链（顺序不可颠倒）。** ① 先看摄像机型号与 CCU 型号的兼容关系——HDCU5000/5500 对 HDC5000/5500；HDCU3500 对 HDC3500/3100/HDC2000 系列；② 再看需要哪些选件才能成立：光纤连 HDC5000/5500 在 HDCU3500 上必须装 HKCU-FB50；单模光纤必须装 HKCU-SM50 且必须配 HDCE-100 适配器；IP 传输必须装 HKCU-SFP50 并接 SFP+/SFP28 模块；③ 然后才设 CABLE TYPE；④ 最后设 FIBER TRANSMIT RATE（ULTRA＝连 HDC5000/5500 或装 HKC-FB50 的 HDC3500；HIGH＝连 HDC3500（未装 HKC-FB50）/HDC3100/HDC2000 系列）。链条中任一环缺失，传输方式就不成立。

**每种连接的必配项是"一个都不能少"的检查表。** 光纤：CABLE TYPE=FIBER CAMERA CABLE + FIBER TRANSMIT RATE（第 4/5 页脚注 a）。同轴 COAX：CABLE TYPE=COAX + SDI-I/O 3 SIGNAL=HD TRUNK + SDI-I/O 4 SIGNAL=HD PROMPTER（第 7 页），且**摄像机必须自带外部直流电源**——CCU 不为摄像机供电。同轴 HDCE：三项同上，仅 CABLE TYPE 取 COAX(HDCE)（第 8 页）。IP：装 SFP50、LAN1/LAN2 接交换机、LAN-COM 接 RCP/MSU 与 IP 计数器，且系统必须在 <OUTPUT FORMAT IP>/<RETURN FORMAT IP> 设格式（第 6/15 页）。单模光纤：CABLE TYPE=SINGLE-MODE FIBER + HDCE-100 + HKCU-SM50（第 7/15 页）。

**边界一：距离上限随型号分档。** 光纤传输 HDCU5000 约 4 km、HDCU5500 约 2 km、HDCU3500 约 2 km；单模光纤最长 10 km。手册两次强调"实际传输距离和拍摄格式可能视摄像机的系统配置和使用的光纤电缆的类型而不同"——上限是**理想值**，不是施工保证值。

**边界二：单模光纤有硬兼容红线。** HKCU-SM50 明令"只能用于连接 HDC3500/3100 和 HDC2000 系列摄像机。不能连接 HDC5000/5500"（第 15 页）。也就是说，单模光纤这条通路在 4K 摄像机上是**不存在**的，与"想拉 10 km 又想连 4K 机"的诉求直接冲突。

**边界三：光纤接口不接时必须盖盖。** 手册在第 11/12/14 页三处重复："光纤电缆表面的灰尘可能会造成传输错误。不连接光纤电缆时,请务必用附带的盖子盖住接口端。"这与 CABLE CONDITION 灯降级直接相关，属于施工纪律而非菜单项。

**持久化边界：OPTICAL SIGNAL 默认不跨重启记忆。** <CAMERA I/F> 页的 OPTICAL SIGNAL（`ON`/`OFF`，仅在使用光纤复合线缆连接时显示）是运行时开关；要让它在下次启动时保留，必须把 <MISC> 的 OPTICAL SIGNAL BACKUP 设为 ENABLE（第 77 页，M10）。

## A1 — 书中配置示例

以下均为**书中自带连接示例**（原书第 4–8 页的五张连接图及其脚注，非实际工程记录）：

1. **光纤传输 — HDCU5000/5500**（c01，第 4 页）：CCU 与 HDC5000/5500 之间走光纤电缆，菜单配 `SYSTEM CONFIG t <CAMERA I/F> t CABLE TYPE t FIBER CAMERA CABLE` 与 `FIBER TRANSMIT RATE`（脚注 a）。HDCU5000 距离上限约 4 km、HDCU5500 约 2 km（脚注 b）。HDCU5000 有**两个** FIBER CABLE 接口：一个连 HDC5000/5500，另一个连 HDC3500 与 HDC2000 系列（脚注 c）。
2. **光纤传输 — HDCU3500**（c02，第 5 页）：HDCU3500 连 HDC3500/3100、HDC2000 系列，距离最长约 2 km（脚注 b）；若要连 HDC5000/5500 并做光纤传输，必须补装 HKCU-FB50（脚注 e）。
3. **IP 连接（SMPTE ST2110）**（c03，第 6 页）：装 HKCU-SFP50（脚注 c），LAN1/LAN2 接 IP 交换机 10G/25G（脚注 d），LAN-COM 接 RCP/MSU 与 IP 计数器（脚注 e）；SNMP 需 HZCU-SNMP50（脚注 f）、Ember+ 需 HZCU-CNFG50（脚注 g）。图中还标出 PTP 主站 × 2、IP Live System Manager × 2、IP 交换机 10G/25G × 2、IP 交换机 1G、IP 交换机 10G/1G。距离：HDCU5000 约 4 km、HDCU5500/3500 约 2 km（脚注 a）。
4. **单模光纤连接**（c04，第 7 页）：装 HKCU-SM50（脚注 b）、配 HDCE-100 摄像机扩展适配器、CABLE TYPE=SINGLE-MODE FIBER（脚注 c）、最长 10 km（脚注 d）。图中受支持摄像机仅为 HDC3500/3100、HDC2000 系列（脚注 a）。
5. **同轴电缆连接**（c05，第 7 页）：CCU 侧 HDCU5500/3500（脚注 b）；三连菜单 `CABLE TYPE=COAX`、`SDI-I/O 3 SIGNAL=HD TRUNK`、`SDI-I/O 4 SIGNAL=HD PROMPTER`（脚注 b）；摄像机侧需外部直流电源（脚注 a）；BNC 电缆（HD SDI）接 SDI 1、SDI 2、SDI I/O 3、SDI I/O 4。
6. **同轴电缆（HDCE）连接**（c06，第 8 页）：HDCU3500 + HDCE-200 摄像机扩展适配器 + HDC2500/2400（或 HDC3500）；三项菜单同上，仅 CABLE TYPE 取 `COAX(HDCE)`（脚注 a）。

**书中未给完整示例的部分**：手册未给出"某现场按距离/型号逐步推演出唯一 CABLE TYPE 与 FIBER TRANSMIT RATE"的端到端文字演算（连接图是图示+脚注形式，纯文本提取会丢失布线细节）。以下为**合成演练（非原书内容）**，仅演示本卡决策链的用法：

> 合成演练：现场一台 HDCU5000，手头单模光缆，摄像机为 HDC3500，已装 HKCU-SM50 与 HDCE-100，SYSTEM=1.001(525)。按第 7 页脚注 b/c/d 与第 15 页规则：① 摄像机 HDC3500 属 SM50 允许清单（非 HDC5000/5500），通过；② CABLE TYPE=SINGLE-MODE FIBER；③ 距离 10 km 以内；④ 因摄像机未装 HKC-FB50，FIBER TRANSMIT RATE=HIGH。结论：CABLE TYPE=SINGLE-MODE FIBER + HIGH，配 HDCE-100。

## A2 — 未来触发

**情境**：

1. 新装/搬迁机位："这台 CCU 跟摄像机怎么接 / 用什么传输方式 / 要买什么选件"。
2. 采购或方案评审阶段：问光纤能拉多远、单模还是多模、同轴要不要外接电源。
3. 现场不通时回查：CABLE ALARM 亮、摄像机无电、或连上后格式对不上，怀疑传输方式选错。
4. 换摄像机型号（如把 HDC3500 换成 HDC5000）后，评估传输方式与选件是否需要变更。
5. 做"传输方式 → 菜单必配项"的施工检查单。

**语言信号**：中文——"传输方式 / 怎么连 / 光纤还是同轴 / 单模光纤 / IP 连接 / CABLE TYPE / 传输速率 / 要装什么选件 / 能拉多远 / 摄像机没电"；英文——"transport / connection setup / fiber / coax / single-mode fiber / ST2110 / CABLE TYPE / FIBER TRANSMIT RATE / option kit / max distance"。

**相邻区分**：

- **ccu-system-format**：本卡管"通路怎么建"（CABLE TYPE / 选件 / 距离 / 必配菜单项）；彼卡管"通路建好后系统工作在哪一档频率与格式"（SYSTEM / CAMERA FORMAT / BIT DEPTH / 延迟）。问"怎么接"归本卡，问"设成什么格式"归彼卡。二者共享 FIBER TRANSMIT RATE 这个交界项：本卡只判它的**取值依据**（连什么摄像机/装没装 FB50），彼卡用它的**取值结果**去派生 CAMERA FORMAT 候选集。
- **ccu-format-lookup**：本卡不回答"某接口能出什么格式"；那属于彼卡（四页分流查表）。
- **ccu-hdr-setup**：HDR 是格式链的下游，归彼卡。
- **RCP 侧 network-setup**：面板侧 CNS/IP/接地归那张卡；本卡只处理 CCU 与摄像机之间的通路（含 CCU 侧 LAN-COM 接 RCP/MSU，但不含面板自身的组网配置）。
- **RCP 侧 led-diagnostics**：CABLE ALARM / CABLE CONDITION 的灯语判读归彼卡；本卡负责把连接"接对"。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：① CCU 型号（HDCU5000 / 5500 / 3500）；② 摄像机型号（HDC5000/5500、HDC3500/3100、HDC2000 系列或其他）；③ 手头线缆类型（光纤复合缆 / 单模光纤 / 同轴 BNC / 网线）；④ 现场距离；⑤ 已装/可装选件清单（HKCU-FB50 / SDI50 / SFP50 / SM50，HZCU-UHD35）；⑥ 是否需要 IP 传输（ST2110）。任一缺失先询问，不得静默假定。

1. **兼容性判定**（不过即停）：按第 3/4/5 页规则核对 CCU↔摄像机配对。HDCU5000/5500 ↔ HDC5000/5500；HDCU3500 ↔ HDC3500/3100/HDC2000 系列。若 HDCU3500 要连 HDC5000/5500，**必须先装 HKCU-FB50**（装后规格等同 HDCU5500），否则光纤传输不成立。
2. **通路归类**（输出唯一结果）：
   - 光纤复合缆 → `FIBER CAMERA CABLE`；
   - 单模光纤 → `SINGLE-MODE FIBER`（**前置**：已装 HKCU-SM50 + HDCE-100；**红线**：摄像机不得是 HDC5000/5500）；
   - 同轴 BNC → `COAX`；
   - 同轴 + HDCE-200 适配器 → `COAX(HDCE)`；
   - 网线 + IP 交换机 → IP 连接（装 HKCU-SFP50，走 LAN1/LAN2）。
3. **距离核对**（超距即停）：光纤 HDCU5000 约 4 km / HDCU5500 约 2 km / HDCU3500 约 2 km；单模光纤 10 km。超限不施工，改方案或加中继/换通路。
4. **选件核对**：按通路列出必备选件——光纤（HDCU3500 连 4K 机时）HKCU-FB50；单模 HKCU-SM50 + HDCE-100；IP HKCU-SFP50 + SFP+/SFP28 模块（如 OTM-10GSR1）；4K 输出另需 HZCU-UHD35。**选件安装仅限受过服务培训的合格技术人员**（第 14 页），本卡不提供安装步骤，须联系 Sony 服务或销售代表。
5. **配菜单**：进入 `SYSTEM CONFIG t <CAMERA I/F>`：
   - 设 CABLE TYPE 为上一步归类值；
   - 设 FIBER TRANSMIT RATE（ULTRA / HIGH；COAX 与 COAX(HDCE) 下显示 `---`）；
   - 如需跨重启保留 OPTICAL SIGNAL，另到 `<MISC>` M10 把 OPTICAL SIGNAL BACKUP 设为 ENABLE。
6. **同轴/HDCE 追加项**：到 `SYSTEM CONFIG t <VIDEO I/O>`，把 SDI-I/O 3 的 SIGNAL 设为 HD TRUNK、SDI-I/O 4 的 SIGNAL 设为 HD PROMPTER；确认摄像机已接外部直流电源。
7. **IP 追加项**：装 SFP50、LAN1/LAN2 接交换机、LAN-COM 接 RCP/MSU 与 IP 计数器；到 `<OUTPUT FORMAT IP>` / `<RETURN FORMAT IP>` 设格式（格式选择见 ccu-format-lookup）；ST2110 系统 GENLOCK MODE 须设 NETWORK（同步细节见同步卡）。
8. **收尾核对**：光纤接口未接的必须盖盖（第 11/12/14 页）；核对系统配置设备的软件与 ROM 版本兼容（第 3 页）。

**判停分支**：连接后摄像机无电 → 先看 CABLE ALARM 是否 OPEN/SHORT（此时 CCU 不向摄像机供电，ce28），灯语判读转 led-diagnostics；连接后格式选项对不上 → 转 ccu-system-format 核对速率/系统频率；需要查某接口实际输出格式 → 转 ccu-format-lookup。

**输出契约**：报告 = 选定传输方式（CABLE TYPE 取值）+ FIBER TRANSMIT RATE 取值 + 必备选件清单 + 距离核对结论 + 已配菜单项清单 + 未决/需 Sony 确认项。

## B — 边界

- **不要用本卡**：输出/返回格式查表（ccu-format-lookup）、系统频率与摄像机格式设定（ccu-system-format）、HDR 配置（ccu-hdr-setup）、CABLE ALARM/CABLE CONDITION 灯语判读（led-diagnostics）、面板侧组网与 IP 规划（network-setup）、规格数值速查（specs-reference）、选件安装步骤（手册未给，见下）。
- **手册警告的失败模式**：
  - 单模光纤接口（HKCU-SM50）**不能连接 HDC5000/5500**，只能连 HDC3500/3100 和 HDC2000 系列（ce12，第 15 页）——把单模光纤接到 4K 摄像机是硬错误。
  - 光纤接口不连接时必须盖盖，端面灰尘会造成传输错误（ce13，第 11/12/14 页）——表现为 CABLE CONDITION 降级。
  - CABLE ALARM 亮起（OPEN 或 SHORT）时**不会对摄像机供电**（ce28，第 10 页）——"摄像机没电"的第一根因就在 CCU 侧，不要先怀疑摄像机。
  - 操作本系统之前必须检查本机与系统配置设备的软件和 ROM 版本是否兼容（ce33，第 3 页）——新设备直接接入既有系统前先核版本。
  - 选件安装/更换只允许经过服务培训的合格技术人员操作（ce40，第 14 页）——未受训人员不得自行拆机装选件。
- **型号差异**（三型号差异极大，必须逐条声明）：
  - **HDCU5000**：两个 CAMERA FIBER 接口（一个连 HDC5000/5500，另一个连 HDC3500 与 HDC2000 系列）；光纤传输约 4 km；可装 HKCU-SDI50（12GSDI 接口板，装于背面选件套件安装端口 3，解锁 UHD-SDI E/F/G/H 与 UHD-SDI G/H 返回）；HKCU-SM50 装于端口 qg；HKCU-SFP50 装于端口 1。
  - **HDCU5500**：1U 紧凑型，单个 CAMERA FIBER 接口，连 HDC5000/5500；支持 4K；光纤传输约 2 km；**不能装 HKCU-SDI50**；机架安装需 RMM-301 适配器。
  - **HDCU3500**：入门型，**仅 HD**；连 HDC3500/3100/HDC2000 系列；光纤传输约 2 km；**必须装 HKCU-FB50 才等同 HDCU5500**（才支持 4K 传输），且**必须再装 HZCU-UHD35 才能做 4K 输出**；机架安装需 RMM-301 适配器。
  - **选件依赖汇总**：光纤（3500 连 4K 机）→ HKCU-FB50；4K 输出 → HZCU-UHD35（且第 3 页注明"当安装了 HKCU-SM50 时,在 HDCU5000/5500 上支持此软件"）；IP → HKCU-SFP50（+SFP+/SFP28 模块）；单模 → HKCU-SM50（+HDCE-100）；SNMP → HZCU-SNMP50；Ember+ → HZCU-CNFG50。**菜单项显隐随选件**：CABLE TYPE 的 `SINGLE-MODE FIBER` 仅装 HKCU-SM50 时可选（第 29 页）；`<OUTPUT FORMAT IP>`/`<RETURN FORMAT IP>` 仅装 HKCU-SFP50 时显示。
- **作者盲点（阶段 0 批判）**：
  - 手册多处写"有关设定的详细说明,请联系 Sony 维修代表或销售代表"（如第 11/12/13/14 页的 SDI/接口设定），属**故意留白**，本卡不编造步骤。
  - SFP+/SFP28 模块型号手册明确"使用 IP 输出需要 OTM-10GSR1 或其他 SFP+ 模块或 SFP28 模块"，未给完整兼容列表，须向 Sony 确认。
  - 连接拓扑大量依赖图示，纯文本提取丢失布线细节，本卡只保留"选件 ↔ 菜单项"的文字规则。
  - 选件安装步骤手册不提供（限定受训人员执行），本卡不含安装流程。
  - 距离上限是理想值，手册两次声明"实际传输距离和拍摄格式可能视摄像机的系统配置和使用的光纤电缆的类型而不同"，不得当作施工保证值。
  - UHB（HKCU-FB50 套件名）手册只使用未定义（g83，needs-review），不得解读为"超宽带"。
