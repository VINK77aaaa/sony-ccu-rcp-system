# 术语词典 — 《Sony 摄像机控制系统使用说明书合辑》

> 阶段 3 产出 · 合辑共享术语词典，共 **128** 条 = **RCP 侧 35 条**（编号 `g01`–`g35`）+ **CCU 侧 93 条**（编号 `h01`–`h93`，其中 3 条待复核）。
> 来源两书：①《遥控面板 RCP-3500/3501 使用说明书》（Sony, 2019，文档号 5-017-036-61 (1)，56 页）；②《摄像机控制单元 HDCU5000 / HDCU5500 / HDCU3500 使用说明书》（Sony, 2019，文档号 5-006-304-43 (1)，94 页）。
> 条目内容自阶段 1 抽取候选与阶段 1.5 三重验证记录**逐字保留，未改写**；合并时只做两件事——加本合辑标题头、给 CCU 侧编号加前缀 `h`。
> 编号规则：RCP 侧沿用其单书编号 `g01`–`g35`（不改）；CCU 侧单书原为 `g01`–`g93`，并入合辑后统一加前缀 `h`，即 **`hNN` ≡ CCU 单书 `gNN`**（一一对应，便于回查 CCU 单书验证记录）。
> 形态差异说明：RCP 侧保留其原始 **YAML 记录**形态（字段含 `source_chapter` / `key_distinction` / `why_it_matters` / `tags`）；CCU 侧保留其 **术语域分组表格**形态（术语 / 手册定义 / 与常识用法的差异）。二者不强行统一，以保真为先。
> 标 `†` 者（`h13` / `h14` / `h83`）手册**只使用未定义**，释义含行业通用知识，待复核通过后才转正式条目。
> 数值、单位、格式串一律**原样保留**（如 `3840×2160/59.94P/12G`、`CCA-5 200 m`），未做改写或换算。

---

## 0. 跨书术语对照（合并后新增）

同一条"控制—被控"链上的两端术语，单独一本书都看不全。下表把**两侧同名/近名但语义或作用域不同**的术语并列，并给出差异要点与跨书操作含义。带「（推断）」者为两侧文本并列后的合理推论，**未经原文直接确认**，使用前需现场验证。

| 术语 | RCP 侧（编号） | CCU 侧（编号） | 差异要点与跨书操作含义 |
|---|---|---|---|
| **CNS / 连接模式** | 四选一：`LEGACY` / `BRIDGE` / `MCS` / **`PC 控制`**（HZC-RCP5，最多 6 台 RCP）；改 CNS 后须重启所有摄像机系统（g01） | 三选一：`LEGACY` / `BRIDGE` / `MCS`；MCS MODE 为**仅显示**固定值 `CLIENT`（h49） | **两侧模式集合不对等**：RCP 侧多一个"PC 控制"，CCU 侧无此项。面板侧选 PC 控制时 CCU 侧 CNS MODE 应如何对应，两书均未给 → 跨书缺口，须按现场拓扑确认。 |
| **CCU 编号 / CCU NO** | "CCU 编号取值 1–96、A–Z"（g02） | CNS MODE 选 MCS 时 `空白, 1 至 96`；选 LEGACY / BRIDGE 时 `空白, 1 至 96, A 至 Z`（h50） | RCP 手册写法笼统；**CCU 手册明确 MCS 下不允许 A–Z**。编号规划以 CCU 侧取值域为准，两侧编号须全系统唯一。 |
| **MCS 主设备** | MSU-1500/1000 或 CNA-1 可作主设备；多 MSU 时一主一从；RCP 编号 = MSU 的机位选择号（g03） | `MASTER IP ADDRESS`：本机作为客户端去连的主设备 IP（h51） | 两侧互补：RCP 侧回答"谁是主设备"（设备层），CCU 侧回答"主设备 IP 填什么"（网络层）。两侧必须指向同一台主设备。 |
| **同步 / GenLock** | 只做**相位微调**：Maintenance > CCU > Phase，含 H / H Step / H Coarse / **SC Phase**（VBS 子载波）；GenLock Mode 选 HD3 值 SYNC 或 BBS（g28） | 决定**参考源与锁定模式**：GENLOCK MODE `HD`/`SD`/`NETWORK` + PTP ST2059-2 + H-PHASE STEP / H-PHASE COARSE / V-PHASE + 10F BB + LOCK STATUS（h29–h36） | 同一个"同步"，**参考源与模式在 CCU 侧定，面板侧只是遥控相位入口**。RCP 侧另有 CCU 侧未列的 `SC Phase`（VBS 子载波，仅模拟复合输出相关）；CCU 侧另有面板侧无概念的 `NETWORK` 模式（ST2110 强制，需 HKCU-SFP50）。两侧同名相位项是否互相覆盖：（推断）同一参数的两个视图，需现场验证。 |
| **返回信号 / RETURN** | `Return Settings`（工程师模式）：Return-1 到 4 的 Input / Aspect / LB Mode / OETF / C Space——**设定格式**（g29） | `RETURN SELECT` + `RETURN FORMAT1-4`（S12–S16）：定义返回信号来源与**格式矩阵**（p49–53）（h64） | 两侧都叫"返回设定"但分工不同：CCU 侧矩阵决定每路可用格式，面板侧在此范围内指定取哪路、以及 SD 纵横比与 HDR 相关项。改一侧前先看另一侧是否被锁。 |
| **文件 / FILE** | **摄像机图像参数**资产：场景文件（面板 1–5 直达 + 菜单最多 32）、参考文件、镜头文件、OHB 文件；USB 备份分 RCP Config 与 Network Config（g13–g16） | **CCU 整机菜单设置**快照：`CCU FILE` 最多 5 个，`RECALL` **不含** LAN COM 的 IP / 子网 / 网关；`LOG` 最多 30 天，改 DATE&TIME 清空全部日志；USB 路径固定 `/MSSONY/PRO/CAMERA/HDCU5000`（h67–h70） | **对象完全不同、互不覆盖**：RCP 文件管"画成什么样"，CCU 文件管"机器怎么配"。两侧各有 USB 备份通道但内容不相交；换机恢复必须两套都做。 |
| **Tally / 计数器** | Tally（红/绿/橙）经 EXT I/O 或 CCU 传输（g12） | `TSL UMD` V5.0（UDP 端口 8900）IP 计数器；`INTERCOM/TALLY/IO` 50 芯 D-sub 一口多用（h41 / h61） | RCP 侧讲信号与线，CCU 侧给协议与物理引脚。IP 化（TSL UMD）与物理引脚两条路都在 CCU 侧。 |
| **供电（摄像机侧）** | `CAM PW` 四态灯语："从 CCU 向摄像机供电"（g02） | `CAMERA FIBER` 一根光纤同时承载电源/控制/视频/音频；**`CABLE ALARM` 亮（OPEN / SHORT）时不会对摄像机供电**（h03 / h75） | **跨书排障要点**：面板侧 CAM PW 按了没反应，可能是 CCU 侧 CABLE ALARM 触发（光纤断/短路）。排障顺序应先看 CCU 灯，再看面板灯。 |
| **供电（面板侧）** | 面板双供电路径：EXT I/O（10.5–17 V 直流）或 PoE（IEEE802.3af class 2，36–57 V，功耗 10 W）；PoE 缆长 ≤ 100 m（g33） | `RCP/CNU 接口`（8 芯 CCA-5）：连 MSU-1000 系列 / CNU-700 / RCP-3000/1000 系列，"**用 RCP-3000/1000 系列时还提供电源**"（h08） | **两书对 RCP-3500/3501 的供电来源描述不一致**（CCU 手册只把"经 RCP/CNU 供电"归给 RCP-3000/1000 系列，而 RCP 手册另有 EXT I/O 与 PoE）。已在合辑缺口清单记录，施工前须以实际机型确认。 |
| **网络接口** | 面板 LAN 口：接 LAN 集线器，缆长 ≤ 100 m；**仅用 LAN 连接时必须接地**（g34 附带规则） | 两套口：`LAN-COM`（5 类以上屏蔽型，10/100/1000BASE-T）承载 RCP/MSU 连接、Web 菜单、Ember+、SNMP、TSL UMD、NMOS；`LAN 1/2`（HKCU-SFP50，SFP+/SFP28）专用于 IP 视频/音频/对讲与 PTP 网络同步（h04 / h79） | 面板接的是 CCU 的 **LAN-COM**，不是 LAN1/LAN2。手册侧证：DHCP"自动 IP"**仅适用于 LAN COM**，不适用于 LAN1/LAN2（h47）。把面板误接 LAN1/LAN2 的后果手册未述 → 缺口。 |
| **HDR** | `HDR Conversion`（SDR→HDR 转换）+ `HDR Operation`（Black Offset / SDR Gain / HDR Contrast / HDR Knee / HDR White Clip / HD Detail Reduction）——作用在**摄像机图像**（g32） | `LIVE HDR`（HDR/SDR 同步双输出）+ `OETF`（S-Log3 / HLG）+ HDR / 4K COLOR SPACE + SDR GAIN / HDR CONTRAST / HDR BLACK OFFSET——作用在 **CCU 输出与返回信号**（h21–h28） | **两个不同的 HDR 域**：面板侧调"图像怎么变 HDR"，CCU 侧调"输出哪一路 HDR、哪一路 SDR"。两侧的 `SDR GAIN` / `HDR CONTRAST` / `HDR BLACK OFFSET` **同名但分属不同域**（面板侧在 HDR Operation，CCU 侧在 HDR 输出配置），不可互推。 |
| **色彩空间 / 伽马** | Gamma Table（Standard / Hyper / Special / User）、Matrix（User / Preset / Multi / Adaptive）、Knee、Black Gamma（g20–g22） | `OETF` 取值随接口变化（SDI/IP 为 `SDR`/`HDR OETF`，UHD-SDI 为 `SDR`/`4K OETF`）、HDR COLOR SPACE `BT709`/`BT2020`、4K COLOR SPACE（LIVE HDR 下强制同 HDR COLOR SPACE）（h22 / h24 / h25） | 面板侧是"创作向"曲线族（可存场景文件），CCU 侧是"输出向"标记（BT709/BT2020 与 OETF 取值）。改面板侧曲线不会自动改 CCU 侧色彩空间标记。 |

---

# A 部分 · 遥控面板 RCP-3500/3501（35 条，编号 `g01`–`g35`）

> 本部分逐字取自 RCP 单书术语词典，**编号与内容均未改动**。字段：`source_chapter` 以"首现 pX"标注术语首次出现的页码，再给定义所在页；缩写均给全称（手册未展开全称者已注明）。

```yaml
- id: g01
  term: CNS（连接模式：LEGACY / BRIDGE / MCS / PC 控制）
  type: term
  source_chapter: 首现 p5（概述·系统配置）；设定步骤 p18-19
  author_definition: |
    "更改连接模式 (CNS) 后,需重启所有摄像机系统。" (p5)
    RCP 与被控设备之间的连接模式体系，四选一：
    - LEGACY："使用 CCA-5 电缆连接摄像机控制单元 (CCU) 和 RCP"，"TCP/IP 和 RCP 编号无需设定" (p5/p18)。
    - BRIDGE："使用 LAN 电缆连接 CCU 和 RCP (一对一)"，需配置本机 IP 与目标 IP (p5)；
      "在 BRIDGE 模式中,无法采用多摄像机操作" (p18)；子模式 Active/Passive/Semi-Auto (p19)。
    - MCS：多摄像机系统，经 LAN 组网，"除了设定本机的 TCP/IP 设定和主设备的 IP 地址以外,还必须设定 RCP 编号" (p19)。
    - PC 控制："使用 HZC-RCP5 摄像机远程控制软件配置"，"可连接最多六个 RCP 单元" (p6)。
  key_distinction: |
    ≠ 通用网络术语 — 手册未展开 CNS 全称，它是 Sony 遥控系统连接模式的总称
    ≠ 可随意切换的软件设置 — 模式变更"需重启所有摄像机系统"，IP/编号冲突会导致整系统不通
    = 全系统组网的第一决策；混合拓扑（LAN 连面板 + CCA-5 连 CCU）也归入 MCS (p19)
  why_it_matters: |
    所有连接类 skill 的前置分叉：IP 规划、编号唯一性、接地要求、可否多机操作，全部挂在具体 CNS 模式下。
  tags: [term, core-concept]

- id: g02
  term: CCU（摄像机控制单元，Camera Control Unit）
  type: term
  source_chapter: 首现 p4；全称与组网 p5；供电 p10；CCU 侧维护 p43/p46/p50
  author_definition: |
    "摄像机控制单元 (CCU)" (p5)，RCP 的控制对象与中继：面板经 CCU 控制摄像机
    （HDCU5000/5500/3500 等，支持清单见 p8）。CCU 编号取值 "1–96、A–Z" (p5)。
    供电关系："按此按钮 (CAM PW) 可从 CCU 向摄像机供电" (p10)，CAM PW 灯四态：
    亮=供电中／熄灭=已断电且按了无效／慢闪=已断电按下即接通／快闪=摄像机正在启动 (p10)。
  key_distinction: |
    ≠ 摄像机机身 — 面板直接对话的是 CCU，摄像机是 CCU 的下游；
    供电 (CAM PW)、同步相位 (CCU Phase, p43)、返送格式 (Return Settings, p50) 都配置在 CCU 侧。
  why_it_matters: |
    灯语诊断（NETWORK/ALARM/CABLE/CAM PW）与维护/Config 的多个项目都以 CCU 为对象；
    CAM PW 四态灯语是"摄像机是否在开机"的第一判断入口。
  tags: [term, core-concept]

- id: g03
  term: MSU（主设置装置，Master Setup Unit）/ CNA-1
  type: term
  source_chapter: 首现 p7（MCS 连接示例）；主/客户端规则 p19
  author_definition: |
    "主设置装置 (MSU) 或 CNA-1 可用作主设备" (p7)；型号 MSU-1500/1000 (p8)。
    "当使用多个 MSU 设备时,将一个设备配置为主设备,将另一个设备配置为客户端" (p19)。
  key_distinction: |
    ≠ RCP — MSU/CNA-1 是 MCS 系统的主设备候选（Master/Client 中的 Master），RCP 是受其仲裁的客户端面板；
    "RCP 编号对应于 MSU 的摄像机选择编号" (p19)。
  why_it_matters: |
    MCS 组网必须先指定主设备；RCP 编号即 MSU 上的机位选择号，编号重复"设备无法正常工作" (p19)。
  tags: [term]

- id: g04
  term: RCP Assign（RCP 分配）
  type: term
  source_chapter: 首现 p7（"RCP 分配"）；RCP Assign 菜单 p47/p49
  author_definition: |
    "选择要通过控制面板控制的目标摄像机。只能在 MCS 模式中设定。此外,所有连接的设备都必须支持 RCP 分配功能" (p47)；
    "可以更改本机控制的摄像机编号" (p49)；[All Camera] 可显示所有摄像机，[Reset] 恢复标准分配 (p49)。
  key_distinction: |
    ≠ 重新接线 — 软件地把某台面板指到另一台摄像机；分配期间"待控制目标摄像机的编号会闪烁" (p14)；
    = ABSOLUTE 自动退回相对值模式的触发条件之一："当使用 RCP Assign 设定更改受控的 CCU/HDCU 时" (p13)。
  why_it_matters: |
    多机位演播中操作者换机位的核心手段；"面板控制了错误机位"类问题的排查入口。
  tags: [term]

- id: g05
  term: 面板激活（PANEL ACTIVE）
  type: term
  source_chapter: 首现 p8（MCS 摄像机操作）；按钮细节 p15；相关设定 p48
  author_definition: |
    "当 PANEL ACTIVE按钮指示灯亮起时的状态。处于激活状态的 RCP 可以操作相应设备。
    其他 RCP 上会显示值,但不能操作设备" (p8)。
    "此按钮用于控制许可。其还可作为一项防止误操作的功能使用,因为当此按钮和 PARA 按钮的指示灯未亮起时,
    无法通过此控制面板控制摄像机" (p15)。
    "如果 MCS 模式系统的主设备断开, 则不可实现面板激活操作。在这种情况下,长按 PANEL ACTIVE按钮将强制激活面板" (p15)。
  key_distinction: |
    ≠ 软件"激活/授权"概念 — 这是多控制器之间的硬件仲裁状态，同一时刻全系统仅一台面板拥有控制权
    ≠ 灯灭即故障 — 未激活面板仍显示数值，只是不能操作
    = 主设备断开时"长按强制激活"是手册给出的唯一旁路 (p15)
  why_it_matters: |
    MCS 模式一切操作的前提；"能看到值但拧不动旋钮"的现象首先查此灯。
  tags: [term, core-concept]

- id: g06
  term: PARA（并行控制，Parallel Control）
  type: term
  source_chapter: 首现 p8；按钮 p10；联动规则 p13
  author_definition: |
    "通过在未激活的控制面板按下 PARA 按钮,从多个控制器进行并行控制" (p8)；
    "此功能可使用处于激活状态的控制面板进行同步控制" (p10)。
  key_distinction: |
    ≠ 面板激活 — PARA 是激活之外的多面板共同控制通道；"在光圈 / 主黑电平激活状态下...PARA(并行控制)不可用" (p8)
    ≠ 无副作用 — PARA 或主/从模式下 ABSOLUTE 自动退回相对值模式 (p13)
    = 与主/从功能（Multi 菜单 p54：基于主摄像机做白平衡跟随，"可用于在旧有连接中使用 CNU (命令网络单元)的系统。LAN 连接不可用"，p8）同属多控制器机制
  why_it_matters: |
    多操作者协作（VD + 灯光/美术各自跟参数）的依据；误开会导致面板之间互相覆盖设定。
  tags: [term, core-concept]

- id: g07
  term: IRIS/MB ACTIVE（光圈 / 主黑电平激活）
  type: term
  source_chapter: 首现 p8；按钮 p14；相关设定 p25/p47/p48
  author_definition: |
    "此按钮用于光圈和主黑电平控制许可功能。光圈和主黑电平仅可在此按钮指示灯亮起时调节。
    按下PANEL ACTIVE按钮亦可导致此按钮指示灯亮起" (p14)；
    "在光圈 / 主黑电平激活状态下, 为了防止误操作,PARA(并行控制)不可用。只有 IRIS/MB ACTIVE 按钮指示灯亮起的
    RCP 可以操作设备" (p8)。
  key_distinction: |
    ≠ PANEL ACTIVE — 它是光圈/主黑层面的第二层独立许可；主黑电平调节功能在 RCP-3501 上不可用 (p25)，
    其 MB Knob 可改配其他功能 (p47)；可经 RCP Mode 设定 "IRIS/MB Active Mode...以仅启用 IRIS" (p48)。
  why_it_matters: |
    "光圈拧不动"的第一排查点；多机位时光圈师与 VD 的控制权划分即靠此灯。
  tags: [term]

- id: g08
  term: 控制许可（ND/CC 滤镜）
  type: term
  source_chapter: 首现 p11（ND 滤镜）；CC 滤镜 p12
  author_definition: |
    "当本机具有 ND 滤镜的控制许可时,这些按钮指示灯会亮起。如果未亮起,则表示摄像机具有控制许可。
    按一次顶部按钮或底部按钮,可将控制许可切换到本机。如果没有滤镜伺服或摄像机没有 ND 滤镜,
    这些按钮的指示灯不会亮起,且无法切换控制许可" (p11；CC 滤镜同, p12)。
  key_distinction: |
    ≠ 安全限制（Page/Item Permission）— 控制许可是面板与摄像机机身之间对同一执行器的即时"夺取"；
      安全限制是面板菜单层面的功能门（见 g11）
    ≠ 灯不亮即故障 — 灯灭只说明许可在机身侧，按上/下按钮即可夺取
  why_it_matters: |
    日常滤镜操作的前置判断（task-05）；无滤镜伺服的机型该机制整体不生效。
  tags: [term]

- id: g09
  term: 工程师模式（Engineer Mode）
  type: term
  source_chapter: 首现 p16；进入/退出步骤 p17；适用范围 p16/p18/p38/p39/p46
  author_definition: |
    "为防止误操作,控制面板的部分设定具有功能限制,不会显示出来。进入工程师模式后,此类限制均将取消" (p17)。
    路径：MENU > Config > RCP > Security > [Engineer Mode] (p17)。
    范围：File 菜单 "仅在工程师模式下显示" (p38)；Maintenance 同 (p39)；
    "在工程师模式中配置所有连接设定" (p18)；Config 菜单未标星号的项目亦然 (p46)。
  key_distinction: |
    ≠ 管理员账户 — 没有用户体系，只是画面级隐藏层，退出即隐藏
    ≠ 让 Paint 可见的唯一途径 — Page Permission 的 Full Paint=ON 也能显示全部 Paint 菜单 (p16/p20)
  why_it_matters: |
    除日常 Paint/Scene/Function/Multi 外几乎所有配置的前置门；
    "菜单里找不到某一项"类问题首先检查是否处于工程师模式。
  tags: [term, core-concept]

- id: g10
  term: 安全代码（Engineer Protection，初始码 0359）
  type: term
  source_chapter: 首现 p17；启用/设码/改码/删除全流程 p51-52
  author_definition: |
    "在默认设定情况下,禁用安全代码" (p51)。启用：按住 "PARA、MASTER和CUSTOM PAINT按钮的同时打开控制面板"，
    输入 "0359" 进入 Engineer Protection 画面，按 [Code Enable] (p51)。
    设码：Security > [Code Change]，任意 "1-8 位数"，二次确认 (p51)。
    设码后 "需要输入安全代码才能切换至工程师模式" (p51)。
    遗失时：从同一隐藏入口按 [Code Enable]（关闭保护）或 [Code Delete]（删除代码） (p52)。
  key_distinction: |
    0359 不是日常密码，而是启用保护/恢复的万能入口 — 知道 0359 的人可以删除任意自定义代码 (p52)；
    手册未讨论此风险（BOOK_OVERVIEW 批判项）。
  why_it_matters: |
    工程师模式的锁；设备交接/回收时必须核查代码状态，否则 File/Maintenance 全线不可用。
  tags: [term, core-concept]

- id: g11
  term: 安全限制（Page Permission / Item Permission）
  type: term
  source_chapter: 首现 p16；Security 画面 p17；设定项 p20；Config 对照 p49
  author_definition: |
    "您可以限制本机可控制的功能,防止在操作过程中误操作" (p20)。
    Page Permission：[Full Lock] "禁止控制面板的所有操作"；[View Mode] "禁止控制面板的所有操作 (查看数据除外)"；
    [Full Paint] 使 Category Select 显示 [Paint] 按钮、"所有 [Paint] 菜单都变为可用" (p20)。
    Item Permission（七项开关）：APR Enable / Ref File Enable / Lens File Enable / OHB File Enable /
    Crop Enable / Knee Max Enable / SW Menu Enable，各自"允许通过控制面板进行...设定" (p20)。
  key_distinction: |
    ≠ 安全代码 — 代码保护的是"进入工程师模式"这道门；Page/Item Permission 是门后的细粒度功能开关；
    二者同在 Security 画面 (p17)，也对应 Config > Security 菜单 (p49)。
  why_it_matters: |
    演播现场防误触的配置清单；Ref/Lens/OHB 文件、Knee Max、Switch 菜单"消失"多因 Item Permission 未开。
  tags: [term]

- id: g12
  term: Tally（计数 / 播出指示信号）
  type: term
  source_chapter: 首现 p14（计数显示窗口，中文以"计数"表述）；亮度设定 p24；Extend Call p48；EXT I/O p56
  author_definition: |
    摄像机编号/计数显示窗口："有红色计数信号发送到摄像机时,则显示黑色数字,数字背景亮为红色。
    有绿色计数信号...背景亮为绿色。有第三个计数信号...背景亮为橙色。
    有多个计数信号发送到摄像机时,则背景会拆分为相应的单个颜色" (p14)。
    EXT I/O 的 TALLY 输入 "可在 LEGACY 模式或 BRIDGE 模式中使用。但在 MCS 模式中会被禁用" (p56)。
    Extend Call："接收到呼叫后, TALLY指示灯会持续闪烁片刻"，时长与条件可设 (p48)。
  key_distinction: |
    ≠ 单一"直播中"红灯 — 本机语境是红/绿/橙三路计数信号 + CALL 呼叫闪烁的综合指示；
    MCS 模式下 EXT I/O 的 Tally 物理输入被禁用（走 CCU）。
  why_it_matters: |
    VD 判断哪台机在播出的依据；LED 亮度设定中 Tally 独立一档 (p24)。
  tags: [term]

- id: g13
  term: 场景文件（Scene File）
  type: term
  source_chapter: 首现 p11（场景文件控制模块）；Scene 菜单 p52；File 菜单 p38
  author_definition: |
    "这些按钮用于注册和读取场景文件" (p11)；面板 1-5 号直读，"使用此按钮 (EXPAND) 可显示最多 32 个场景文件" (p11)；
    "场景文件中存储的项目视所连接的摄像机而异" (p11)；
    存储流程：按 STORE 使其闪烁 → 按编号按钮；读取时按编号按钮 (p11)。
    Scene 菜单可设 Dissolve（读取时图像渐变切换）及 Dissolve Speed (p52)；
    File > Scene Store/Recall/Transfer 支持 CAM↔USB 传输与 File ID/Delete (p38)。
  key_distinction: |
    ≠ RCP 自身设定备份 — USB Backup 的 [RCP Config] 是"RCP 自定义设定,不包括网络设定" (p25)，
      场景文件存在摄像机侧、经 File 菜单传输
    ≠ 无副作用 — "当读取场景文件时" ABSOLUTE 自动退回相对值模式 (p13)
  why_it_matters: |
    多机位风格统一的核心资产；存/取流程与"未保存退出即丢失"是高频坑（对应 task-07）。
  tags: [term, core-concept]

- id: g14
  term: 参考文件（Reference File）
  type: term
  source_chapter: 首现 p17；File 菜单 p38；开关 p20；用途 p46
  author_definition: |
    "Ref Store 记录参考文件" (p38)；Ref Transfer 支持 CAM↔USB 与 File ID (p38)；
    需要 Item Permission 的 [Ref File Enable] 才能"允许通过控制面板进行参考文件设定" (p20)；
    用途：Camera Mode > White Setup Mode > Auto Level "恢复参考文件值" (p46)。
  key_distinction: |
    ≠ 场景文件 — 参考文件是自动设定 (Auto Level) 回退时使用的基准值；
      场景文件是整套画质套装；二者都可 CAM↔USB 传输但入口与用途不同。
  why_it_matters: |
    白平衡自动设定的基准逻辑；菜单里看不到 Ref 项时先查 Ref File Enable (p20)。
  tags: [term]

- id: g15
  term: 镜头文件（Lens File）
  type: term
  source_chapter: 首现 p20（Lens File Enable）；File 菜单 p38
  author_definition: |
    "Lens Store 记录镜头文件"；"Change Name 更改镜头名称"；"Select File 选择镜头文件"；
    "Auto White 调节自动白平衡" (p38)；需要 [Lens File Enable] (p20)。
  key_distinction: |
    ≠ 场景/OHB 文件 — 按镜头个体保存的补偿数据；换镜头后选择对应镜头文件，而非重调参数。
  why_it_matters: |
    换镜头作业流程的一环；与 Shading/Flare 类镜头相关补偿数据配套使用。
  tags: [term]

- id: g16
  term: OHB（光学头模块文件 / OHB Matrix）
  type: term
  source_chapter: 首现 p20（OHB File Enable）；File 菜单 p38；规则 p40-41
  author_definition: |
    File > OHB："OHB Store 记录 OHB 文件"，其下可调节/保存 Auto B Shading、Auto W Shading、
    Black Shading、White Shading、Black Set、OHB Matrix (p38)。
    "OHB Matrix 吸收因光学头模块 (光学单元)而引起的色彩还原变化" (p41)。
    关键规则："如果 2D Black Shading 未保存到 OHB 文件,则在摄像机断电时不会进行保存" (p40；
    3D White Shading 同，p40)。
  key_distinction: |
    ≠ 普通菜单调节值 — Shading 类校正的落盘载体就是 OHB 文件，"断电不保存除非存入 OHB 文件"
    ≠ 镜头文件（g15）— 镜头文件按镜头个体；OHB 按光学头模块（光学单元）
  why_it_matters: |
    维护校正后不 Store 到 OHB = 白做；这是手册明示的易失点（task-14 的核心注意事项）。
  tags: [term, core-concept]

- id: g17
  term: RPN（画面白点手动校正）
  type: term
  source_chapter: 首现 p44（Maintenance 表）；专节 p45
  author_definition: |
    "选择 Maintenance 菜单中的 [RPN], 可以手动校正画面上出现的白点" (p45)。
    成因："宇宙射线和其他噪声可能影响 CCD 图像传感器的像素, 导致显示屏上出现小白点。
    这是图像传感器的物理特性,并非故障"；"执行自动黑平衡调节可激活校正功能,可能会减少这种现象的影响" (p45)。
    流程：R/G/B 选通道 → [H/V Cursor] 开十字光标（显示在"连接到CCU 的 PIX 监视器上"）→ 旋转调节旋钮移动光标
    → [Enter] → [Save]；[Delete] 删除之前的值 (p45)。
  key_distinction: |
    ≠ 坏点报修 — 手册明示"并非故障"，属可自行校正的传感器特性；RPN 全称手册未给出（Sony 私有功能名）。
  why_it_matters: |
    白点投诉的处置路径；依赖 PIX 监视器配合，且与 ABB 的自动校正功能互补。
  tags: [term]

- id: g18
  term: ATW / AWB / ABB（自动追踪白平衡 / 自动白平衡 / 自动黑平衡）
  type: term
  source_chapter: 首现 p11（AWB/ABB 按钮）；定义 p28-29；ATW Setting p41
  author_definition: |
    ATW = "Auto Tracing White Balance功能。此功能可持续校正白平衡以便与拍摄期间的画面相匹配。
    根据所用模式,可能会发生错误" (p28)；ATW Setting 可设 Speed（收敛速度） (p41)。
    AWB = "Auto White Balance 功能。在拍摄白色物体时按下此按钮,将会自动校正色温,
    以便正确显示物体的白色区域" (p28)。
    ABB = "Auto Black Balance 功能。此功能可以自动调节 R 黑色和 B 黑色,确保在镜头闭合时不会有色彩添加到黑色中。
    根据摄像机型号,也会同时调节 Black Set。当执行此操作时,镜头会暂时闭合" (p29)。
    按钮行为：运行中指示灯亮，完成后熄灭；"在调节进行期间再次按此按钮将停止自动调节" (p11)。
  key_distinction: |
    ATW 是持续跟踪（手册提示"可能会发生错误"），AWB/ABB 是一次性触发；
    ABB 需要镜头闭合；三者的统一物理入口是 AUTO SETUP 模块（含 SKIN DTL AUTO HUE / LEVEL，p10-11）。
  why_it_matters: |
    每日/每场景必做（task-04）；Camera Mode > White Setup Mode 决定自动设定后恢复
    "上次获取的自动白平衡值 (AWB)" 还是 "参考文件值 (Auto Level)" (p46)。
  tags: [term, core-concept]

- id: g19
  term: Skin DTL（肤色细节；含 Auto Hue / Gate）
  type: term
  source_chapter: 首现 p10（SKIN DETAIL 按钮 / SKIN DTL AUTO HUE）；定义 p31-32
  author_definition: |
    "支持进行设定色彩区域的轮廓校正电平调节。例如,可以使拍摄的人的面部表现的比较光洁" (p31)。
    "允许最多单独调节三个通道" (p31)；每通道：Level（"使用 Phase 或 Width 设定的色彩区域内的轮廓校正值"）、
    Phase（"调节 Skin DTL 的有效色彩区域的色调中心。此值几乎等同于矢量范围的相位"）、
    Width（"设定以相位为中心的范围"）、Saturation（低饱和区禁用/启用）；
    Auto Hue = "此功能可自动搜索色调。捕捉画面中心您想要测量的物体并执行此功能。自动调节此通道的相位" (p31)；
    Gate = "将区域显示信号添加到 Skin DTL 功能有效的通道范围内" (p31)；
    另有 Natural Skin DTL（三通道通用）、Zoom Link（随变焦改变校正量）、Y Limit（低照度禁用的 Y 等级上限）。
  key_distinction: |
    ≠ 全画面 Detail — 只作用于 Phase/Width 圈定的色彩区域；
    AUTO SETUP 模块的 "SKIN DTL AUTO HUE:将肤色细节自动设为有效色调" (p10) 即自动取色入口；
    Gate 显示与多矩阵 Gate 共用面板 GATE 按钮的区域显示机制 (p10)。
  why_it_matters: |
    人像/肤色核心调整；AUTO HUE 需"捕捉画面中心"目标物体配合（task-04 的前置条件）。
  tags: [term, core-concept]

- id: g20
  term: Matrix（User / Preset / Multi / Adaptive Matrix）
  type: term
  source_chapter: 首现 p22（菜单分配表）；定义 p32-33；OHB Matrix 另见 g16
  author_definition: |
    "在不改变白平衡的情况下校正色彩还原" (p32)。
    User Matrix："单独设定矩阵校正系数"——R-G/G-B/B-R 与 R-B/G-R/B-G 六个系数，分两页 (p32)。
    Multi Matrix："更改分割为 16 份的每个色调的色彩还原"，经 Phase（选色调）/ Hue / Saturation 调节，
    辅以 All Clear 与 Gate（区域显示） (p32-33)。
    Preset Matrix："预先选择摄像机提供的矩阵" (p33)。
    Adaptive Matrix："启用 Adaptive Matrix 功能。此功能对控制所有矩阵功能是通用的"，
    其 Level 用于"调节 Adaptive Matrix 功能的有效条件"（Gain/Total Gain/F Drop Gain/Step Gain/M White，p33）。
  key_distinction: |
    ≠ 白平衡 (White) — Matrix 校正色彩还原"在不改变白平衡的情况下"进行；
    各矩阵（User/Preset/Multi 及 OHB/SD 矩阵）可独立开关，选项卡左侧 ON 标记指示生效者。
  why_it_matters: |
    调色/匹配机位的手段；Multi Matrix 的 Phase+Hue/Saturation 是逐色调精调的入口。
  tags: [term]

- id: g21
  term: Gamma Table（Standard / Hyper / Special / User）
  type: term
  source_chapter: 首现 p23（菜单分配表）；定义 p35；基础 Gamma 定义 p33
  author_definition: |
    "允许选择用于伽马校正的曲线" (p35)。
    Standard："使用标准伽马曲线"；Hyper："使用伽马功能彻底还原摄像机的动态范围 (包括高亮度部分)"；
    Special："允许选择模仿电影的伽马以及其他伽马"；User："允许选择使用 CVP File Editor 创建的伽马以及其他伽马"；
    每种类型内均有 Gamma OFF（"禁用伽马校正"）。
    基础定义："Gamma 将图像拾取设备的光电转换特性校正为显示器的亮度特性" (p33)。
  key_distinction: |
    ≠ Paint > Gamma 微调 — Gamma Table 换整条曲线（风格/交付基准），Gamma 菜单（Gamma R/G/B、Master、Step Gamma）
      在选定曲线上做电平微调；User 曲线需经 CVP File Editor 制作并经 USB 传入 (p35/p38)。
  why_it_matters: |
    风格与交付标准（标准/宽动态/电影感/自定义）的起点设置；Hyper 类选择影响高光与 Knee 的配合预期。
  tags: [term]

- id: g22
  term: Knee（拐点：Knee Point/Slope、Auto Knee、Soft Knee、Knee Apt、Knee Max）
  type: term
  source_chapter: 首现 p20（Knee Max Enable）；Knee Apt p29；定义 p33
  author_definition: |
    "压缩画面明亮部分以启用信号标准范围内的表现。这可使您获得具有高动态范围的图片" (p33)。
    Knee Point "压缩明亮部分并调节开始电平"；Knee Slope "调节压缩图像的比例"。
    Auto Knee："根据捕捉到的图像信号自动调节拐点系数。...忽略为 Knee Point/Slope 配置的设定"，
    辅以 Point Limit（自动调节的下限）与 Auto Slope (p33)。
    Soft Knee："将拐点附近的折线改为曲线"，Radius 调曲率 (p33)。
    Knee Apt："调节应用了拐点功能的高亮度部分的分辨率灵敏度" (p29)。
    Knee Max："在应用了拐点校正的时刻应用削波,以便易于拐点调节。仅当在工程师模式下或当启用
    Knee Max Enable 功能时才能设定此项" (p33)。
    "OFF 禁用拐点校正。 Auto Knee 也会被禁用" (p33)。
  key_distinction: |
    ≠ White Clip — Knee 是压缩（保留高光层次），White Clip 是削波（硬限制到最大值）(p33/p34)
    ≠ 手动参数仍有效 — Auto Knee ON 时"忽略为 Knee Point/Slope 配置的设定"
  why_it_matters: |
    高光处理的基础；HDR Conversion 的 Highlight Cre. 本质是"恢复应用了拐点的区域" (p36)；
    Knee Max 受工程师模式/Item Permission 双重门控。
  tags: [term, core-concept]

- id: g23
  term: Black Shading / White Shading（黑/白色差校正；H·V SAW/PARA）
  type: term
  source_chapter: 首现 p38（File 菜单）；定义 p40-41
  author_definition: |
    "Black Shading 校正图像的黑色色差"；"White Shading 校正图像的灵敏度色差" (p40)。
    按 R/G/B 三通道，各有："Auto B/W Shading...可自动调节每项 RGB、 HV 和 SAW/PARA参数"；
    H SAW "校正...左右方向的光斑 (直线形式)"；H PARA "水平方向光斑 (抛物线形式)"；
    V SAW / V PARA 为上下方向的直线/抛物线光斑 (p40-41)。
    落盘规则："如果 2D Black Shading 未保存到 OHB 文件,则在摄像机断电时不会进行保存" (p40；3D White Shading 同)。
  key_distinction: |
    ≠ Black Set（g24）— Shading 校正画面空间分布上的斑渍（SAW=直线形、PARA=抛物线形），
      Black Set 处理的是黑电平随增益的漂移；两者都在 Maintenance > Camera 下但语义不同层。
  why_it_matters: |
    周期性维护核心（task-14）；自动校正（Auto B/W Shading）后必须 Store 到 OHB 文件，否则断电即失。
  tags: [term]

- id: g24
  term: Black Set（黑色设定）
  type: term
  source_chapter: 首现 p38（File > OHB 下）；定义 p41
  author_definition: |
    "执行相应调节,使得当主增益改变时,各色彩的黑色电平不会改变" (p41)。
    Black Set R/G/B 分通道调节；"ABB...根据摄像机型号,也会同时调节 Black Set" (p41；p29 同)。
  key_distinction: |
    ≠ Black（黑平衡）— Black 调当前增益下的黑电平值；Black Set 保证增益切换时黑电平不漂移；
    ≠ Black Shading（g23）— Black Set 是电平漂移补偿，Shading 是空间性黑斑校正。
  why_it_matters: |
    多增益拍摄（会场明暗切换等）黑电平一致性的关键；常被误当成"黑平衡没调好"而重复执行 ABB。
  tags: [term]

- id: g25
  term: F Drop（F Drop Comp / F Drop Gain / Drop Point / Roundness）
  type: term
  source_chapter: 首现 p14（F DROP 指示灯）；定义 p42；Total Gain 联动 p33
  author_definition: |
    "F Drop Comp 自动调节增益以补偿因镜头 F drop 而导致的亮度降低" (p42)；
    F Drop Gain "用于补偿镜头 F drop 的增益值 (仅显示)"；Max Gain "当镜头光圈全开且在长焦端变焦时调节增益"；
    Drop Point "镜头光圈全开时, F drop 特性的近似折线中断点的位置。此位置与发生 F drop 时的变焦位置大致对应"；
    Roundness "F drop 特性可通过折线大致表示。但是,根据镜头,此折线不是一条完美的折线,在断点 (平滑插入)附近
    有一定的圆度。...值越大,折线的两条直线之间就越平滑。值为 0 表示完美的折线" (p42)。
    面板指示："F DROP:外围亮度降低时亮起" (p14)；
    灵敏度联动："摄像机的灵敏度根据主增益、主白色增益和 F drop增益的总量而定"（Total Gain，p33）。
  key_distinction: |
    ≠ 镜头故障 — 是变焦/全开光圈下的自然边缘减光，由增益自动补偿；
    Roundness=0 表示理想折线模型；F Drop Gain 只显示不可直接调（经 Max Gain/Drop Point/Roundness 间接成型）。
  why_it_matters: |
    换镜头后的校正项目（Maintenance > Lens）；估算 Total Gain/噪声水平时须计入 F Drop Gain。
  tags: [term]

- id: g26
  term: ALAC / V Mod Saw（镜头像差校正）
  type: term
  source_chapter: V Mod Saw 首现 p23（菜单分配表）、定义 p34/p42；ALAC 定义 p42
  author_definition: |
    ALAC = "镜头自动彩色误差补偿 (Auto Lens Aberration Compensation) 功能。此功能可在使用兼容的镜头时
    自动降低色差或进行放大。当此功能停止或未连接兼容的镜头时,画面上会显示 'Stop'" (p42)。
    V Mod Saw = "校正因镜头或光学系统引起的垂直方向色差" (p34/p42)，R/G/B 可调，
    Master 链动时 "R、 B 和 G 沿着反方向移动"。
    关联：D.shade Comp "根据镜头的状态自动校正 V Mod Shading。仅在使用可兼容的镜头时才能执行此操作" (p42)。
  key_distinction: |
    ALAC 是全自动（需兼容镜头，失效显示 "Stop"）；V Mod Saw 是手动参数校正；
    二者同属 Maintenance > Lens 的镜头像差项目，但一自动一手动，排查路径不同。
  why_it_matters: |
    边缘紫边/垂直色差的处置入口；看到 "Stop" 先查镜头兼容性而非反复开关。
  tags: [term]

- id: g27
  term: 快门模式（SLS / SHT / ECS；DEG 指示灯）
  type: term
  source_chapter: 首现 p12（快门控制模块）；Shutter 菜单定义 p34
  author_definition: |
    指示灯 "对应于所选功能的指示灯亮起。从菜单中选择功能。SLS:慢速快门模式 SHT:快门模式
    ECS:ECS (扩展清晰扫描)模式" (p12)。
    "DEG 指示灯：当快门显示为角度值时, 此指示灯亮起" (p12)。
    Paint > Shutter：Slow Shutter "以捕捉图像格式的帧频的频率拍摄 (单位:帧数)"；
    Shutter "逐渐控制曝光时间。显示为 1/x 秒"；Angle 将快门速度显示为角度值；
    "ECS 这是 Extended Clear Scan功能。可精细控制曝光时间 (单位:Hz)" (p34)。
    FPS 用于快速和慢速拍摄，Comp（OFF/Angle/Gain）"校正更改 FPS 时的图像电平的变化" (p34)。
  key_distinction: |
    ≠ 帧率 (FPS) — SLS/SHT/ECS 都是单帧曝光时间控制；四种单位各异（帧数 / 1/x 秒 / Hz / 角度）；
    DEG 灯决定显示窗口读角度值还是速度值。
  why_it_matters: |
    演播室消 flicker、匹配显示设备的手段；快门档位与单位切换是 Paint > Shutter 的开关设定 (p12)。
  tags: [term]

- id: g28
  term: GenLock（同步；GenLock Mode 与 CCU Phase）
  type: term
  source_chapter: CCU Phase p43；GenLock Mode p46
  author_definition: |
    "GenLock Mode 使用同步功能选择信号类型。HD 这是 HD3 值 SYNC。SD 这是 BBS" (p46)。
    配套：Maintenance > CCU > Phase："如果有同步信号输入 CCU,此功能允许设定与该信号相关的相位"——
    H / H Step / H Coarse 调 H 相位，SC 调子载波，"SC Phase 调节 VBS 子载波的相位" (p43)。
  key_distinction: |
    ≠ 网络时钟 — 是视频系统的共相位；调整对象在 CCU 侧（面板只是遥控入口）；
    SC Phase 仅在涉及 VBS（模拟复合）输出时相关。
  why_it_matters: |
    多机位切换画面无跳动的前提；切换画面"滚动/闪跳"先查 GenLock 与 Phase。
  tags: [term]

- id: g29
  term: Return Settings（CCU 返回输入设定）
  type: term
  source_chapter: 首现 p46（Config 菜单表）；设定步骤 p50
  author_definition: |
    "在 CCU 的 Config 菜单中选择 [Return Settings],设定 CCU 的返回信号的格式。
    这只能在工程师模式中设定" (p50)。
    Return-1 到 Return-4 四路；第 1 页 [Input] 指定输入信号；
    第 2 页 [Aspect]（"仅在...指定了 SD 信号时,才能设定此项"）、[LB Mode]（"指定宽银幕的显示模式"）、
    [OETF]（"只能为支持HDR 的CCU 设定此项"）、[C Space]（同） (p50)。
  key_distinction: |
    ≠ 返送选路 — 这里设定的是返送信号的"格式"（信号类型/纵横比/OETF/色彩空间），不是路由给谁；
    OETF 与 C Space 是 HDR 相关项，只对支持 HDR 的 CCU 生效。
  why_it_matters: |
    取景器/监视器返送显示异常（比例不对、灰调不对）的排查点；HDR 制作中与 HDR Conversion 配套。
  tags: [term]

- id: g30
  term: PIX/WF（PIX/WF 输出与 PIX/WF Synchro）
  type: term
  source_chapter: 首现 p48（RCP Mode > PIX/WF）；Synchro 细节 p50；Function 菜单 p53
  author_definition: |
    "PIX (R/G/B/ENC) 选择 CCU 的 PIX2 的 OUTPUT 输出信号。R/G/B:输出 R、 G 和 B 信号中的一个信号
    (或者多个信号的组合)。ENC:输出编码信号"；"WF (R/G/B/SEQ/ENC) 选择 CCU 的 WF2 的 OUTPUT 输出信号...
    SEQ:按顺序模式监视三个信号 R、 G 和 B 的波形" (p53)。
    PIX/WF Synchro："在调节了Black Shading 和 White Shading 之后,将菜单中的RGB选择和PIX/WF 控制相关联
    (ON 时已链接)" (p48)；OFF 时用 "PICTURE MONITOR 或 WAVEFORM MONITOR按钮...输出...选定的信号" (p50)。
  key_distinction: |
    ≠ 返送 (Return) — PIX/WF 是调机用的图像/波形监视输出口（PIX=画面监视、WF=波形监视，据 p50 按钮名）；
    Synchro 决定该输出是否跟随面板菜单里的 RGB 选择。
  why_it_matters: |
    Shading 校正（g23）与 RPN 白点校正（g17）都依赖 PIX 监视器；看波形调机的信号源选择入口。
  tags: [term]

- id: g31
  term: Live Tone Control（实时色调控制）
  type: term
  source_chapter: p36-37（Live Tone Control 1 / 2）
  author_definition: |
    "配置实时色调控制的设定" (p36)。Live Tone Control 1：Base/Low/Mid Tone 开关；
    Curve "调节基本色调调节曲线的曲率。值越大,曲率越大"；
    Low/Mid Tone 的 Width "设定...区域宽度。值越大,亮度范围越宽"；
    Mid Tone 的 Center "设定中等亮度色调调节中心的亮度。值越大,范围越明亮"；
    各 Tone 的 Master "设定...强度。应用于 R、 G 和 B" (p36-37)。
    Live Tone Control 2："可以单独设定 R、 G 和 B" 的强度 (p37)。
  key_distinction: |
    ≠ Gamma / Black Gamma — 按亮度区（低/中/基调）的实时色调塑形，不替换伽马曲线；
    第 1 页（Master 联动 R/G/B）与第 2 页（分通道）同时配置时效果会叠加。
  why_it_matters: |
    快速氛围调整（如压暗部色调）的专用通道；分页语义易混，是 Paint 菜单新功能项。
  tags: [term]

- id: g32
  term: HDR Conversion（SDR→HDR 转换；含 HDR Operation）
  type: term
  source_chapter: p36（HDR Operation / HDR Conversion）
  author_definition: |
    "用于从 SDR 转换为 HDR 的调节项目" (p36)。
    Highlight Cre. = "高亮创建 (恢复应用了拐点的区域)功能"，辅以 Point/Slope（"调节 SDR 图像的拐点/拐点斜率"）；
    Black：经 Input Lvl Adjust 设 Input / SDR Output / HDR Output 各黑色电平；
    White/Gain：White Balance / Gain R/G/B、M.White (p36)。
    同页 HDR Operation：Black Offset（"在 Live HDR 中,仅调节 HDR 图像的黑色偏移"）、
    SDR Gain（"仅调节 (降低) SDR 图像的增益"）、HDR Contrast（"源于 SDR Gain 的 HDR 对比度值 (仅限显示)"）、
    HDR Knee（Knee Point/Slope）、HDR White Clip、HD Detail Reduction (p36)。
  key_distinction: |
    ≠ 拍摄端 HDR 伽马（Gamma Table）— 这是把 SDR 信号"转换/提升"为 HDR 的调节组；
    Highlight Cre. 的本质是找回被 Knee 压掉的高光；HDR Contrast 为仅显示项，实际由 SDR Gain 决定。
  why_it_matters: |
    HDR 制作中兼容 SDR 机位的方案；与 Return Settings 的 OETF/C Space 配套设定。
  tags: [term]

- id: g33
  term: PoE（以太网供电，IEEE802.3af）
  type: term
  source_chapter: 首现 p5（PoE 集线器）；接口 p15；规格 p55；缆长 p16
  author_definition: |
    LAN 接口 "可接收连接到 IEEE802.3af 兼容 PoE 集线器时提供的电源" (p15)；
    规格："PoE 36 V至57 V(兼容IEEE802.3af class 2)"，功耗 10 W（含 AUX 接口输出）(p55)；
    供电拓扑：BRIDGE/MCS/PC 控制示例均经 "PoE 集线器" (p5-7)；
    "使用 LAN 电缆从 PoE 兼容集线器到本机的最大连接长度为 100 m" (p16)。
  key_distinction: |
    ≠ 仅 EXT I/O 供电 — 面板有双供电路径（EXT I/O "10.5 V 至 17 V 直流" / PoE）；
    经非 PoE 集线器接入时需另行安排供电。
  why_it_matters: |
    施工布线决策：是否选 PoE 集线器、供电预算（10 W/台）与 100 m 缆长限制。
  tags: [term]

- id: g34
  term: CCA-5（遥控电缆）
  type: term
  source_chapter: 首现 p4；Legacy 组网 p5；缆长与接地 p16；选购件 p55
  author_definition: |
    "使用 CCA-5 电缆连接摄像机控制单元 (CCU) 和 RCP" (p5)；
    "使用 CCA-5 电缆从 CCU 到本机的最大连接长度为 200 m" (p16)；
    选购件 CCA-5-3/-10/-30（3/10/30 m）(p55)；
    "传统的 CCA-5 电缆" (p4)；
    混合组网规则："当使用 LAN 电缆连接本机,并使用 CCA-5 电缆连接 CCU 时,请设定 MCS 模式" (p19)。
  key_distinction: |
    ≠ 网线 — 专用多芯遥控电缆（LEGACY 模式专用），"TCP/IP 和 RCP 编号无需设定" (p18)；
    200 m 上限是 LAN 连接（100 m）的两倍；
    接地要求仅针对 "只使用 LAN 电缆连接时" (p16) — 纯 CCA-5 连接无强制接地条款。
  why_it_matters: |
    LEGACY 组网的物理前提；缆长与接地规则是安装阶段（task-01/02）的直接依据。
  tags: [term]

- id: g35
  term: ABSOLUTE（绝对值模式 / 相对值模式）
  type: term
  source_chapter: 首现 p13（ABSOLUTE 按钮）；光圈/主黑侧 p14；灵敏度 p24
  author_definition: |
    "此按钮使用绝对值模式 (亮起)和相对值模式 (未亮起)之间的 WHITE、BLACK、FLARE 和 DETAIL旋钮更改手动调节模式。
    在绝对值模式下,旋钮指示值变为设定值。在相对值模式下,旋钮指示角度和设定值不匹配" (p13)。
    七种情况"将自动选择相对值模式"：通电中／面板激活状态改变时／PARA 或主/从模式时／
    自动设定（电平、白色和黑色）完成后／读取场景文件时／按 FLARE 切换调节模式时／
    用 RCP Assign 更改受控 CCU 时 (p13)。
    光圈/主黑侧：IRIS RELATIVE 按钮；相对值模式"调节相对于...初始值的光圈和主黑电平...初始值为 1/4"，
    灵敏度经 VR Setting 更改；绝对值模式"控制杆/旋钮...位置会直接确定...值"，
    用 COARSE（CLOSE 侧下限）与 SENS（OPEN 侧上限）定调节范围 (p14, p24)。
  key_distinction: |
    ≠ 旋钮故障 — 相对值模式下"旋钮指示角度和设定值不匹配"是设计行为；
    换面板/读场景文件/RCP Assign 后旋钮"对不上刻度"即此机制（七条自动退回规则）；
    ≠ IRIS RELATIVE 是独立按钮 — WHITE/BLACK/FLARE/DETAIL 共用 ABSOLUTE，光圈/主黑各有 RELATIVE 开关。
  why_it_matters: |
    手动调节手感的根基；七条自动退回场景是手动白黑平衡调节（task-06）的记忆重点。
  tags: [term, core-concept]
```

### 覆盖自检（RCP 侧，随单书保留）

- [x] `author_definition` 均为手册原文压缩片段（带页码）
- [x] `key_distinction` 标注与"常识用法/易混概念"的差异（设备手册语境 = 易混功能对：PANEL ACTIVE vs PARA vs IRIS/MB ACTIVE、控制许可 vs 安全限制、场景/参考/镜头/OHB 四种文件、Knee vs White Clip、Black vs Black Set vs Black Shading、PIX/WF vs Return）
- [x] 任务必收 37 项全部收录：CNS 四模式(g01)、CCU(g02)、MSU+CNA-1(g03)、RCP Assign(g04)、PANEL ACTIVE(g05)、PARA(g06)、IRIS/MB ACTIVE(g07)、控制许可(g08)、工程师模式(g09)、安全代码(g10)、Tally(g12)、场景文件(g13)、参考文件(g14)、镜头文件(g15)、OHB(g16)、RPN(g17)、ATW/AWB/ABB(g18)、Skin DTL 含 Auto Hue/Gate(g19)、四种 Matrix(g20)、四种 Gamma Table(g21)、Knee 家族(g22)、Black/White Shading(g23)、Black Set(g24)、F Drop 全参数(g25)、ALAC+V Mod Saw(g26)、ECS/SLS/SHT+DEG(g27)、GenLock(g28)、Return Settings(g29)、PIX/WF(g30)、Live Tone Control(g31)、HDR Conversion(g32)、PoE(g33)、CCA-5(g34)、ABSOLUTE(g35)，另收安全限制 Page/Item Permission(g11)
- [x] 单元数 35（任务预期 20–35；家族式术语按任务示例方式合并：ATW/AWB/ABB、ECS/SLS/SHT、Knee 家族、Matrix 家族、ALAC/V Mod Saw、MSU/CNA-1）
- [x] 缩写均给全称；手册未展开全称者（CNS、RPN）已如实注明，未杜撰
- [x] 取材路径：全量扫描通读全书（extractor v2.2 回退条款），引文已回原文核验

---

# B 部分 · 摄像机控制单元 HDCU5000 / HDCU5500 / HDCU3500（93 条，编号 `h01`–`h93`）

> 本部分逐字取自 CCU 单书术语表，**仅把编号前缀 `g` 改为 `h`**（`hNN` ≡ CCU 单书 `gNN`），条目文字未改动。按 10 个术语域分组，末附待复核术语。

---

## 1. 连接与传输

| 术语 (h) | 手册定义 | 与常识用法的差异 |
|---|---|---|
| **CABLE TYPE** (h01) | 指定用于连接摄像机的电缆类型；取值 `FIBER CAMERA CABLE`、`COAX`、`COAX(HDCE)`、`SINGLE-MODE FIBER`。`SINGLE-MODE FIBER` 仅当已安装 HKCU-SM50 时可选。 | ≠ 物理线缆型号/规格——它是四选一的**系统模式开关**，决定 FIBER TRANSMIT RATE 是否可选（选 COAX/COAX(HDCE) 时该速率固定显示 `---`），并派生后续全部格式。 |
| **FIBER TRANSMIT RATE** (h02) | 设置连接光纤电缆时的传输速率；取值 `HIGH`、`ULTRA`、`---`。HIGH＝连 HDC3500（未装 HKC-FB50）/HDC3100/HDC2000 系列；ULTRA＝连 HDC5000/5500 或装 HKC-FB50 的 HDC3500；`---`＝CABLE TYPE 为 COAX/COAX(HDCE) 时。 | ≠ 以太网/光纤链路速率（如 10G/25G）——HIGH/ULTRA 是 Sony **私有光纤分级**，决定 CAMERA FORMAT 合法取值集合，并在 ULTRA 下把 NETWORK TRUNK 锁定为 NETWORK+VIDEO。 |
| **CAMERA FIBER 接口** (h03) | 用于通过光纤电缆连接摄像机；所有摄像机信号（含电源、控制、视频、音频）经一根光纤收发。不连接时须用附带盖子盖住接口端。HDCU5000 有两个（一个连 HDC5000/5500，另一个连 HDC3500 与 HDC2000 系列）；HDCU5500/3500 各一个。 | ≠ 普通视频输入口——它**同时承载电源/控制/视频/音频**（复合光纤）。CABLE ALARM 灯的 OPEN 态即指"未通过光纤电缆将摄像机连接到本机后面板上的 CAMERA FIBER 接口"。 |
| **LAN-COM 接口** (h04) | 用于连接 LAN；用 LAN 电缆（5 类以上屏蔽型）连接 LAN 集线器（`10BASE-T/100BASE-TX/1000BASE-T`）。RCP/MSU 设备连接与 IP 计数器输入也用它。 | ≠ HKCU-SFP50 的 LAN 1/LAN 2——LAN-COM 是 1G 级控制/管理口。DHCP 的"自动 IP"**仅适用于 LAN COM**；Web 菜单、Ember+、SNMP、TSL UMD、NMOS 均走此口。 |
| **NETWORK TRUNK 接口** (h05) | 后面板 RJ-45 8 芯：用于将连接到摄像机的 NETWORK TRUNK 接口的设备连接到网络连接设备。 | ≠ 本机联网口——它是把"摄像机侧 NETWORK TRUNK 设备"旁路到网络的通道（以太网干线）。**与同名菜单项 M02 是两个概念**。 |
| **NETWORK TRUNK（菜单项 M02）** (h06) | 设置网络总线的模式；取值 `OFF`、`NETWORK`、`NETWORK+VIDEO`。NETWORK＝网络干线（最大 1 Gbps）；NETWORK+VIDEO＝在用高清干线/HD 提示器时用网络干线（最大 100 Mbps）。当 FIBER TRANSMIT RATE 设为 ULTRA 时**固定为 NETWORK+VIDEO**。 | ≠ 接口名——同名但指菜单项；且其取值受 FIBER TRANSMIT RATE 约束（ULTRA 下不可自由选）。 |
| **TRUNK 接口** (h07) | 后面板圆形 12 芯：用于通过 RS-232C 或 RS-422A 接口连接摄像机上的 CCU 接口，最多可与 2 个频道通信。M01：CHANNEL MODE `2CH(MAX 75Kbps)`/`1CH(MAX 150Kbps)`，INTERFACE `232C`/`422A`。 | ≠ 网络干线——这是**串行低速数据干线**，与 NETWORK TRUNK（以太网）是两条独立通路；也与 HD/UHD TRUNK（视频干线）不同。 |
| **RCP/CNU 接口** (h08) | 后面板圆形 8 芯：通过 CCA-5 连接电缆连接 MSU-1000 系列主设置装置、CNU-700 摄像机指令网络装置或 RCP-3000/1000 系列遥控面板，收发控制信号；用 RCP-3000/1000 系列时还提供电源。 | ≠ LAN 口——控制信号走 CCA-5 专线（8 芯），且对 RCP 供电（故有 RCP POWER 状态项、前面板 RCP/MSU 状态灯）。 |
| **CAMERA SMF IN / CAMERA SMF OUT** (h09) | 单模光纤接口。IN 输入视频（来自摄像机）、音频（麦克风）、HD-TRUNK、NETWORK TRUNK 信号；OUT 输出返回视频（至摄像机）、提示机视频、节目音频、NETWORK TRUNK 信号，还支持 RS-422A/RS-232C。规格：适用于单模光纤电缆的 ST 接口 (2)。 | ≠ 普通 CAMERA FIBER——方向被拆成 IN/OUT 两个 ST 接口，且"**只能用于连接 HDC3500/3100 和 HDC2000 系列摄像机。不能连接 HDC5000/5500。**"单模连接还需 HDCE-100 摄像机扩展适配器。 |
| **HD TRUNK / UHD TRUNK** (h62) | 经 SDI 链路承载的"视频干线"。S02：SDI-I/O 3（OUT 时）可选 HD TRUNK；UHD-SDI B 的 SIGNAL 可选 UHD TRUNK（**仅适用于 HDCU5000/5500**）。M02：HD TRUNK DATA RATE `1.5G`/`12G`；UHD TRUNK DATA RATE `1.5G`/`3G`/`6G`/`12G`。 | ≠ 串行 TRUNK 接口 (h07)——HD/UHD TRUNK 是**经 SDI 链路的视频干线**（1.5G/12G），TRUNK 接口是 RS-232C/RS-422A 串行通路。**近义非重复**。 |
| **OPTICAL SIGNAL / OPTICAL SIGNAL BACKUP** (h91) | S01：`ON`/`OFF` 切换从 CCU 输出到摄像机的光学信号（仅在使用光纤复合线缆连接时显示）。M10：OPTICAL SIGNAL BACKUP `ENABLE`/`DISABLE` 设置是否在 <CAMERA I/F> 页保存 OPTICAL SIGNAL 状态以用于下次启动。 | ≠ 光学信号本身——它是"是否向摄像机输出光学信号"的开关，且**默认不记忆**（需 M10 BACKUP 才能跨重启保存）。 |

---

## 2. 格式与信号

| 术语 (h) | 手册定义 | 与常识用法的差异 |
|---|---|---|
| **SYSTEM** (h10) | 选择系统的工作频率；取值 `1.001(525)`、`1.000(625)`。 | ≠ 操作系统/软件版本——它指 59.94（525 行）/50（625 行）两大**场频体系**，决定格式查表翻哪一页。 |
| **CAMERA FORMAT** (h11) | 选择系统格式，可选值视所连摄像机的有效格式而不同。例（ULTRA + 1.001(525)）：`3840×2160/59.94P(2×)`、`3840×2160/59.94P`、`3840×2160/29.97P`、`3840×2160/23.98P`、`1080/59.94P`…；例（HIGH + 1.001(525)）：`UHD/59.94P (4K/HDR)`、`1080/59.94P (4K/HDR)`、`1080/59.94P`… | ≠ CABLE TYPE（电缆类型）——两者极易混：CAMERA FORMAT 是"**信号格式**"，CABLE TYPE 是"**连接模式**"。 |
| **BIT DEPTH** (h12) | 设置 RGB4:4:4 输出位长度并更改 CCU 输出格式；取值 `10BIT`、`12BIT`。仅当 CAMERA FORMAT 设为 `1080/59.94I (RGB444)`、`1080/29.97PsF (RGB444)`、`1080/23.98PsF (RGB444)`、`1080/50I (RGB444)`、`1080/25PsF (RGB444)` 或 `1080/24PsF (RGB444)` 时可选。 | ≠ 通用量化位深——它只在 `(RGB444)` 格式族下出现，是格式派生链的末端开关。 |
| **PsF** † (h13) | 手册**未单独定义**，仅以格式串出现：`1080/29.97PsF`、`1080/23.98PsF`、`1080/25PsF`、`1080/24PsF`、`1080/59.94I(PsF)`、`1080/50I(PsF)`、`525/59.94I(PsF)`、`625/50I(PsF)`、`3840×2160/29.97PsF/SQD/3G-B`。 | ≠ 逐行扫描的"P"——PsF（Progressive segmented Frame）是逐行内容按隔行方式分段传输；手册把它与 I 并列书写（如 `1080/59.94I(PsF)`）。**格式串必须原样保留，不得当 P 处理。** |
| **SQD / 2SI** † (h14) | 手册**未展开定义**，以格式串出现：`3840×2160/59.94P/SQD/3G-A`、`3840×2160/59.94P/2SI/3G-A`。V01 2SI DIAMOND MARK：设置 4K 2SI 输出的标记显示，"此功能用于在 4K 双样本交错输出期间在 4K 颜色条右下方区域中显示…测试图案。如果链路 1 到 4 的连接正确,则显示 OK,否则不显示 OK。" | ≠ 图像缩放/分辨率——SQD（Square Division）与 2SI（2 Sample Interleave）是 **4K 四链路（Link-1..4）的像素切分方式**，直接决定线缆/链路编配是否正确。 |
| **3G-A / 3G-B** (h15) | 3G SDI 的两种映射（Level-A/B）。规格：3G SDI＝SMPTE ST424/425 Level-A/B、0.8 Vp-p、75 欧姆、`2.970 Gbps`/`2.967 Gbps`。格式串如 `1080/59.94P/3G-A`、`1080/59.94P/3G-B`、`1080/59.94I(2×)/3G-B/Link1&Link2`。 | ≠ 不同速率——3G-A 与 3G-B **速率相同**，区别在双链路/单链路映射；RGB444 与 `(2×)` 等多链路格式一律强制走 3G-B。 |
| **12G / 6G / 1.5G** (h16) | 单链路 SDI 速率等级。规格：12G SDI＝SMPTE ST2082、`11.88 Gbps`/`11.868 Gbps`；6G SDI＝SMPTE ST2081、`5.940 Gbps`/`5.934 Gbps`；HD SDI＝SMPTE ST292、`1.485 Gbps`/`1.4835 Gbps`（均 0.8 Vp-p、75 欧姆）。格式串如 `3840×2160/59.94P/12G`、`3840×2160/29.97P/6G`。 | ≠ 链路数量——12G/6G/1.5G 是**单链路速率**，与"四链路 3G-A/B（SQD/2SI）"是两种不同的 4K 承载方式。 |
| **HFR** (h17) | 高帧率格式，以 `(2×)`/`(3×)`/`(4×)`/`(6×)`/`(8×)` 后缀出现，如 `1080/59.94P(2×)`、`720/59.94P(8×)`、`1080/59.94I(8×)/12G`。注："HFR 输出 (1080/59.94) 与 SDI-OUT1、SDI-OUT2、SDI-I/O1 和 SDI-I/O2 关联。" | ≠ 普通多链路——HFR 是同一格式的**倍帧率**，被绑定到特定接口组（仅 OUT1/2、I/O1/2），且 720 输出需所连摄像机 HDR 模式设为 OFF。 |
| **RGB444** (h18) | CAMERA FORMAT 中以 `(RGB444)` 标注的格式族（`1080/59.94I (RGB444)`、`1080/29.97PsF (RGB444)`、`1080/50I (RGB444)` 等）；BIT DEPTH 项仅在这些格式下可选。输出格式串如 `1080/59.94I(PsF)/RGB444/3G`。 | ≠ 普通 4:2:2——RGB444 在本手册中**强制走 3G-B**，且是唯一能选 BIT DEPTH（10/12BIT）的格式族；返回格式表中一律标 `(SDR)`，即不支持 HDR。 |
| **CCU VIDEO CONVERT** (h19) | 设置视频转换器功能；取值 `DISABLE`、`ENABLE`。当 CAMERA FORMAT 设置为特定项时须设为 ENABLE；选 ENABLE 时将 FRAME SYNCHRONIZER 设为 ON。提示：设 ENABLE 会引入延迟，可通过提前摄像机信号补偿。 | ≠ 简单开关——它是多项格式/延迟项的**使能前提**（返回与输出格式表多处标注"当 CCU VIDEO CONVERT 设为 ENABLE 时,可以选择 720 输入/输出"）。 |
| **FRAME CONVERT DELAY / HD-SD DELAY** (h20) | FRAME CONVERT DELAY：设置 2-3 下拉的视频延迟时间；取值 `0.8`、`1.2`、`1.6 [F@23.98PsF]`，仅当 SYSTEM 为 1.001(525) 时启用。HD-SD DELAY：设置从 HD 信号降频转换的 SD 信号的延迟；取值 `LINE`、`FRAME`。1080 格式：LINE＝`90H`、FRAME＝`1F`；720 格式：LINE＝`120H`、FRAME＝`2F`。 | ≠ 用户自由填写的延迟量——HD-SD DELAY 选 LINE/FRAME 后延迟被**固定**为 90H/1F 或 120H/2F，不能任意填数；FRAME CONVERT DELAY 单位是 `[F@23.98PsF]` 且仅 525 系统可用。 |

---

## 3. HDR 与色彩

| 术语 (h) | 手册定义 | 与常识用法的差异 |
|---|---|---|
| **LIVE HDR** (h21) | HDR MODE 取值 `OFF`、`LIVE HDR`。OFF＝正常拍摄；LIVE HDR＝用于 LIVE HDR 拍摄。选择 LIVE HDR 时，摄像机绘制功能可用于 HDR 输出和 SDR 输出，"但是, HDR 输出不支持某些绘制功能。" | ≠ "高动态范围"泛称——它是 Sony 的**同步双输出机制**（同一摄像机同时输出 HDR 与 SDR），附带"HDR 输出不支持某些绘制功能"的限制；也是 SDR GAIN / HDR CONTRAST / HDR BLACK OFFSET 三项的使能前提。 |
| **OETF** (h22) | HDR OETF：设置视频输出 OETF；取值 `S-Log3`、`HLG`。各输出（SDI-OUT/SDI-I/O/IP-OUT）OETF：设置视频输出的伽马曲线；取值 `SDR`、`HDR OETF`。UHD-SDI 各口 OETF：取值 `SDR`、`4K OETF`。 | ≠ 仅"伽马曲线"——手册在同一字段名 OETF 下混用"OETF/伽马曲线"两种表述，且**取值集合随接口类型变化**（SDI/IP 为 SDR/HDR OETF，UHD-SDI 为 SDR/4K OETF）。 |
| **HDR LOOK** (h23) | 设置视频输出 LOOK；取值 `Natural`、`Mild`、`Live`。 | ≠ 后期调色 LUT——它是本机 HDR 输出的**观感预设**（三选一）。 |
| **HDR COLOR SPACE** (h24) | 选择视频输出的颜色空间；取值 `BT709`、`BT2020`。 | ≠ 显示器色彩管理——它是输出信号的颜色空间标记；与 4K COLOR SPACE 是**成对但不同**的两项。 |
| **4K COLOR SPACE** (h25) | 选择 4K 视频输出的颜色空间；取值 `BT709`、`BT2020`。当 HDR MODE 设为 LIVE HDR 时，设置与 HDR COLOR SPACE 相同。 | ≠ HDR COLOR SPACE——专管 4K 输出；在 LIVE HDR 下被**强制**与 HDR COLOR SPACE 相同（不独立可调）。 |
| **SDR GAIN** (h26) | 仅在 LIVE HDR 模式下启用；增益设置适用于 SDR 输出；取值 `–15 至 0.0`、`0 dB`。 | ≠ 通用增益——只作用于 LIVE HDR 下的 **SDR 那一路输出**，取值范围为负值到 0 dB；它决定 HDR CONTRAST 的显示值。 |
| **HDR CONTRAST** (h27) | 仅在 LIVE HDR 模式下启用；通过设置 SDR GAIN 维持 HDR 输出对比度（**仅显示**）；取值 `100 至 560%`。 | ≠ 可自由调整的对比度——标注"仅显示"，实际由 SDR GAIN 决定，不是独立可调项。 |
| **HDR BLACK OFFSET** (h28) | 仅在 LIVE HDR 模式下启用；HDR 输出黑色偏移；取值 `–99 至 99`、`0`。 | ≠ 通用黑电平——只作用于 LIVE HDR 下的 **HDR 输出支路**。 |

---

## 4. 同步

| 术语 (h) | 手册定义 | 与常识用法的差异 |
|---|---|---|
| **GENLOCK MODE** (h29) | 设置外部参考信号的锁定模式；取值 `HD`、`SD`、`NETWORK`。仅在安装了 HKCU-SFP50 网络接口板时才会显示 NETWORK。在 SMPTE ST 2110 兼容系统中运行时设置为 NETWORK。设为 NETWORK 时不需要 REFERENCE IN 接口的外部参考输入，且使用 HKCU-SFP50 的 LAN 1/LAN 2 接口进行网络同步。 | ≠ 仅 HD/SD 二选一——第三选项 NETWORK 只在装 SFP50 时出现，且 ST2110 系统**强制**用它并免掉外部 REFERENCE 输入。 |
| **REFERENCE / REFERENCE IN/OUT** (h30) | S04 REFERENCE 为"REFERENCE IN 接口的信号输入（仅显示）"，取值 `NOT DETECTED`、`EXT IN`、`1080/59.94I`、`1080/23.98PsF`、`720/59.94P`、`1080/50I`、`1080/24PsF`、`720/50P`。接口：输入 HD 三电平同步或 SD 参考信号（黑场/带 10 场 ID 的黑场）；REFERENCE OUT 原样输出输入信号（环路），不使用环路输出时须在 75 欧姆端接。规格：HD＝SMPTE ST274、3 电平同步、0.6 Vp-p、75 欧姆。 | ≠ 双向口——OUT 只是 IN 的**环路**（loop-through）原样输出；且 REFERENCE 菜单项是"检测结果（仅显示）"，不是可设的参考源类型。 |
| **10F BB** (h31) | 设置是否使用添加到外部参考信号的 10 场 ID；取值 `OFF`、`ON`。当 GENLOCK MODE 为 SD 且 SYSTEM 为 1.001(525) 时可选。错误消息：`CCU:10FIELD-ID ERROR`——即使 10F BB 设为 On 也未检测到 10 场 ID。 | ≠ 黑场信号本身——它是 NTSC 10F-BB（带 10 场 ID 的黑场）中"场 ID"的**使用开关**，仅在 SD 模式 + 525 系统下可选。 |
| **LOCK STATUS** (h32) | S04（GENLOCK 选 HD/SD 时）：`LOCKED`、`NOT LOCKED`（外部参考信号锁定状态，仅显示）。N04（PTP）：`NOT IN USE`、`NO MASTER`、`LOCKING`、`LOCKED`。 | ≠ 一套取值——同名项在 GENLOCK（HD/SD）与 NETWORK GENLOCK（PTP）两处**取值体系完全不同**，不能混用。 |
| **H-PHASE STEP / H-PHASE COARSE / V-PHASE** (h33) | H-PHASE STEP：GENLOCK HD 时 `–3.01 至 3.45 微秒`、SD 时 `–8.29 至 9.48 微秒`（默认 0.00），调整与参考信号（步长）有关的水平锁定相位。H-PHASE COARSE：`–99 至 99`、`0`（精细调整）。V-PHASE：`0 至 7`（垂直锁定相位，行）。 | ≠ 普通相位旋钮——H-PHASE STEP 范围**随 GENLOCK MODE 变化**，单位为微秒；且手册把"步长"命名为 STEP、把"精细调整"命名为 COARSE（**命名与直觉相反**）。 |
| **SYNC OUT SELECT** (h34) | 设置 REFERENCE OUT 接口的输出信号；取值 `SD SYNC`、`HD SYNC`。 | ≠ 输入参考——它管的是 REFERENCE OUT（环路输出口）的输出类型；本机可作参考源向下游输出。 |
| **NETWORK GENLOCK / PROFILE ST2059-2** (h35) | NETWORK GENLOCK：`DISABLE`/`ENABLE` 启用/禁用网络同步锁定。PROFILE：仅支持 ST2059-2 配置文件。DOMAIN NUMBER：`0 至 127`、`127`（设为要连接的主站设备的域编号）。COMMUNICATION MODE：`MULTICAST MODE`/`MIXED MODE`（MIXED＝单播回复主站）。DELAY REQUEST INTERVAL：`–7 至 –1`、`–3`。 | ≠ 通用 NTP/网络校时——它是 **IEEE 1588 PTP 且只支持 SMPTE ST2059-2 配置文件**，需要 HKCU-SFP50；域号/通信模式必须与主站一致。 |
| **PTP STATUS / STEP** (h36) | N05 显示：PTP NIC `LAN1`/`LAN2`；STATUS `NO MASTER`/`LOCKED`/`LOCKING`/`NOT IN USE`；UTC Time `1970-01-01 00:00:00`；MasterID / GMClockID（祖父时钟 ID）；Sync / FollowUp / DelayReq / DelayResp 报文速率；Network Status `UNAVAILABLE`/`NOT GOOD`/`GOOD`/`VERY GOOD`；Delay `0ns`；Jitter `0ns`。N04 STEP：`ONE-STEP`/`TWO-STEP`。 | ≠ 单一"是否同步"指示——PTP 状态有独立取值体系，且区分一步/两步时间戳模式与祖父时钟（GMClockID），还有多个报文速率计数器。 |
| **FRAME SYNCHRONIZER** (h65) | S12：设置返回信号的帧同步器功能；取值 `OFF`、`ON`。M02（HD/UHD PROMPTER）：`FRAME SYNC OFF`/`ON`/`(ON)` 在 ON/OFF 之间切换。 | ≠ 全局单一开关——在返回信号（S12）与提示机（M02）**两处各有独立开关**，且 M02 中默认标为 `(ON)`。 |

---

## 5. 网络与 IP

| 术语 (h) | 手册定义 | 与常识用法的差异 |
|---|---|---|
| **IP Live（LSM / IP LIVE SYSTEM MANAGER）** (h37) | 设置 IP Live System Manager。PORT：`DISABLE`/`LAN1&LAN2`（LAN1&LAN2＝用 LAN1 和 LAN2 与 LSM 通信，用于冗余）；**更改 PORT 设置后重启本机**。PRIMARY/SECONDARY IP ADDRESS 设 LSM1/LSM2 地址。连接状态：`DISCONNECTED`/`CONNECTING`/`CONNECTED`。MULTICAST ADDRESS：PORT 设 LAN1&LAN2 时**固定为 AUTO**。 | ≠ 普通 IP 组网——IP Live 是 Sony 的 ST2110 全 IP 制作系统，由 LSM 集中管理（双 LSM 冗余）；启用 LSM 后多播地址被 LSM 接管（固定 AUTO）。 |
| **SMPTE ST2110** (h38) | HKCU-SFP50 网络接口板"可与 SMPTE ST 2110 兼容设备连接"；"如果在 SMPTE ST 2110 兼容系统中运行, 则设置为 NETWORK"（GENLOCK MODE）。 | ≠ 普通以太网/IP 视频——ST2110 系统**要求 GENLOCK MODE＝NETWORK**（PTP 同步），不使用外部 REFERENCE。 |
| **NMOS（IS-04 / IS-05）** (h39) | PORT：`DISABLE`/`LAN-COM`（仅当 <IP LIVE> IP LIVE SYSTEM MANAGER PORT 设为 DISABLE 时才能选）。PORT NUMBER (IS-04 NODE)：`100 至 65535`、`3001`；PORT NUMBER (IS-05 CONNECTION)：`100 至 65535`、`3002`。 | ≠ 通用 REST API——IS-04 是 Node API（发现/注册）、IS-05 是 Connection API（连接管理），属广播 NMOS 规范；且与 IP LIVE（LSM）**互斥**。 |
| **RDS** (h40) | 使用"注册和发现系统"(RDS) 启用/禁用自动检测；启用后将在同一子网内启用 RDS 发现。"如果 RDS 在同一子网内不可用,请禁用此设置并手动设置 IP 地址。"RDS IP ADDRESS / RDS PORT NUMBER：`100 至 65535`、`18235`。 | ≠ 广播 RDS（调频数据）——此处 RDS ＝ **NMOS Registration & Discovery System**（注册与发现系统），与 FM 的 Radio Data System 无关。 |
| **TSL UMD** (h41) | 使用 TSL UMD V5.0 启用/禁用 IP 计数器；PORT：LAN-COM；PORT NUMBER `8900`（UDP 端口）。PACKET STATUS：`NOT RECEIVED`/`RECEIVED`，收到时还显示 ID 与红/绿/黄计数器开/关状态，最多显示五个 ID，超过则显示 `AND MORE`。 | ≠ 本地 Tally 接线——它是通过网络（UDP 8900）传输 Tally/UMD 的协议。 |
| **Ember+** (h42) | 使用 Ember+ 启用/禁用配置；可通过安装 HZCU-CNFG50 摄像机升级软件（选件）启用。PORT：LAN-COM；PORT NUMBER `9000`（TCP）。CONNECTION STATUS：`DISCONNECTED`/`CONNECTING`/`CONNECTED`。 | ≠ 通用协议——Ember+ 是通过 CCU 的 LAN-COM 接口**配置本机**的控制协议（TCP 9000），需 HZCU-CNFG50 软件选件。 |
| **SNMP / SNMP TRAP** (h43) | 启用/禁用 SNMP，可通过安装 HZCU-SNMP50 摄像机升级软件（选项）启用；PORT：LAN-COM；NAME/CONTACT/LOCATION：ASCII 最多 32 字符；V1/V2C `ENABLE`；RO COMMUNITY `sony`；ALLOW HOST `ANY`/`SPECIFIC`；HOST1-3 IP ADDRESS。SNMP TRAP：当启用 SNMP 时可选，禁用 SNMP 时固定 `DISABLE`。 | ≠ 通用网管——本机 SNMP **仅 V1/V2C（无 V3）**、只读社区默认 `sony`、走 LAN-COM，且需 HZCU-SNMP50 软件选件。 |
| **MULTICAST ADDRESS** (h44) | 设置 IP 流的多播地址设置的模式切换方法；取值 `AUTO`、`MANUAL`。PORT 设 LAN1&LAN2 时固定 AUTO（用从 LSM 配置的地址）；PORT 设 DISABLE 时固定 MANUAL（用 MULTICAST ADDRESS 1 至 5 页手动设置）。IP ADDRESS：`224.0.0.1 至 239.255.255.255`；PORT：`100 至 65535`。 | ≠ 可随时手改的组播地址——被 LSM PORT 设置**锁定**为 AUTO 或 MANUAL，并分 5 页（N08-N12）覆盖 VIDEO OUT / RETURN / AUDIO / HD TRUNK AUDIO / PGM IN / INTERCOM / META。 |
| **HITLESS FAILOVER** (h45) | 启用/禁用 IP 流冗余；取值 `ON`、`OFF`。 | ≠ 普通链路冗余——它是 **IP 流级**的无中断倒换（配合双 LSM/双 LAN）。 |
| **25G FEC（RS-FEC / FC-FEC）** (h46) | 为 25G 设置 FEC 模式；取值 `OFF`、`RS-FEC(CL108)`、`FC-FEC(CL74)`。仅当选择了 LAN1 或 LAN2 时显示；设为要连接的 IP 交换机的端口设置。 | ≠ 通用纠错开关——必须与对端 IP 交换机端口一致；分 RS-FEC(CL108) 与 FC-FEC(CL74) 两种。 |
| **自动 IP（Auto IP）** (h47) | 将 DHCP 设为 ON 而网络无 DHCP 服务器时，本地分配唯一的链路本地地址（`169.254.0.0/16`）。"**'自动 IP'功能仅适用于 LAN COM 接口。它不适用于 HKCU-SFP50 的 LAN 1 和 LAN 2 接口。**"重启后地址可能更改，只能用于设置目的。 | ≠ 通用 DHCP 回退——手册明确限定**仅 LAN COM 生效**，LAN1/LAN2 不适用；重启后地址可能改变、只能用于设置目的。 |
| **SERVICE DISCOVERY** (h48) | 启用/禁用服务发现功能。ON＝在 Web 菜单中显示 CCU 列表；OFF＝不显示。"设为 OFF 时,本机无法由同一子网上其他 CCU 的服务发现功能检测到。"本机使用多播从同子网其他 CCU 获取信息，建议用支持 IGMP Snooping 的路由器。 | ≠ 通用网络发现——用**多播**获取同子网 CCU 信息，建议支持 IGMP Snooping 否则造成广播负载；关掉后本机也不被他人发现。 |

---

## 6. CNS 与编号

| 术语 (h) | 手册定义 | 与常识用法的差异 |
|---|---|---|
| **CNS MODE** (h49) | 设定通信模式；取值 `LEGACY`、`BRIDGE`、`MCS`。MCS MODE `CLIENT`（选择 MCS 模式时本机作为客户端，仅显示）。 | ≠ 通用"通信模式"——这是 **Sony 私有摄像机控制网体系**（与 RCP 手册同名用法）；且 MCS MODE 是"仅显示"固定值 CLIENT，不可改。 |
| **CCU NO** (h50) | 设定 CCU 编号。CNS MODE 选 MCS 时：`空白, 1 至 96`；选 LEGACY 或 BRIDGE 时：`空白, 1 至 96, A 至 Z`。前面板：摄像机编号为 0 时，LAN COM 接口的 IP 地址和子网掩码会定期滚动显示。 | ≠ 任意字符串——取值域**受 CNS MODE 约束**（MCS 下不允许 A-Z）；编号为 0 时触发前面板 IP/子网滚动显示。 |
| **MASTER IP ADDRESS** (h51) | 设定主设备的 MCS 模式 IP 地址；范围 `0.0.0.0 至 255.255.255.255`。 | ≠ 本机 IP——它是 MCS 体系里"主设备"的 IP（本机作为客户端去连的主），与 N01 的 IP ADDRESS（本机自身）不同。 |
| **FORCE LEGACY** (h90) | M08 ASSIGNABLE SWITCH 取值 FORCE LEGACY："将通信模式强制设定为 LEGACY 模式。"M06 ALARM SETTINGS：`OFF`/`ON`（设为 OFF 将不显示 FORCE LEGACY 警报）。错误消息：`CCU:FORCE LEGACY`——为 CNS MODE 强制设置 LEGACY。 | ≠ 普通模式切换——它既是**前面板可编配按钮功能**，又是**报警项**（有 CCU:FORCE LEGACY 报警），用于把 CNS 强制拉回 LEGACY。 |

---

## 7. 接口

| 术语 (h) | 手册定义 | 与常识用法的差异 |
|---|---|---|
| **SDI-OUT** (h52) | SDI OUT（3G/HD/SD SDI 输出）1/2/3/4 接口（BNC 型）：摄像机信号可作为 3G/HD SDI/SD SDI 信号输出，可输出叠加有文本字符和标记的信号。菜单 MONITOR：`C`＝不添加字符、`M`＝已添加字符。 | ≠ 四个口行为一致——SDI-OUT1/2 的 MONITOR **固定为 C**，只有 SDI-OUT3/4 可选 C 或 M；且 SDI-OUT4 设为 C 时不显示 CCU MENU（需将 DISP/MENU 杆保持在 MENU 位置 3 秒钟）。 |
| **SDI-I/O** (h53) | SDI I/O（3G/HD SDI 输入/输出）1/2/3/4 接口（BNC 型）：可用作返回视频输入、HD 提示器输入、摄像机视频信号输出和 HD-TRUNK 输出，按应用程序在 MAINTENANCE <TRUNK/PROMPTER> 的 NETWORK TRUNK 设置。I/O：`IN`/`OUT`。SIGNAL：OUT 时 `SDI-OUT`/`HD TRUNK`（仅 SDI-I/O 3）；IN 时 `SDI-RET`/`HD PROMPTER`（仅 SDI-I/O 4）。 | ≠ 固定输入或输出——每个口方向由 I/O 项决定，功能**随方向与端口号变化**（仅 3 可 HD TRUNK、仅 4 可 HD PROMPTER）。 |
| **SDI-RET** (h54) | SDI RET（3G/HD/SD SDI 返回视频输入）1/2/3/4 接口（BNC 型）：可单独接收四个不同的 3G/HD/SD SDI 返回视频输入信号，由摄像机返回开关进行 RET 1 到 4 的选择，也可选择 SD 信号纵横比。S13 设置值如 `1080/59.94P/3G`、`1080/50P/3G`、`1080/59.94I(PsF)`、`1080/23.98PsF`、`720/59.94P`、`525/59.94I(PsF)`、`625/50I(PsF)`；SD 时须设 `SQUEEZE`/`LETTER BOX`/`EDGE CROP`。 | ≠ 本机输出——它是"**返送**"（从外部回到摄像机方向）输入；RET1-4 格式由 RETURN FORMAT1 设定，且 SD 信号须设纵横比。 |
| **UHD-SDI A-H** (h55) | UHD SDI A/B/C/D 接口（BNC 型）：来自摄像机的信号输出为 UHD(4K) SDI 信号，还可将 C 和 D 接口用作输入接口。UHD-SDI B：I/O `OUT`（固定）；SIGNAL `SDI-OUT`/`UHD TRUNK`（UHD TRUNK 仅适用 HDCU5000/5500）。UHD-SDI D：IN 时 SIGNAL `SDI-RET`/`UHD PROMPTER`（UHD PROMPTER 仅适用 HDCU5000/5500）。UHD-SDI E/F/G/H：仅在已安装 HKCU-SDI50 时显示。格式表注：B/C/D/E/F/G/H 设置与 UHD SDI A 设置**关联**。 | ≠ 八个独立可配口——B/C/D 及 E/F/G/H 的格式设置都"与 UHD SDI A 设置关联"；**A/B 是专用输出**（无法配置返回格式），C/D/G/H 可作返回输入。 |
| **IP-OUT / IP-RET** (h56) | IP-OUT：设置 LAN 1 和 LAN 2 接口的输出，含 MONITOR、FORMAT、OETF、COLOR、SOURCE（`CAMERA`/`HD TRUNK`）。"IP-OUT4 是专用 4K 输出的设置。当 HZCU-UHD35 选件启用时,HDCU3500 支持输出。"IP-RET：设置要在 LAN 1/LAN 2 上输入的返回信号格式——IP-RET1、2：`1080/59.94P`、`1080/50P`、`1080/59.94I`、`1080/50I`；IP-RET3：`1080/59.94I(PsF)`、`1080/50I(PsF)`；IP-RET4：`3840×2160/59.94P/12G`、`3840×2160/50P/12G`。 | ≠ SDI 的 IP 版统一格式——只在装 HKCU-SFP50 时存在，且**各 IP-RET 口的格式集合不同**（RET1/2/3/4 不等同）。 |
| **PROMPTER** (h57) | PROMPTER（电视播音稿提示机输入）1/2 接口（BNC 型）：根据 <REAR I/F> 的 PROMPTER2/VBS-RET 设置与 <TRUNK/PROMPTER> 的 PROMPTER CHANNEL MODE 设置，输入 1 个或 2 个通道的提示器信号。"如果使用的信号是 1.0 Vp-p、75 欧姆模拟信号, 则无论信号格式如何,都会以 5M H z 的频带宽度从摄像机的 PROMPTER OUT 接口输出信号。""如果是 HDC5500, 请连接 PROMPTER1 接口。PROMPTER2 接口不支持此信号。" | ≠ 数字视频接口——PROMPTER 是 **1.0 Vp-p、75 欧姆模拟信号**，带宽 5MHz；且 PROMPTER2 兼做 VBS-RET，HDC5500 的提示机只能用 PROMPTER1。 |
| **VBS-RET** (h58) | VBS-RET（VBS 返回视频输入）接口（BNC 型）：可独立输入 VBS 返回视频信号；"此接口可兼做 PROMPTER 2 接口。"S03 PROMPTER2/VBS-RET：设为 `ENABLE`（固定）——设置为第二个电视播音稿提示机和 VBS 返回信号输入的信号输入。 | ≠ 独立专用口——它与 PROMPTER2 **共用同一物理 BNC**，且 S03 项被固定为 ENABLE（不可改）。 |
| **AES/EBU** (h59) | AES/EBU 接口（BNC 型）：输出将输入到摄像机的 AES/EBU 格式的数字音频信号。S03 CHARACTER：取值 `CHARACTER`/`AES/EBU`/`SYNC`；"AES/EBU 仅适用于 HDCU5500/3500。" | ≠ 可任意分配的独立口——在 HDCU5000 上 AES/EBU **不可选**（仅 HDCU5500/3500），且它与 CHARACTER/SYNC 共享一个 BNC（由 S03 CHARACTER 项三选一）。 |
| **CHARACTER / SYNC** (h60) | CHARACTER：将自诊断结果或本机的设定菜单作为 SD 模拟视频信号输出。SYNC：从内部同步信号发生器输出 SD 复合同步（无脉冲信号）或 HD 3 电平同步信号（默认值：SD 复合同步信号）。S03 CHARACTER：取值 `CHARACTER`/`AES/EBU`/`SYNC`。 | ≠ 两个独立物理口——CHARACTER 与 SYNC（及 AES/EBU）**共用同一 BNC**，由 S03 选择功能；CHARACTER 输出是 SD 模拟视频（用于看菜单/自诊断）。 |
| **INTERCOM/TALLY/IO** (h61) | 对讲/计数/输入/输出接口（D-sub，50 芯）：用于对讲、计数器和程序音频信号的输入和输出；连接对讲系统的对讲/计数器/程序音频接口。REAR PREVIEW 功能：为输出引脚分配第 35 芯。S03 MIC/WF REMOTE：切换第 36 芯到 43 芯的功能。 | ≠ 仅对讲口——它是**一口多用**的 50 芯 D-sub（对讲+Tally+PGM+REAR PREVIEW），引脚功能可切换。 |
| **HD PROMPTER / UHD PROMPTER** (h63) | S02：SDI-I/O 4（IN 时）SIGNAL 可选 HD PROMPTER；UHD-SDI D（IN 时）SIGNAL 可选 UHD PROMPTER（仅适用 HDCU5000/5500）。M02：HD PROMPTER FRAME SYNC `OFF`/`ON`/`(ON)`，SOURCE `SDI-I/O4`/`IP-RET3`；UHD PROMPTER DATA RATE `1.5G`/`3G`/`6G`/`12G`，SOURCE `UHD-SDI D`。 | ≠ 模拟 PROMPTER 接口 (h57)——HD/UHD PROMPTER 是**经 SDI 链路的数字提示机信号**（SDI-I/O4 或 UHD-SDI D），与 BNC 模拟 PROMPTER 1/2 是两套机制。**近义非重复**。 |
| **RETURN SELECT / RETURN FORMAT1-4** (h64) | S12 RETURN SELECT：设置要输入的返回信号的格式；每项 RET1-8 取值含 `SDI-RET1`…`SDI-RET4`、`SDI-I/O1`…`SDI-I/O4`、`UHD-SDI C/D/G/H`、`VBS-RET`、`IP-RET1`…`IP-RET4`。S13 RETURN FORMAT1（SDI-RET 1-4）、S14 RETURN FORMAT2（SDI-I/O 1-4）、S15 RETURN FORMAT3（UHD-SDI C/D/G/H）、S16 RETURN FORMAT IP（IP-RET1-4）。 | ≠ 与输出格式同表——返回格式是**独立的一张矩阵**（p49-53），由 CAMERA FORMAT × FIBER TRANSMIT RATE × SYSTEM 决定；且 RETURN SELECT 只"选择返回信号来源"，具体格式在 RETURN FORMAT1-4 设定。 |
| **MONITOR (C / M)** (h66) | 设置是否向输出信号添加字符。`C`＝不添加字符、`M`＝已添加字符。SDI-OUT1/2、SDI-I/O1-4、UHD-SDI A-H **固定为 C**；SDI-OUT3/4、IP-OUT2/3 可选 C 或 M（SOURCE 设 CAMERA 时固定 M，设 HD TRUNK 时固定 C）。SDI-OUT4 设为 C 时不显示 CCU MENU（将 DISP/MENU 杆保持在 MENU 位置 3 秒钟可显示）。 | ≠ 监视器设备设置——它是"**是否在输出信号上叠加字符**"的开关，且多数口被固定为 C，只有 OUT3/4 与 IP-OUT2/3 可选。 |

---

## 8. 文件与诊断

| 术语 (h) | 手册定义 | 与常识用法的差异 |
|---|---|---|
| **CCU FILE** (h67) | 本机的所有菜单设置都可保存到 CCU 文件中；使用 RECALL 加载并应用。**使用 RECALL 不会加载 LAN COM 接口的 IP 地址、子网掩码和默认网关设置。**STORE：将 CCU 文件保存到内存中，本机最多可保存五个。FILE NAME1 至 5：ASCII 代码，1 至 32 个字符。USB 闪存驱动器的路径为 `/MSSONY/PRO/CAMERA/HDCU5000`。 | ≠ 普通"配置文件"——它是整机菜单设置的**快照**（最多 5 个），但明确**不含 LAN COM 的 IP/子网/网关**；USB 路径固定。 |
| **FILE INDEX** (h68) | `1 至 5`、`1`：选择目标文件编号以便操作。 | ≠ 文件列表——它是"选择要操作哪个 CCU 文件槽"的编号（1-5），所有 RECALL/STORE/EXPORT/IMPORT/FILE NAME 操作都以它为对象。 |
| **RECALL / STORE** (h69) | RECALL：加载并应用保存的设置以简化设置操作；**不会加载 LAN COM 接口的 IP 地址、子网掩码和默认网关设置**。STORE：将 CCU 文件保存到内存中。 | ≠ 对称的保存/加载——STORE 存的是完整快照，而 RECALL 加载的是"**除网络设置外**"的菜单设置，二者**不对称**。 |
| **LOG** (h70) | 启用或禁用保存日志文件；取值 `ENABLE`、`DISABLE`。EXPORT TO USB 将日志保存到 USB（EXEC 执行）；CLEAR 删除本机内部存储的日志（EXEC 执行）。**日志最多保存 30 天。当达到 30 天的最大值时,会从最旧的日志开始删除。**M04 DATE&TIME："当此项更改时,本机上存储的所有日志都会被删除。" | ≠ 无限期日志——最多 30 天、超期从最旧开始删；且**更改 DATE&TIME 会清空全部日志**。 |
| **BOARD STATUS** (h71) | VIF `OK`/`POWER ERROR`/`PLD ERROR`/`TEMP WARNING`（VIF 板自诊断）；TX 板自诊断结果；NET（HKCU-SFP50 板，选件）自诊断结果。POWER ON HOUR METER `99999 H`；HOUR METER `99999 H`。 | ≠ 单一整机状态——它是**分板卡**（VIF/TX/NET）的自诊断，取值体系为 OK/POWER ERROR/PLD ERROR/TEMP WARNING。 |
| **HOUR METER** (h72) | POWER ON HOUR METER `99999 H`（累计开机时间）；HOUR METER `99999 H`（累计开机时间）。 | ≠ 时钟时间——单位是 **H（小时）**，上限显示 `99999 H`，用于累计开机时长（维护周期参考）。 |
| **光线传感器电平** (h73) | CABLE CONDITION 灯：指示 CAM 与 CCU 的通信状态——右侧两个绿灯亮＝接收状态非常好；右起第二个绿灯＝良好；左起第二个黄灯＝水平低；左侧红灯＝最低水平。状态画面：CAM＝摄像机光线传感器电平、CCU＝控制单元光线传感器电平。Web 菜单：以九个等级的条形颜色和长度显示。错误消息：`CCU:OPTICAL CONDITION OK/WARNING/CARE/ERROR`。 | ≠ 环境光传感器——它是**光纤收发功率的健康度指标**（CAM 侧/CCU 侧各一），错误消息里叫 OPTICAL CONDITION。 |
| **CABLE CONDITION** (h74) | CABLE CONDITION（信号接收状态）指示灯：指示 CAM 与 CCU 的通信状态。状态画面：Camera Cable＝摄像机电缆连接状态（如 `Connected`）。 | ≠ 线缆是否插好——它实为**光纤链路接收质量**（与光线传感器电平同源）；"是否插好"由 CABLE ALARM 的 OPEN 态表达。 |
| **CABLE ALARM** (h75) | OPEN：当未通过光纤电缆将摄像机连接到本机后面板上的 CAMERA FIBER 接口时点亮；**当此指示灯点亮时,不会对摄像机供电**。SHORT：当过电流流经光纤电缆时点亮；**当此指示灯点亮时,不会对摄像机供电**。错误消息：`CCU:PS CABLE SHORT`（短路）、`CCU:PS CABLE OPEN`（断路）。 | ≠ 通用报警——只有 **OPEN/SHORT 两态**，且两态都导致"不对摄像机供电"。 |
| **SIGNAL BAR** (h76) | SIGNAL BAR 指示灯：指示视频信号的输出状态。灰色信号输出期间＝关闭；彩条输出期间＝按 M08 `SIGNAL BAR` `READY COLOR`（`WHITE`/`GREEN`/`BARS`）指定颜色点亮；摄像机视频输出期间＝以**白色流动**方式点亮。 | ≠ 电平表——它是"**当前输出信号类型**"的指示（灰场=灭、彩条=READY COLOR 色、摄像机视频=白色流动），不是信号强度条。 |
| **CCU:XXX 错误消息格式** (h93) | 当本机或摄像机检测到错误时，ALARM 指示灯点亮，且本机上显示出错信息。例：`CCU:XXX POWER ERROR`（板载电源错误，XXX 为板名称）、`CCU:XXX PLD ERROR`、`CCU:XXX TEMP WARNING`、`CCU:PS FAN STOP`、`CCU:GENLOCK ERROR`、`CCU:10FIELD-ID ERROR`、`CCU:SET DATE&TIME`（无效日期）、`CCU:LINK SPEED MISMATCH`（LAN1 和 LAN2 的链路速度不匹配）。 | ≠ 自由文本——错误消息遵循固定前缀 `CCU:` + 对象（板名/PS/OPTICAL 等）+ 现象；其中 `XXX` 是板名称占位符（与 BOARD STATUS 的 VIF/TX/NET 对应）。 |

---

## 9. 选件与型号

| 术语 (h) | 手册定义 | 与常识用法的差异 |
|---|---|---|
| **HKCU-FB50** (h77) | UHB 传输套件（HDCU3500）：将本机升级到相当于 HDCU5500。可替代 HDCU3500 背面的 UHD SDI A/B/C/D 接口，在 HDCU3500 上支持 4K 传输。**要进行 4K 输出，必须安装 HZCU-UHD35 4K/HDR 软件（选件）。**规格：功耗 40 W；接口 BNC、行数 4；信号类型 SMPTE ST2082/ST2081/ST425/ST424/ST292。 | ≠ 普通接口板——它**改变 HDCU3500 的型号能力**（等同 HDCU5500），且 4K 输出还需叠加 HZCU-UHD35；装它后 FIBER TRANSMIT RATE 才能选 ULTRA。 |
| **HKCU-SDI50** (h78) | 12GSDI 接口板（HDCU5000）：使用四个输出的单个系统，启用 4K 格式的 12G-SDI 输出。可安装在 HDCU5000 背面的选件套件安装端口 3 中。规格：功耗 5W；HIF 板 BNC 型 (4)；12G SDI＝SMPTE ST2082、`11.880 Gbps`/`11.868 Gbps`。 | ≠ 通用 SDI 板——它只在 HDCU5000 上装，并解锁 **UHD-SDI E/F/G/H（OUTPUT FORMAT4）与 UHD-SDI G/H 返回**。 |
| **HKCU-SFP50** (h79) | 网络接口板（HDCU5000/5500/3500）：在 IP 传输系统中启用操作，"可与 SMPTE ST 2110 兼容设备连接"。使用 LAN 1 和 LAN 2 接口（SFP+/SFP28）执行 IP 视频/音频输入输出、内部通信和网络同步，"这将在 HDCU5000/5500/3500 上启用一个 4K 和三个 HD IP 输入/输出"。使用 IP 输出需要 OTM-10GSR1 或其他 SFP+ 模块或 SFP28 模块。规格：功耗 43 W；信号类型 10GBASE-\*\*、25GBase-\*\*。 | ≠ 仅"网络口扩展"——它同时是 IP 输出、IP 返回、IP 音频/对讲、PTP 网络同步（GENLOCK MODE＝NETWORK）、IP Live/NMOS/SNMP/Ember+/TSL UMD 的**前提**；装了它菜单里才出现大量标记项。 |
| **HKCU-SM50** (h80) | 单模光纤接口（HDCU5000/5500/3500）：启用与支持单模光纤传输的 Sony 摄像机的连接。**"只能用于连接 HDC3500/3100 和 HDC2000 系列摄像机。不能连接 HDC5000/5500。"**单模光纤连接：信号传输最长可达 10 km；**需要 HDCE-100 摄像机扩展适配器（选件）**。规格：功耗 1.2 W；适用于单模光纤电缆的 ST 接口 (2)。 | ≠ 普通光纤接口——它是**单模（ST 接口）**，且明确**不能连 HDC5000/5500**；单模连接还需 HDCE-100 适配器，且 CABLE TYPE 需设为 SINGLE-MODE FIBER。 |
| **HZCU-CNFG50 / HZCU-SNMP50** (h81) | 摄像机升级软件（HDCU5000/5500/3500）：CNFG50 支持使用 EMBER+ 协议通过 CCU 的 LAN-COM 接口配置本机；SNMP50 支持使用 SNMP 协议通过 CCU 的 LAN-COM 接口进行远程监控。M09 OPTION：READ KEY FROM USB——从 USB 闪存驱动器读取安装密钥。 | ≠ 硬件板——它们是**软件升级**（通过 USB 安装密钥），分别解锁 Ember+ 与 SNMP 两类协议，均走 LAN-COM。 |
| **HZCU-UHD35** (h82) | 4K/HDR 软件（HDCU5000/5500/3500）：支持将从摄像机传输的 HD 信号转换为 4K 信号。当安装了 HKCU-SM50 时，在 HDCU5000/5500 上支持此软件。IP-OUT4：当 HZCU-UHD35 选件启用时，HDCU3500 支持输出。HKCU-FB50：要进行 4K 输出，必须安装 HZCU-UHD35。 | ≠ 通用 4K 升级——它是"**把 HD 信号转成 4K**"（4K/HDR 软件），且与 HKCU-SM50/FB50 有依赖说明；HDCU3500 的 IP-OUT4 与 IP-RET4 都需它。 |
| **UHB** † (h83) | 手册中仅作 "HKCU-FB50 UHB 传输套件"、"UHB 标签 (2)"、"UHB 密封件" 出现，**未展开含义**。 | ≠ 通用缩写——UHB 在本手册是 HKCU-FB50 套件的名称，不是"超宽带"泛称。**释义待复核。** |
| **RMM-301** (h84) | 本机可在标准 19 英寸 EIA 机架中安装，高度为 3 个单位；对于 HDCU5500/3500，使用 RMM-301 机架适配器（选件）。 | ≠ 机架本身——它是 **HDCU5500/3500 装机架时所需的适配器**（HDCU5000 不需）。 |
| **HDCU5000 / HDCU5500 / HDCU3500** (h85) | HDCU5000/5500 通过光纤电缆连接 HDC5000/5500 高清彩色摄像机；HDCU3500 连接 HDC3500 高清彩色摄像机、HDC3100 光纤彩色摄像机或 HDC2000 系列高清彩色摄像机。规格差异：HDCU5000 约 19.5 kg、电流 7A（最大）、工作温度 `5°C 至 40°C`、CAMERA FIBER 光纤接口 (2)；HDCU5500 约 6.4 kg、4.5A、`–10°C 至 +40°C`、CAMERA FIBER (1)；HDCU3500 约 6.3 kg、4.5A、`–10°C 至 +40°C`。 | ≠ 同一设备的三个型号——连接对象、CAMERA FIBER 数量（2 vs 1）、工作温度范围、可装选件（SDI50 仅 5000；FB50 仅 3500）都不同；4K 能力也不同（3500 入门仅 HD，需选件升级）。 |
| **HDC5000 / HDC5500** (h86) | HDCU5000/5500 通过光纤电缆连接 HDC5000/5500 高清彩色摄像机。FIBER TRANSMIT RATE：ULTRA＝连 HDC5000/5500 或装 HKC-FB50 的 HDC3500 时。 | ≠ HDCU（CCU）——**HDC 是摄像机头，HDCU 是控制单元**；连 HDC5000/5500 时 FIBER TRANSMIT RATE 用 ULTRA。 |
| **HDC3500 / HDC3100** (h87) | HDCU3500 通过光纤电缆连接 HDC3500 高清彩色摄像机、HDC3100 光纤彩色摄像机或 HDC2000 系列高清彩色摄像机。HKCU-SM50 可连接 HDC3500/3100 和 HDC2000 系列。FIBER TRANSMIT RATE：HIGH＝连 HDC3500（未装 HKC-FB50）/HDC3100/HDC2000 系列时。 | ≠ HDC5000/5500——连 HDC3500（未装 FB50）/HDC3100 时速率用 HIGH；装 FB50 后 HDC3500 才能升到 ULTRA。 |
| **HDC2000 系列** (h88) | HDC2000 系列：`HDC2000/2580/2500/2400/1700`。该系列支持光纤连接。FIBER TRANSMIT RATE：HIGH＝连 HDC3500（未装 HKC-FB50）/HDC3100/HDC2000 系列时。 | ≠ 单一型号——它是**五个型号的统称**（HDC2000/2580/2500/2400/1700），需整体理解。 |
| **HDCE-100 / HDCE-200** (h89) | HDCE-100：单模光纤连接需要 HDCE-100 摄像机扩展适配器（选件）。HDCE-200：同轴电缆 (HDCE) 连接示例使用 HDCE-200 摄像机扩展适配器，配合 CABLE TYPE 设为 COAX(HDCE)。 | ≠ 可选配件——它们是两种连接方式的**必备适配器**：HDCE-100 用于单模光纤、HDCE-200 用于 COAX(HDCE) 模式；缺失则对应连接方式不成立。 |

---

## 10. 前面板与操作

| 术语 (h) | 手册定义 | 与常识用法的差异 |
|---|---|---|
| **菜单锁定开关 / DISP/MENU 控制杆 / CONTROL 旋钮** (h92) | 菜单锁定开关：锁定前面板菜单操作区域的操作。DISP/MENU 控制杆和指示灯：选择状态显示或设定菜单显示，在设定菜单模式指示灯点亮。CONTROL 旋钮（旋转编码器）：在状态画面模式用于更改显示的页面；在设定菜单模式用于移动光标和更改菜单设定；按下此旋钮可执行与将 CANCEL/ENTER 控制杆设定到 ENTER 位置相同的功能。Web 菜单："当本机的菜单锁定开关处于 ON 位置时, 无法使用 Web 菜单配置本机。" | ≠ 普通面板按键——**菜单锁定开关 ON 会同时禁用前面板菜单与 Web 菜单配置**；DISP/MENU 控制杆在 DISP/MENU 位置分别进入"状态画面/设定菜单"。 |

---

## 附：待复核术语（手册未定义）

以下 3 条手册**只使用未定义**，释义含行业通用知识，已列入 `needs-review.md`；上表仍以 `†` 标出以便查阅，待复核通过后转为正式条目。

| 术语 (h) | 手册中的出现方式 | 缺口 |
|---|---|---|
| **PsF** † (h13) | 仅以格式串出现（`1080/29.97PsF`、`1080/59.94I(PsF)` 等） | 手册未定义；"Progressive segmented Frame" 系行业外部知识。 |
| **SQD / 2SI** † (h14) | 仅以格式串出现（`3840×2160/59.94P/SQD/3G-A`、`…/2SI/3G-A`），V01 提到"4K 双样本交错" | 手册未展开 SQD/2SI 全称与像素切分规则。 |
| **UHB** † (h83) | 仅作 "HKCU-FB50 UHB 传输套件"、"UHB 标签"、"UHB 密封件" | 手册未展开 UHB 含义。 |

---

---

## 溯源说明

- **RCP 侧 35 条**：阶段 1 `glossary-extractor` 候选 → 阶段 1.5 三重验证通过，条目内容未改动。
- **CCU 侧 93 条**：阶段 1 `glossary-extractor` 候选（`candidates/glossary.md`）→ 阶段 1.5 三重验证，其中 90 条正式、3 条（`h13` PsF / `h14` SQD-2SI / `h83` UHB）待复核。相关逐条验证记录与待复核缺口清单保存在 CCU 单书工作目录中，**未随本技能包分发**。
- 合辑合并只做两件事：加本标题头（含第 0 节跨书对照）、给 CCU 侧编号加前缀 `h`。除此之外两书条目**零改写**。
- 待复核的 3 条（`h13` / `h14` / `h83`）在合辑内仍标 `†`，其释义含行业通用知识而非手册原文，**引用时须注明来源非手册**。
