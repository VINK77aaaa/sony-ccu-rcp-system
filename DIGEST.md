# Sony 摄像机控制系统使用说明书合辑（RCP-3500/3501 + HDCU5000/5500/3500）— 精华 (DIGEST)

> 本文由 cangjie-skill 蒸馏生成，只呈现**通过三重验证**的内容 — 不是全书摘要，是筛过水分的精华。
> 想深入某个方法论时，点小节末尾的能力卡链接；想看全貌，读 [SKILL.md](./SKILL.md)。
> 作者: Sony Corporation | 2019（文档号 5-017-036-61 (1)，56 页 + 5-006-304-43 (1)，94 页）| 全文约 7,900 字，预计阅读 24 分钟

## 这套系统在讲什么

这不是一本书，是两本：一本是《遥控面板 RCP-3500 / RCP-3501 使用说明书》（56 页），讲的是演播室里那个控制摄像机画质的控制台；一本是《摄像机控制单元 HDCU5000 / HDCU5500 / HDCU3500 使用说明书》（94 页），讲的是机架上那台负责信号进出的 CCU。合在一起，它们描述的是**同一条"控制—被控"链的两端**：面板侧决定"谁控制谁、怎么调"（组网、控制权仲裁、权限、日常调整、参数资产），主机侧决定"信号怎么进出、怎么同步"（传输方式、系统格式、输出/返回格式、HDR、同步、网络、诊断）。

一句话主旨是：教工程师与操作者把 Sony 遥控面板与摄像机控制单元组成一套可用的演播室摄像机控制系统。但**这套合辑真正值得读的地方，恰恰在于"两本书合成一条链"这件事本身**——单看任何一本，你只能看到半条链。面板手册写"怎么接、怎么编号、怎么配 IP"，主机手册写"这条链的另一端长什么样"；两侧处在同一条链的上下游，互为前置。把两本放在一起读，才会浮现出单本里根本看不见的东西：一个横跨两端的**四开关派生链**、一个**同名不同义的灯语陷阱**、一组**两端不对称的权限与错误体系**、以及几处**两书互相矛盾或互相留白**的接缝。这些是本文最想交付的部分。

因此本文不按"31 张能力卡清单"组织，而按**这套设备系统本身的结构**组织：先讲接进系统的第一个分叉（两端各有一个模式开关），再讲信号怎么从开关派生出来，然后是 HDR 与同步这两个容易混的"域"，接着是权限与控制权、资产与日志，最后是排障与联调。读完之后，你应该能在任何一个"系统不对劲"的现场，第一反应不是乱拧旋钮，而是先问一句：**问题出在面板侧、主机侧，还是两者之间的链路侧？**

---

## 一、接进系统的第一个分叉：两端各有一个"模式开关"

### 面板侧：CNS 是四选一，判据是物理连线

RCP 与摄像机系统怎么连，由一个叫 **CNS** 的连接模式决定，四选一：只拉 CCA-5 专用电缆 → `LEGACY`（唯一免配网络参数的模式，"TCP/IP 和 RCP 编号无需设定"，第 5 / 18 页）；只拉网线且一对一 → `BRIDGE`（要配本机 IP + 目标 IP，但"无法采用多摄像机操作"，第 18 页）；网线连面板 + CCA-5 连 CCU 的混合拓扑，或多面板 / MSU 多机系统 → `MCS`（要配本机 IP + 主设备 IP + RCP 编号）；由 PC 软件 HZC-RCP5 控制 → `PC 控制`（"可连接最多六个 RCP 单元"，第 6 页）。三条铁律横跨所有模式：系统内 IP 与 RCP 编号必须唯一；**更改 CNS 后必须重启所有摄像机系统**（不是只重启本面板）；纯 LAN 供电安装必须接地。施工硬约束是 CCA-5 最长 `200 m`、LAN 最长 `100 m`、屏蔽型 5e 类线、IEEE802.3af PoE 集线器。所有连接设定都在工程师模式中配置。

MCS 编址有一条可复算的规律（第 7 / 19 页）：MSU-1500 = `192.168.0.201`（主设备），CCU n ↔ `192.168.0.n`，RCP m ↔ `192.168.0.(100+m)`，各 RCP 的主机 IP 均填主设备 `192.168.0.201`，RCP 编号 = MSU 上的摄像机选择编号。

> "更改连接模式 (CNS) 后,需重启所有摄像机系统。"（第 5 页）

**什么时候会失效**：PC 控制模式的**面板侧配置步骤手册未给**——原书只给了编址示例，CNS 画面里没有 PC 控制配置入口，必须查 HZC-RCP5 的文档。此外组网拓扑大量依赖图示，纯文字只能保留可文字化的规则。

→ 深入: [`network-setup`](./references/capabilities/network-setup.md)

### 主机侧：CABLE TYPE 是四取值、五拓扑

CCU 侧对应的是"摄像机怎么接进来"。`CABLE TYPE` 只有四个取值（`FIBER CAMERA CABLE`、`COAX`、`COAX(HDCE)`、`SINGLE-MODE FIBER`），但连接示例共五种——因为 `FIBER CAMERA CABLE` 这一档在 HDCU5000/5500（连 HDC5000/5500）与 HDCU3500（连 HDC3500/3100/HDC2000）上是两套不同拓扑。**CABLE TYPE 是系统模式开关，不是物理线缆名**：它决定 `FIBER TRANSMIT RATE` 是否可选（选 `COAX`/`COAX(HDCE)` 时该速率固定显示 `---`），进而派生后面全部输出 / 返回格式。

前置条件链顺序不可颠倒：先核对摄像机型号与 CCU 型号的兼容关系（HDCU5000/5500 ↔ HDC5000/5500；HDCU3500 ↔ HDC3500/3100/HDC2000 系列）→ 再看需要哪些选件才能成立（光纤连 HDC5000/5500 在 HDCU3500 上必须装 HKCU-FB50；单模光纤必须装 HKCU-SM50 且配 HDCE-100 适配器；IP 传输必须装 HKCU-SFP50 并接 SFP+/SFP28 模块）→ 然后才设 CABLE TYPE → 最后设 FIBER TRANSMIT RATE（`ULTRA` = 连 HDC5000/5500 或装 HKC-FB50 的 HDC3500；`HIGH` = 连 HDC3500（未装 HKC-FB50）/HDC3100/HDC2000 系列）。

距离上限随型号分档：光纤传输 HDCU5000 约 `4 km`、HDCU5500 约 `2 km`、HDCU3500 约 `2 km`；单模光纤最长 `10 km`。手册两次声明"实际传输距离和拍摄格式可能视摄像机的系统配置和使用的光纤电缆的类型而不同"——上限是理想值，不是施工保证值。同轴路径还有一条容易被忽略的约束：**CCU 不为摄像机供电**，"需要适合摄像机的专用电源 (外部直流电源)"（第 7 页）。

**什么时候会失效**：单模光纤有硬兼容红线——HKCU-SM50 明令"只能用于连接 HDC3500/3100 和 HDC2000 系列摄像机。不能连接 HDC5000/5500"（第 15 页），"想拉 10 km 又想连 4K 机"直接冲突。光纤接口不接时必须盖盖，端面灰尘会造成传输错误。

→ 深入: [`ccu-transport-setup`](./references/capabilities/ccu-transport-setup.md)

---

## 二、信号的派生链：四个开关决定一切

### 四个开关，派生所有格式

主机侧的信号能力由四个开关共同决定：`CABLE TYPE` + `FIBER TRANSMIT RATE` + `SYSTEM` + `CAMERA FORMAT`。其中 `SYSTEM` 取 `1.001(525)` 或 `1.000(625)`（59.94 / 50 两大场频体系），决定格式查表翻哪一页；`CAMERA FORMAT` 的候选集则**完全不同地**依赖 (FIBER TRANSMIT RATE × SYSTEM)：`ULTRA` × `1.001(525)` 能直接选 `3840×2160/59.94P` 等原生 4K 格式（共 15 项，含 8 个 HFR 项），而 `HIGH` × `1.001(525)` 只有 `UHD/59.94P (4K/HDR)`、`1080/59.94P (4K/HDR)` 这类由 HD 上转换的格式（共 12 项）。手册明确"可供选择的格式视连接的摄像机的有效格式而不同"——候选表是**上限**，实际可用子集取决于所连摄像机。

几条关键联动必须记住：`BIT DEPTH`（`10BIT`/`12BIT`）只在 CAMERA FORMAT 落在六个 `(RGB444)` 项之内时才可选；`CCU VIDEO CONVERT` 一旦设为 `ENABLE`，**必须**把返回信号的 `FRAME SYNCHRONIZER` 设为 `ON`；当 FIBER TRANSMIT RATE 为 `ULTRA` 时，`NETWORK TRUNK` 被**固定**为 `NETWORK+VIDEO`（第 75 页），改不动。4K 能力还分两层："4K 传输"（HKCU-FB50 提供）与"4K 输出"（需 HZCU-UHD35）是两件事，只装 FB50 不等于能出 4K。

**什么时候会失效**：`(FIBER TRANSMIT RATE, SYSTEM)` 一旦定死，输出 / 返回格式的候选页也就唯一确定了（`HIGH`×`1.001(525)`→第 54 页；`HIGH`×`1.000(625)`→第 56 页；`ULTRA`×`1.001(525)`→第 58 页；`ULTRA`×`1.000(625)`→第 63 页）。现场"按查表结果拿不到想要的格式串"，第一反应应是回上游核对这两个开关，而不是去改查表方式。

→ 深入: [`ccu-system-format`](./references/capabilities/ccu-system-format.md)

### 两张独立矩阵，一个"不可自由填"的口径

输出与返回是**两套独立的表**，不要混。输出矩阵在 S07–S11：OUTPUT FORMAT1（SDI-OUT1-4）、OUTPUT FORMAT2（SDI-I/O1-4）、OUTPUT FORMAT3（UHD-SDI A-D）、OUTPUT FORMAT4（UHD-SDI E-H，仅装 HKCU-SDI50）、OUTPUT FORMAT IP（IP-OUT1-4，仅装 HKCU-SFP50）。返回矩阵在 S12–S16：先在 `RETURN SELECT` 把 RET1-8 各自指定到某个物理返回口，再到对应的 `RETURN FORMAT` 项设该口格式——**返回侧的顺序是"先分配、再查表"，与输出侧不同**。

核心口径只有一句：**格式不是自由设定的，是查表结果**。所有 FORMAT 项在菜单里都只写"请参阅第 54/56/58/63 页"。你不能手输一个表外的格式串——举例：CAMERA FORMAT=`1080/59.94I(2×)` 在 `HIGH`×`1.001(525)` 下，SDI-OUT1 列给的是 `1080/59.94I(2×)/Link1`（分链路），SDI-OUT2 列给的是 `1080/59.94I(2×)/Link2`（第 55 页）。同一格式在相邻两个口上被拆成不同 Link，这是表结构决定的。理解了这一点，就不会在"某口出不了目标格式"时误以为是菜单故障。

伴随项也有纪律：`MONITOR` 多数口固定为 `C`（SDI-OUT1/2、SDI-I/O1-4、UHD-SDI A-H、IP-OUT1、IP-OUT4），只有 SDI-OUT3/4、IP-OUT2/3 可选 `C`/`M`；`OETF` 的取值集合随接口变化——SDI-OUT / SDI-I/O / IP-OUT 取 `SDR`/`HDR OETF`，而 UHD-SDI 各口取 `SDR`/`4K OETF`，**UHD-SDI 上没有 "HDR OETF" 这个选项**。

**什么时候会失效**：UHD-SDI A/B 是专用输出，**无法配置返回格式**；4K 四链路接线是否接对，靠 V01 的 `2SI DIAMOND MARK` 自检——开启后若链路 1 到 4 连接正确，4K 颜色条右下角会显示 `OK`，否则不显示。另外，**HFR 施工接线的 Link 分配依据不完整**（见文末缺口清单）。

→ 深入: [`ccu-format-lookup`](./references/capabilities/ccu-format-lookup.md)

---

## 三、HDR 与同步：两个容易混的"域"

### HDR 不是一个概念，是两个域

`LIVE HDR` 不是"高动态范围"泛称，而是 Sony 的**同步双输出机制**：同一台摄像机在 LIVE HDR 下同时输出 HDR 与 SDR 两路，CCU 对两路各自做设置。它的使能闸门是 `HDR MODE` 设为 `LIVE HDR`——`SDR GAIN`（`–15 至 0.0`、`0 dB`）、`HDR CONTRAST`（`100 至 560%`）、`HDR BLACK OFFSET`（`–99 至 99`、`0`）三项**仅在 LIVE HDR 模式下启用**。

这里有两个最容易设错的地方。其一，`SDR GAIN` 是"总闸"，`HDR CONTRAST` 是"读数"——后者标注"仅显示"，其值"通过设置 SDR GAIN 维持"，你调的是 SDR GAIN，对比度读数随之变化，它**不是独立可调项**。其二，`4K COLOR SPACE` 在 LIVE HDR 下被**强制跟随** `HDR COLOR SPACE`（第 35 页"设置与 HDR COLOR SPACE相同"），不要在 LIVE HDR 下试图把两者设成不同值。

更关键的是一条跨书缝：**面板侧与主机侧各有一个 HDR 域**。面板侧是 `HDR Conversion`（SDR→HDR 转换）与 `HDR Operation`，作用在**摄像机图像**；主机侧是 `LIVE HDR` / `OETF` / `COLOR SPACE`，作用在 **CCU 输出与返回信号**。两侧的 `SDR GAIN` / `HDR CONTRAST` / `HDR BLACK OFFSET` **同名但分属不同域**，不可互推。现场遇到"HDR 参数设了但画面不对"，应先确认摄像机侧状态，再回查 CCU 侧参数。

**什么时候会失效**：`LIVE HDR` 下 **HDR 输出不支持某些绘制功能**（手册未列明具体缺哪些，不得编造）；想用 720 返回就得放弃 HDR（`*3` 前置要求"CCU VIDEO CONVERT 设为 ENABLE **并且**所连摄像机的 HDR 模式设为 OFF"）；格式串中标注 `(RGB444)` 的项在返回表里一律标 `(SDR)`，即 RGB444 与 HDR 不共存。

→ 深入: [`ccu-hdr-setup`](./references/capabilities/ccu-hdr-setup.md)

### 同步来源三选一，且与传输方式绑定

本机的时间基准从哪来、相位怎么对齐，由 `GENLOCK MODE` 的三选一决定：`HD`、`SD`、`NETWORK`，三者互斥，选错就是"锁不上"或"整系统不同步"。`NETWORK` 这一项**仅在安装了 HKCU-SFP50 网络接口板时才会显示**；且在 SMPTE ST 2110 兼容系统中运行时**必须**设为 `NETWORK`——此时不需要 REFERENCE IN 接口的外部参考输入，同步改由 HKCU-SFP50 的 LAN 1 和 LAN 2 接口承载。`REFERENCE` 菜单项本身只是"REFERENCE IN 接口的信号输入（仅显示）"，是**检测结果，不是你可以设的参考源类型**。

HD/SD 路径的参数集里有两个坑：`10F BB`（是否使用添加到外部参考信号的 10 场 ID）**只有 GENLOCK MODE 为 SD 且 SYSTEM 为 1.001(525) 时才可选**；`H-PHASE STEP` 的范围**随 GENLOCK MODE 变化**——HD 时 `–3.01 至 3.45 微秒`、SD 时 `–8.29 至 9.48 微秒`（默认均为 `0.00`）。而且手册把"步长"命名为 `STEP`、把"精细调整"命名为 `COARSE`，**命名与直觉相反**。

NETWORK 路径（PTP）在 `<NETWORK GENLOCK>`（N04）与 `<PTP STATUS>`（N05）两页，**二者仅在安装 HKCU-SFP50 时显示**。`PROFILE` **仅支持 ST2059-2 配置文件**；`DOMAIN NUMBER` 取 `0 至 127`、默认 `127`，必须设为要连接的主站设备的域编号。PTP 的锁定判读有两套同名但不同取值的东西：GENLOCK 选 HD/SD 时 `LOCK STATUS` 只有 `LOCKED`/`NOT LOCKED`，而 N04 的 PTP `LOCK STATUS` 是四态 `NOT IN USE`/`NO MASTER`/`LOCKING`/`LOCKED`，不可混用。

**什么时候会失效**：PTP 依赖 LAN1/LAN2 链路，而 LAN1 与 LAN2 的链路速度**必须相同**（第 79 页），否则"无法进行正常操作"并可能报 `CCU:LINK SPEED MISMATCH`——同步问题因此可能实际是链路速度问题。此外 `REFERENCE OUT` 原样输出输入信号（环路），不使用环路输出时须在 `75 欧姆` 端接，端接缺失会破坏参考信号质量，是"锁不上"的常见物理原因。

→ 深入: [`ccu-genlock-sync`](./references/capabilities/ccu-genlock-sync.md)

---

## 四、权限与控制权：谁能动、动哪一层

### 面板侧：控制权先行

多台面板共享同一批摄像机时，谁说了算？MCS 靠"两层许可 + 一个仲裁者"维持秩序。**整机层**：`PANEL ACTIVE` 灯亮 = 本面板独占该摄像机的操作权，全系统同时只有一台激活，其余面板只显示数值。**光圈/主黑层**：`IRIS/MB ACTIVE` 是第二层独立许可，这一层被某台面板独占时，`PARA`（并行控制）不可用。**PARA** 是并行通道：未激活面板按 PARA 即加入，适合多岗位协作。**仲裁者**是主设备（MSU-1500/1000 或 CNA-1）——主设备一断开，常规激活全部失效。

最反直觉、也最有价值的一条冷知识是主设备掉线后的应急路径：

> "如果 MCS 模式系统的主设备断开, 则不可实现面板激活操作。在这种情况下,长按 PANEL ACTIVE按钮将强制激活面板。"（第 15 页）

还有一条容易踩的边界：主/从白平衡是 CNU 旧有连接的遗留功能，"LAN 连接不可用"——在 BRIDGE/MCS 组网下反复找这个开关是白费力气。

**什么时候会失效**：强制激活绕过主设备仲裁，多人同时长按会争抢控制权；**强制激活后主设备恢复流程原书未述**，这是明确的缺口。

→ 深入: [`mcs-operations`](./references/capabilities/mcs-operations.md)

### 面板侧：先查权限，再查故障

"Category Select 里怎么都找不到 File / Maintenance / Paint 菜单"——这大概率不是设备缺功能，是权限。**工程师模式**是这台面板的"管理员层"：时钟、连接、安全限制、自定义、备份、初始化等十类设定全藏在这层后面，File/Maintenance/Paint 三个整个菜单也只在其中显示（路径 `MENU > Config > RCP > Security > [Engineer Mode]`）。所以"找不到菜单/找不到设定项"的第一反应应该是查权限。

三层防误操作结构：①工程师模式门（可加安全代码保护）；②**Page Permission**（整机级：Full Lock 全锁 / View Mode 只读 / Full Paint 开放 Paint）；③**Item Permission**（功能级：APR、参考文件、镜头文件、OHB 文件、Crop、Knee Max、SW 菜单七项逐个开放）。安全代码的应急入口值得记住：按住 `PARA`、`MASTER` 和 `CUSTOM PAINT` 按钮的同时打开控制面板，输入 `0359` 进入 Engineer Protection 画面。

**自定义配置**是工程师模式下的"提效层"：SW Customize 给自由按键派功能，Assignable Knob 给旋钮派功能，Custom Menu SW 给 CUSTOM1-5 派着色菜单项。三者共用同一条铁律——**未按完两段 Save 就退出 = 全部白做**；另有顺序依赖：22 个受限着色项目必须**先在 Menu Customize 里记录，再配置 CUSTOM1-5**，顺序反了不成立。

**什么时候会失效**：**Full Lock 误启用后无原文解除路径**（手册未说明如何回到 Security 画面，属待核查缺口）；`0359` 既是万能入口也是安全弱点——任何知道三键组合的人都能解除代码，手册未讨论此风险；输错安全代码的表现原书未述。

→ 深入: [`engineer-mode-security`](./references/capabilities/engineer-mode-security.md) ｜ [`customization`](./references/capabilities/customization.md)

---

## 五、资产与日志：两套互不覆盖的落盘通道

### 面板侧：场景文件与 USB 备份是两条通道

**场景文件**是摄像机侧的图像参数套装，面板上最常用：STORE 按钮本质是"写入模式开关"——它闪烁时按编号 = 把当前状态写进该号（**覆盖**！），不闪烁时按编号 = 读取；编号 1-5 有独立灯可直达，6 号及以后编号灯不亮是设计行为，要走 EXPAND 显示（容量上限 32 个）。**USB 备份**是面板侧的设定资产，分两类且互斥：`[RCP Config]` = RCP 自定义设定（**不包括网络设定**），`[Network Config]` = 网络设定。完整换机必须两类各备一次，只备一类 = 丢另一半。

编号是唯一防线——选择已存在的文件编号保存，"则会覆盖其数据"，**没有回收站、没有二次警告**。备份文件的时间戳取自面板内部时钟，所以校时是备份可信度的一部分。

**什么时候会失效**：备份文件的**跨面板、跨固件格式兼容性原书未述**；场景文件的内容项"视所连接的摄像机而异"，跨机型直接互调同一编号得到的参数集不同；场景文件不在 RCP USB Backup 的 `[RCP Config]` 内，要落 U 盘得走 File>Scene Transfer。维护侧还有一条硬提醒：Shading 校正后必须 Store 到 OHB 文件，否则"在摄像机断电时不会进行保存"。

→ 深入: [`scene-files`](./references/capabilities/scene-files.md) ｜ [`file-backup`](./references/capabilities/file-backup.md) ｜ [`maintenance-correction`](./references/capabilities/maintenance-correction.md)

### 主机侧：CCU FILE 与 LOG，两条不对称的通道

CCU 的"资产"也分两类，各自有独立存取通道，混用会出事。第一类是 **CCU 文件（CCU FILE）**：本机全部菜单设置的一张快照，存在本机内存里，**最多五个**（FILE INDEX 1 至 5）。第二类是 **日志（LOG）**：最多保存 **30 天**，超期从最旧的开始删。

最容易被误判的一条铁律：**RECALL 不会加载 LAN COM 接口的 IP 地址、子网掩码和默认网关设置**。也就是说换机恢复时，用 CCU 文件能还原几乎所有菜单设置，唯独 LAN COM 的三项网络参数必须**另外手工重配**。这条不对称性（STORE 存整机、RECALL 少网络）是换机 / 故障恢复时最容易漏掉的一步。第二条硬风险来自日期时间：**更改 DATE&TIME 会删除本机上存储的所有日志**（第 76 页 M04 明文）——不是"可能影响"，而是"更改即清空、不可逆"，正确顺序永远是"先 EXPORT TO USB 导出日志 → 再改日期时间"。

USB 路径是固定约定：CCU 文件与日志的 EXPORT/IMPORT 都落在 USB 闪存驱动器上的 `/MSSONY/PRO/CAMERA/HDCU5000`，三型号共用同一字符串。

**什么时候会失效**：**两套资产对象完全不同、互不覆盖**——RCP 文件管"画成什么样"，CCU 文件管"机器怎么配"，两侧各有 USB 备份通道但内容不相交，换机恢复必须两套都做。此外手册**未说明** CCU 文件的跨型号 / 跨固件兼容性，也未给出 RECALL 失败时的排查步骤。

→ 深入: [`ccu-file-log`](./references/capabilities/ccu-file-log.md)

---

## 六、排障：两端各看什么

### 灯语诊断：先分层、再查表、后转介，且两端同名不同义

面板侧与主机侧各有一套观测面，判读方法都是"**先分层、再查表、后转介**"：把观察到的灯态归属到某一层，再查该灯的状态→含义，最后把处置动作转给对应的能力卡。

**同名不同义是最大的陷阱。** 两端都有 `NETWORK` 与 `ALARM` 灯，判读体系却完全不同：面板侧的 `NETWORK` 管"本机与控制设备的连接"（亮=与控制设备相连；闪烁=无法找到控制设备；熄灭=无法与摄像机网络相连，或模式为 LEGACY），主机侧的 `NETWORK` 管"PTP 网络同步锁定状态"（低速闪烁=未检测到 PTP 主站；高速闪烁=正在锁定；点亮=已锁定；不点亮=禁用网络同步锁定设置）。同一个"NETWORK 闪烁"，在面板上是控制链路问题，在主机上是 PTP 同步问题，**排查方向完全相反**。面板侧的 `ALARM` 是红/绿/黄闪四态（红=受控设备错误；绿=本机启动；黄闪=本机错误 / 不支持的 USB 设备 / 时间设置不正确；灭=正常），主机侧的 `ALARM` 只有"亮/灭"（亮=发生各种错误，明细读状态画面 Alarm 页）。

报故障之前必须先排三类"不是故障"：LEGACY 模式下 NETWORK 熄灭属正常；面板权限态（`PANEL ACTIVE`/`PARA` 双灯全灭只是没控制权）；LCD 坏点与 CCD 白点是物理特性。主机侧还有一条跨书要点：`CABLE ALARM` 亮起（无论 `OPEN` 还是 `SHORT`）**都不会对摄像机供电**——摄像机无电时先看这个灯，而不是先怀疑摄像机本身。

**什么时候会失效**：两端手册都只有"状态→含义"的灯语表，**没有"现象→原因→处置"完整决策树**——比如 `CABLE ALARM` 的 `SHORT` 态、多数 `CCU:XXX` 错误消息都只给现象、不给处置。本卡只能给"下一步查哪里"与"转哪张卡"，绝不编造处置流程。

→ 深入: [`led-diagnostics`](./references/capabilities/led-diagnostics.md) ｜ [`ccu-panel-diagnostics`](./references/capabilities/ccu-panel-diagnostics.md)

### 状态画面：11 页的"体检面板"与固定页序

主机侧还有一层比灯更细的观测面：状态画面共 **11 页**（System Status / Multi Format1-4 / Multi Format IP / Audio / Intercom / Network / IP Stream / Alarm）。进入方式是前面板 `DISP/MENU` 控制杆拨到 DISP 位置，转动 `CONTROL` 旋钮换页。接监视器有前置条件：必须经 CHARACTER、SDI OUT 3 或 SDI OUT 4 接口输出；若用 SDI OUT 3/4，必须先把 `MONITOR` 设为 `M`。

判读有两个通用约定：①**摄像机未连接时各项目显示 "-"**，`Reference` 未输入参考信号时显示 "Not Detected"——这些是"未连接/未输入"约定，**不是故障**；②部分页依赖选件才显示（UHD-SDI 页仅装 HKCU-SDI50 时出现；Multi Format IP、Network、IP Stream 页仅装 HKCU-SFP50 时出现），"看不到某页"往往是选件未装，不是故障。

**什么时候会失效**：手册**未给出**"某字段出现异常值时应如何处置"的步骤，状态画面只提供"读值 / 读状态"；Alarm 页条目本身也无处置，须交叉第 88 页错误消息表。

→ 深入: [`ccu-status-screen`](./references/capabilities/ccu-status-screen.md)

---

## 七、装机与联调：把两端对齐

### 投运顺序、重启范围与两端一致性

整系统能不能通，必须同时核对两端。物理连接上，控制信号走 CCA-5 专线：RCP 侧 `CCU/CNU REMOTE` 接口（8 芯）↔ CCU 侧 `RCP/CNU` 接口（圆形 8 芯）。一致性有三条硬要求：两侧的 CNS MODE 必须同值；RCP 侧"主机 IP 地址"就是 CCU 侧 `MASTER IP ADDRESS`；RCP 编号与 CCU NO 必须全系统唯一且对应。取值域还不同：CCU NO 在 MCS 下只能 `1 至 96`，LEGACY/BRIDGE 下可 `1 至 96` 或 `A 至 Z`（CCU 第 79 页）——**编号规划以 CCU 侧取值域为准**。

投运顺序建议：先物理（线、供电、接地）→ 再 CCU 侧系统配置 → 再面板侧 CNS/IP/编号 → 最后统一重启。重启范围要分清：RCP 侧改 CNS 要求"重启所有摄像机系统"；CCU 侧改 IP Live 的 `PORT` 要求"重启本机"。两端都改过就按整系统重启执行——**就大不就小**。

**什么时候会失效**：面板侧"看不到某功能"往往是选件缺失的下游结果（如 HKCU-SFP50 → LAN1/LAN2 + IP Live/NMOS/PTP；HKCU-SDI50 → UHD-SDI E–H，仅 HDCU5000；HZCU-UHD35 → 4K 输出）；两端都改过配置却不重启，会出现新旧配置混杂。

→ 深入: [`system-integration`](./references/capabilities/system-integration.md)

### 联合排障：先定端，再看面

"系统不通 / 画面没信号 / 面板拧不动"——联合排障的本质是"在正确的观测面上读到正确的项，再判断故障落在链路哪一段"：面板↔CCU 是控制链，CCU↔摄像机是信号链，两端灯各管一段。三类典型现象的分诊路径：①"面板拧不动 / 只能看数不能调"→ 看面板 `PANEL ACTIVE` 与 `PARA` 双灯（双灯全灭=无控制权，非故障），MCS 主设备断开 → 长按 PANEL ACTIVE 强制激活；②"画面没信号 / 摄像机没电"→ 看主机 `CABLE ALARM`/`CABLE CONDITION` + 面板 `CABLE`/`CAM PW`，`CABLE ALARM`=`OPEN`/`SHORT` 则光纤链路问题且不供电；③"两端都正常但不同步"→ 看主机 `NETWORK` 灯（PTP）与状态画面 Network 页的 PTP/Ref/LSM。

**什么时候会失效**：两端观测面**互不覆盖**——面板侧看不到主机侧状态画面 / 错误消息，主机侧看不到面板侧权限态，联合排障必须两侧同时观察。RCP 手册无 `CCU:XXX` 错误消息表，CCU 手册无面板 PANEL ACTIVE/PARA 权限态，这是结构性缺口，"另一端查不到"是常态而非遗漏。

→ 深入: [`system-troubleshooting`](./references/capabilities/system-troubleshooting.md)

---

## 陷阱与反例

以下十条是这套系统里杀伤力最大的失败模式，都来自"看起来正常、实则错了"的地方：

1. **把两端的 NETWORK 灯混为一谈**。以为"NETWORK 闪烁"是同一件事 → 实际面板侧指"找不到控制设备"、主机侧指"PTP 未锁/正在锁" → 后果是往完全相反的方向排查。
2. **以为 CABLE ALARM 亮时摄像机该有电**。以为只是提示 → 实际 `OPEN` 与 `SHORT` 两态都"不会对摄像机供电" → 后果是在摄像机端白拆白换，根因在 CCU 侧。
3. **以为 CAMERA FORMAT 是电缆类型 / 格式可以手填**。以为格式项是自由设定 → 实际它是 `CABLE TYPE` × `FIBER TRANSMIT RATE` × `SYSTEM` × `CAMERA FORMAT` 的**派生查表结果**，菜单里只有选择项 → 后果是"某口出不了目标格式"时去改查表方式，而不是回上游核对开关。
4. **以为单模光纤能连 4K 机**。以为"光纤就是光纤" → 实际 HKCU-SM50"不能连接 HDC5000/5500" → 后果是单模通路在 4K 摄像机上根本不存在，方案从采购阶段就错了。
5. **改完 CNS 只重启本面板**。以为重启刚动过的那台就够 → 实际手册要求"重启所有摄像机系统" → 后果是新旧拓扑混杂，系统半通不通。
6. **以为 CCU FILE 的 RECALL 能恢复网络**。以为整机快照一网打尽 → 实际 RECALL **不含** LAN COM 的 IP / 子网 / 网关 → 后果是换机后菜单都对、就是网络不通，得手工补配三项。
7. **以为改 DATE&TIME 只是校时**。以为随手改个日期 → 实际"本机上存储的所有日志都会被删除" → 后果是取证前把 30 天日志一次清空，不可逆。
8. **以为 720 返回随手可选**。以为选了 `CCU VIDEO CONVERT` 就有 720 → 实际返回侧 720 的 `*3` 前置还要求"所连摄像机的 HDR 模式设为 OFF" → 后果是 HDR 与 720 互斥，两个需求同时提必然失败一个。
9. **以为 HDR CONTRAST 可独立调**。以为它是可调对比度 → 实际它标注"仅显示"，由 `SDR GAIN` 决定 → 后果是在一个不响应的项上反复试，真正的旋钮在 SDR GAIN。
10. **把"未连接/未装选件"当故障**。以为状态画面显示 "-"、`Not Detected`、看不到 UHD-SDI/Network 页是坏了 → 实际是未连接或选件未装 → 后果是无谓报修。同理，面板 `PANEL ACTIVE`/`PARA` 双灯全灭只是没控制权，`ULTRA` 下 `NETWORK TRUNK` 改不动是固定值，都不是故障。

---

## 作者的局限（读这套书要打的折扣）

1. **时代局限**：两书均为 **2019 年文档**，支持设备清单止于当时型号（面板侧：HDC-P50/P1、BRC-X1000 等；主机侧：HDC5000/5500、HDC3500/3100、HDC2000 系列）。面板手册提"请使用最新固件"却不含任何固件版本号对照。ST2110 / ST2059-2 支持以 HKCU-SFP50 为前提；SFP+/SFP28 模块型号手册明确"请与 Sony 销售或服务代表联系"，**不含完整兼容列表**。
2. **立场盲点**：两书都**假设读者已具备广播系统常识**（同步、Tally、返送、TBC、PsF、SQD/2SI、SDI 分级），不解释概念本身；连接拓扑与接口位置大量依赖**图示**，纯文本提取会丢失布线细节；菜单全表是**查阅型**内容，只有"设置值 + 说明"，**没有"现象→原因→处置"的完整决策树**；主机侧选件安装被限定为"只有经过服务培训的合格技术人员才能执行"，手册不提供安装步骤。
3. **未被证明 / 需标注的假设**：面板侧安全代码 `0359` 是启用保护的万能入口，遗失自定义代码时的恢复依赖该后门，手册未讨论此安全风险；电解电容 `5 年` 寿命只按"每天 8 小时、每月 25 天"一个工况推算，其他工况无数据。主机侧"带下划线的格式可根据所连接摄像机的 Live HDR 模式设置在 HDR 和 SDR 之间切换"依赖摄像机侧配合，手册未给完整前置条件；DHCP 的"自动 IP"**仅适用于 LAN COM**（此限制只在 N01 说明里出现一次）；LAN1/LAN2 必须设为相同链路速度，否则"无法正常操作"，无容错说明。
4. **四项待复核（手册只使用未定义，或提取不可靠）**：①`PsF` —— 手册未单独定义，仅以格式串出现（如 `1080/59.94PsF`、`1080/59.94I(PsF)`），"Progressive segmented Frame"系行业外部知识，**格式串必须原样保留，不得当 P 处理**；②`SQD / 2SI` —— 手册未展开定义，仅以格式串出现（如 `3840×2160/59.94P/SQD/3G-A`、`3840×2160/59.94P/2SI/3G-A`），全称与像素切分规则含行业常识；③`UHB` —— 手册仅作 "HKCU-FB50 UHB 传输套件"出现，**未展开含义**，不得解读为"超宽带"；④**第 67 页 HFR ↔ BNC Link 编配表** —— 纯文本列对齐丢失（提取为 `4 K 2 × 1 2 G 2 1 6 0 P L i n k - 1` 一类乱码），6× 及 3G-B 半链路的完整 Link 映射**无法确证**，HFR 施工接线依据不完整，须回查原 PDF 图形或向 Sony 确认。
5. **跨书缝（两书各自都不完整）**：**a.** 无统一的"两端编号 ↔ 机位"对照表（面板侧 RCP 编号对应 MSU 机位选择号，主机侧 CCU NO 受 CNS 模式约束，两书都未给出可交叉查表的完整映射）；**b.** "重启所有摄像机系统"的作用域未定义（是否含摄像机头与主机侧、以何种顺序重启，均未说明）；**c.** RCP-3500/3501 的**供电来源两书描述不一致**——主机侧把"经 RCP/CNU 接口供电"只归给 RCP-3000/1000 系列，而面板侧另有 EXT I/O（`10.5–17 V` 直流）与 PoE（IEEE802.3af class 2），施工前须以实际机型确认；**d.** 错误与权限的两端不对称（主机侧有完整的 `CCU:XXX` 错误消息表，面板侧没有；面板侧有 Page/Item Permission 权限状态，主机侧没有对应表）；**e.** 选件 ↔ 能力的映射在每本书里都是单端的，两书都不覆盖"某选件对整套系统的能力增量"。
6. **对蒸馏工作本身的警示**：两书都是**查阅型文本**，大量价值在"精确参数 / 格式串原样可查"（如 `3840×2160/59.94P/12G`、`1080/59.94P(2×)/3G-A`、`CCA-5 200 m`）。因此本文与能力卡里，**数值、单位、格式串、页码、代码一律原样保留、禁止换算**；菜单全表类内容适合做参考索引而非执行卡。

---

## 关键术语速查

| 术语 | 面板侧（RCP） | 主机侧（CCU） | 操作含义 |
|---|---|---|---|
| **CNS / 连接模式** | 四选一：`LEGACY` / `BRIDGE` / `MCS` / `PC 控制`（HZC-RCP5，最多 6 台 RCP）；改 CNS 后须重启所有摄像机系统 | 三选一：`LEGACY` / `BRIDGE` / `MCS`；MCS MODE 为**仅显示**固定值 `CLIENT` | 两侧模式集合不对等，面板侧多一个"PC 控制"；面板选 PC 控制时 CCU 侧如何对应，两书均未给 → 跨书缺口 |
| **CCU 编号 / CCU NO** | "CCU 编号取值 1–96、A–Z" | MCS 时 `空白, 1 至 96`；LEGACY / BRIDGE 时 `空白, 1 至 96, A 至 Z` | 手册侧明确 MCS 下不允许 A–Z；编号规划以 CCU 侧取值域为准，两侧须全系统唯一 |
| **MCS 主设备** | MSU-1500/1000 或 CNA-1 可作主设备 | `MASTER IP ADDRESS`：本机作为客户端去连的主设备 IP | 两侧互补：面板侧回答"谁是主设备"，CCU 侧回答"主设备 IP 填什么" |
| **同步 / GenLock** | 只做**相位微调**：Maintenance > CCU > Phase（含 `SC Phase`） | 决定**参考源与锁定模式**：`HD`/`SD`/`NETWORK` + PTP `ST2059-2` + H-PHASE/V-PHASE | 参考源与模式在 CCU 侧定，面板侧只是遥控相位入口；两侧同名相位项是否互相覆盖属（推断），需现场验证 |
| **返回信号 / RETURN** | `Return Settings`（工程师模式）：Return-1 到 4 的 Input / Aspect / LB Mode / OETF / C Space——**设定格式** | `RETURN SELECT` + `RETURN FORMAT1-4`：定义返回信号来源与**格式矩阵**（p49–53） | 两侧分工不同：CCU 侧矩阵决定每路可用格式，面板侧在此范围内指定取哪路 |
| **文件 / FILE** | **摄像机图像参数**资产：场景文件、参考文件、镜头文件、OHB 文件；USB 备份分 `[RCP Config]` 与 `[Network Config]` | **CCU 整机菜单设置**快照：`CCU FILE` 最多 5 个，`RECALL` **不含** LAN COM 的 IP / 子网 / 网关；`LOG` 最多 30 天 | 对象完全不同、互不覆盖；换机恢复必须两套都做 |
| **HDR** | `HDR Conversion` + `HDR Operation`——作用在**摄像机图像** | `LIVE HDR` / `OETF` / `COLOR SPACE`——作用在 **CCU 输出与返回信号** | 两个不同的 HDR 域；两侧的 `SDR GAIN`/`HDR CONTRAST`/`HDR BLACK OFFSET` 同名但分属不同域，不可互推 |
| **供电（摄像机侧）** | `CAM PW` 四态灯语："从 CCU 向摄像机供电" | `CAMERA FIBER` 一根光纤同时承载电源/控制/视频/音频；**`CABLE ALARM` 亮（OPEN / SHORT）时不会对摄像机供电** | 跨书排障要点：面板侧 CAM PW 按了没反应，可能是 CCU 侧 CABLE ALARM 触发；排障顺序先看 CCU 灯，再看面板灯 |
| **网络接口** | 面板 LAN 口：接 LAN 集线器，缆长 ≤ 100 m；仅用 LAN 连接时必须接地 | 两套口：`LAN-COM`（承载 RCP/MSU 连接、Web 菜单等）；`LAN 1/2`（HKCU-SFP50，SFP+/SFP28）专用于 IP 视频/音频/PTP | 面板接的是 CCU 的 **LAN-COM**，不是 LAN1/LAN2；"自动 IP"仅适用于 LAN COM |
| **Tally / 计数器** | Tally（红/绿/橙）经 EXT I/O 或 CCU 传输；MCS 模式下 EXT I/O 的 Tally 输入被禁用 | `TSL UMD` V5.0（UDP 端口 `8900`）IP 计数器；`INTERCOM/TALLY/IO` 50 芯 D-sub 一口多用 | 面板侧讲信号与线，CCU 侧给协议与物理引脚 |
| **CABLE TYPE** | 无此概念 | 四取值：`FIBER CAMERA CABLE`、`COAX`、`COAX(HDCE)`、`SINGLE-MODE FIBER`（末项仅装 HKCU-SM50 时可选） | 它是四选一的**系统模式开关**，不是物理线缆名；决定 FIBER TRANSMIT RATE 是否可选并派生全部格式 |
| **FIBER TRANSMIT RATE** | 无此概念 | `HIGH`、`ULTRA`、`---`；ULTRA＝连 HDC5000/5500 或装 HKC-FB50 的 HDC3500 | HIGH/ULTRA 是 Sony 私有光纤分级；ULTRA 下把 `NETWORK TRUNK` 锁定为 `NETWORK+VIDEO` |
| **CCU 文件 / 日志** | 面板侧对应 `[RCP Config]` / `[Network Config]` 两类 USB 备份 | `CCU FILE` 最多 5 个；`LOG` 最多 30 天；USB 路径固定 `/MSSONY/PRO/CAMERA/HDCU5000`；改 DATE&TIME 清空全部日志 | 两套资产对象不同；换机恢复须两套都做 |
| **GENLOCK MODE / LOCK STATUS** | 无对应项（只做相位） | `HD`/`SD`/`NETWORK`；`LOCK STATUS` 同名两项取值不同（GENLOCK 为 `LOCKED`/`NOT LOCKED`，PTP 为四态 `NOT IN USE`/`NO MASTER`/`LOCKING`/`LOCKED`） | 同名项两处取值体系不同，不可混用；`NETWORK` 仅在装 HKCU-SFP50 时显示 |
| **H-PHASE STEP / COARSE** | 面板侧有 H / H Step / H Coarse / SC Phase | HD 时 `–3.01 至 3.45 微秒`、SD 时 `–8.29 至 9.48 微秒` | 手册把"步长"命名为 STEP、"精细调整"命名为 COARSE，**命名与直觉相反** |
| **工程师模式 / 权限** | Security 画面开启的隐藏设定层；Page Permission（全锁/只读/Full Paint）+ Item Permission（七开关） | 无对应表；靠菜单锁定开关与"仅显示"项 | 面板侧三层防误操作；主机侧没有对应权限体系（两端不对称） |

---

## 如果只带走三句话

1. **先定层级再动手**：任何"系统不对劲"的问题，先判它是面板侧、主机侧还是链路侧——面板侧管"控制关系与权限"，主机侧管"信号与同步"，否则会在错误的一层反复试。
2. **前置条件链不可越级**：传输方式（`CABLE TYPE` / `FIBER TRANSMIT RATE`）→ 系统格式（`SYSTEM` / `CAMERA FORMAT`）→ 输出 / 返回格式是一条**派生链**，格式是查表结果、不是自由填写；越级设定必然失败。
3. **落盘与重启收尾**：改 CNS 必须重启所有摄像机系统；改 DATE&TIME 会清空全部日志；CCU FILE 的 RECALL 不含 LAN COM 网络三项；Shading 校正必须 OHB Store——不落盘、不重启，等于没做。
