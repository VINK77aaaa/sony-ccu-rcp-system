---
name: sony-ccu-rcp-system
description: |
  Sony 摄像机控制系统（RCP-3500/3501 遥控面板 + HDCU5000/5500/3500 摄像机控制单元）的统一技能入口，蒸馏自 Sony 2019 两本官方使用说明书。覆盖 31 项能力：RCP 侧 13 项（组网连接、MCS 多机仲裁、面板灯语诊断、摄像机日常操作、工程师模式与安全代码、白黑闪光平衡、场景文件、USB 备份、自定义、Paint 图像调整、维护校正、规格速查、环境红线）+ CCU 侧 16 项（传输方式决策、系统格式、输出/返回格式派生查表、HDR、同步 GENLOCK-PTP、网络与 IP、IP Live/NMOS/第三方协议、Web 菜单、CCU 文件与日志、前面板灯语诊断、状态画面判读、DIAGNOSIS 硬件诊断、音频与对讲、干线提示机、本机菜单操作、接口规格环境速查）+ 跨书 2 项（整系统组网与联调、整系统联合排障）。按用户意图路由到对应能力卡执行。
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.sony-ccu-rcp-system
  cangjie.capability-count: 31
  cangjie.entrypoint-count: 1
---
# Sony 摄像机控制系统使用说明书合辑（RCP-3500/3501 遥控面板 + HDCU5000/5500/3500 摄像机控制单元） — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 摄像机（HDC 系列）自身的维修与固件升级操作
- 选件板（HKCU-* / HZCU-*）的物理安装步骤（手册明示仅经培训人员可执行）
- 其他型号遥控面板或 CCU 的专属操作
- 书摘/读后感/作者人设扮演

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 数值与格式串零改写：规格、接口、格式串、页码、代码一律原样回报，禁止换算或四舍五入
2. 先定层级再动手：系统级问题先判"面板侧 / 主机侧 / 链路侧"，再进对应能力卡
3. 两端一致性：RCP 与 CCU 的 CNS 模式、CCU 编号、主设备 IP 必须一致且全系统唯一
4. 前置条件链：传输方式 → 系统格式 → 输出/返回格式是派生链，越级设定必然失败
5. 选件门槛先核：菜单项是否存在取决于是否安装 HKCU-SFP50/SDI50/SM50 或 HZCU-UHD35/CNFG50/SNMP50
6. 手册留白诚实转介：多处"请联系 Sony 维修代表或销售代表"，未载内容标注缺口不编造
7. 不可逆操作先警示：改 CNS 需重启所有摄像机系统；改 DATE&TIME 会清空全部日志

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 把 RCP 接入摄像机系统并选定组网模式（LEGACY/BRIDGE/MCS/PC 控制）；配置面板 TCP/IP、目标 IP、主设备 IP 与 RCP 编号；判断安装是否需要接地、布线是否合规格；组网变更后按铁律收尾投用（重启所有摄像机系统）；规划 MCS/PC 控制的 IP 编址与编号唯一性 | references/capabilities/network-setup.md | references/capabilities/mcs-operations.md、references/capabilities/engineer-mode-security.md、references/capabilities/led-diagnostics.md、references/capabilities/specs-reference.md |
| 判断"面板能看到值但拧不动"的原因并取得控制权；多面板并行控制同一摄像机（PARA）；独占或切换光圈/主黑电平控制（IRIS/MB ACTIVE）；用 RCP Assign 更换本面板受控摄像机；主设备（MSU/CNA-1）断开后的应急操作（强制激活）；判断主/从白平衡是否可用及冲突归属 | references/capabilities/mcs-operations.md | references/capabilities/network-setup.md、references/capabilities/daily-operation.md、references/capabilities/white-black-balance.md、references/capabilities/customization.md |
| 判读指示灯状态含义（CAM PW/NETWORK/ALARM/CABLE）；从面板给摄像机供电/断电并判断供电状态；定位故障层级（电源/网络/链路/设备）；甄别伪故障（LEGACY 正常态、权限态、兼容性、坏点白点）；处理"监视器一直出彩条"类信号输出异常（BARS 优先） | references/capabilities/led-diagnostics.md | references/capabilities/network-setup.md、references/capabilities/environment-care.md、references/capabilities/maintenance-correction.md、references/capabilities/daily-operation.md、references/capabilities/file-backup.md |
| 查整机规格参数（电源/PoE/功耗/温度/质量/机架）；查电缆长度上限与 LAN 线材规格；查 EXT I/O 接口针脚分配与接口选件型号；查电解电容寿命口径（基准工况）；核对既有接入参数是否超规 | references/capabilities/specs-reference.md | references/capabilities/network-setup.md、references/capabilities/environment-care.md |
| 判断冷凝等环境风险并处置；按手册方法清洁触控面板；制定电容更换/维护计划的寿命口径；接入网络前确认网络安全；选址避开医疗设备与电磁干扰源；每日投入使用前确认运行正常 | references/capabilities/environment-care.md | references/capabilities/led-diagnostics.md、references/capabilities/network-setup.md、references/capabilities/specs-reference.md、references/capabilities/maintenance-correction.md |
| 执行/中止 AWB、ABB、LEVEL、SKIN DTL AUTO HUE 自动调整；调节光圈、快门、增益并读懂指示灯；切换 ND/CC 滤镜并夺取控制许可；选择彩条/测试信号输出；判断变焦/对焦控制权归属（面板 vs 机身） | references/capabilities/daily-operation.md | references/capabilities/white-black-balance.md、references/capabilities/mcs-operations.md、references/capabilities/led-diagnostics.md、references/capabilities/paint-adjustment.md、references/capabilities/maintenance-correction.md |
| 手动调节白平衡（WHITE 旋钮 RGB 按序）；手动调节黑平衡与闪光平衡（BLACK/FLARE 双用途切换）；判断/恢复 ABSOLUTE 绝对值与相对值模式；评估主/从白平衡联动的可用性（CNU vs LAN） | references/capabilities/white-black-balance.md | references/capabilities/daily-operation.md、references/capabilities/paint-adjustment.md、references/capabilities/scene-files.md |
| 注册（存储）当前参数到场景文件；读取场景文件（含 6 号以上 EXPAND 通道）；恢复访问前状态/取消注册待命；设定读取时的 Dissolve 渐变与速度 | references/capabilities/scene-files.md | references/capabilities/file-backup.md、references/capabilities/white-black-balance.md、references/capabilities/paint-adjustment.md |
| 将 RCP 设定备份到 USB 驱动器；从 USB 恢复/删除备份文件；执行 All Preset 全量初始化；校准内部时钟以保证备份时间戳可信 | references/capabilities/file-backup.md | references/capabilities/scene-files.md、references/capabilities/engineer-mode-security.md、references/capabilities/customization.md、references/capabilities/maintenance-correction.md |
| 向自由按键/旋钮分配功能（SW Customize / Assignable Knob）；编辑自定义着色菜单并向 CUSTOM1-5 分配项目；自定义状态画面版式与 Knob 1-4 功能；更改调节旋钮灵敏度（VR Setting）；排查"分配改了但不生效" | references/capabilities/customization.md | references/capabilities/engineer-mode-security.md、references/capabilities/file-backup.md、references/capabilities/daily-operation.md、references/capabilities/paint-adjustment.md |
| 进入/退出工程师模式（含已设码分支）；设置/更改/删除安全代码，接手无码或遗忘码的面板；配置 Page Permission 与 Item Permission 防误操作；判断某设定是否属于工程师模式清单；排查"菜单不见了/选项不显示"的权限原因 | references/capabilities/engineer-mode-security.md | references/capabilities/network-setup.md、references/capabilities/customization.md、references/capabilities/paint-adjustment.md、references/capabilities/file-backup.md |
| 按画面问题定位 Paint 菜单项与调节方向；调肤色细节（Skin DTL 三通道/Auto Hue/Gate）；调细节锐度与降噪的权衡（Detail/Crispening/Noise Suppression）；调高光/暗部（Knee/Auto Knee/White Clip/Black Gamma）；整体色彩还原（User/Preset/Multi Matrix）与伽马曲线选择；HDR 输出与实时色调控制 | references/capabilities/paint-adjustment.md | references/capabilities/white-black-balance.md、references/capabilities/maintenance-correction.md、references/capabilities/customization.md、references/capabilities/daily-operation.md |
| 执行 Black/White Shading 校正（自动/手动 SAW-PARA）并落盘 OHB；RPN 白点手动校正（先 ABB 后 RPN）；自动白色色差模式选型（RGB vs RB Only）；调整自动光圈参数（Level/APL Ratio/Iris Gain/Pattern）；切换变焦/对焦控制权（Zoom/Focus Active）；配置校正作业的监视联动（PIX/WF Synchro） | references/capabilities/maintenance-correction.md | references/capabilities/paint-adjustment.md、references/capabilities/led-diagnostics.md、references/capabilities/file-backup.md、references/capabilities/daily-operation.md |
| 把 CCU 接进摄像机系统并选定传输方式（光纤/IP/单模光纤/同轴/同轴-HDCE）；判断需要装哪块选件板（HKCU-FB50/SDI50/SFP50/SM50）；核算光纤与同轴的最大传输距离；配置 <CAMERA I/F> 与 <VIDEO I/O> 的必配菜单项 | references/capabilities/ccu-transport-setup.md | references/capabilities/ccu-system-format.md、references/capabilities/system-integration.md |
| 设置系统工作频率与摄像机信号格式；判断某 CAMERA FORMAT 在当前 SYSTEM 与速率下是否可选；配置 BIT DEPTH、CCU VIDEO CONVERT、延迟与 4K 输出选件 | references/capabilities/ccu-system-format.md | references/capabilities/ccu-format-lookup.md、references/capabilities/ccu-hdr-setup.md |
| 查某接口（SDI-OUT/SDI-I/O/UHD-SDI/IP-OUT）能输出什么格式；查某返回选择（SDI-RET/UHD-SDI/IP-RET）对应什么格式；理解格式派生机制与四张格式表的分流规则；用 2SI DIAMOND MARK 自检 4K 链路接线 | references/capabilities/ccu-format-lookup.md | references/capabilities/ccu-system-format.md、references/capabilities/ccu-transport-setup.md |
| 开启/关闭 LIVE HDR 拍摄模式；选择 HDR OETF（S-Log3 / HLG）与色彩空间；配置 SDR GAIN、HDR CONTRAST、HDR BLACK OFFSET、HDR LOOK；判断某输出格式能否在 HDR/SDR 间切换 | references/capabilities/ccu-hdr-setup.md | references/capabilities/ccu-system-format.md、references/capabilities/ccu-format-lookup.md |
| 选择外部参考锁定模式（HD/SD/NETWORK）；配置网络同步 PTP（域号、通信模式、延迟请求间隔）；调整 H-PHASE/V-PHASE 与 SYNC OUT；判读 LOCK STATUS 与 PTP STATUS | references/capabilities/ccu-genlock-sync.md | references/capabilities/ccu-network-setup.md、references/capabilities/ccu-ip-live.md |
| 配置 LAN-COM / LAN1 / LAN2 的 IP、子网掩码与默认网关；设定 CNS MODE、CCU 编号与 MASTER IP ADDRESS；用 PING 做网络连通性诊断；判断 DHCP/自动 IP 的适用范围与链路速度约束 | references/capabilities/ccu-network-setup.md | references/capabilities/ccu-genlock-sync.md、references/capabilities/system-integration.md |
| 配置 IP Live System Manager（主/备 IP、连接状态、多播地址、HITLESS FAILOVER）；配置 NMOS IS-04/IS-05 与 RDS 发现；配置 Ember+、SNMP/SNMP TRAP、TSL UMD；判断各协议的前置选件与互斥关系 | references/capabilities/ccu-ip-live.md | references/capabilities/ccu-network-setup.md、references/capabilities/ccu-genlock-sync.md |
| 访问并操作 Web 菜单（远程配置与监控）；启用 CCU 信息列表与服务发现；用 Web 菜单做版本升级、许可证、日志下载、重启；排查 Web 菜单打不开或布局错乱 | references/capabilities/ccu-web-menu.md | references/capabilities/ccu-menu-operation.md、references/capabilities/ccu-network-setup.md |
| 保存/读取 CCU 文件（最多 5 个）；通过 USB 导出/导入 CCU 文件与日志；命名与清除 CCU 文件；判断 RECALL 不覆盖哪些设置、日志的保存期限与清空风险 | references/capabilities/ccu-file-log.md | references/capabilities/file-backup.md、references/capabilities/ccu-menu-operation.md |
| 看 CCU 前面板指示灯判断故障层级；查错误消息表（CCU:XXX POWER/PLD/TEMP/FAN/CABLE/GENLOCK…）含义；判断摄像机供电、光纤电缆、风扇、同步状态；区分"主机侧告警"与"面板侧告警" | references/capabilities/ccu-panel-diagnostics.md | references/capabilities/ccu-status-screen.md、references/capabilities/ccu-diagnosis-menu.md、references/capabilities/system-troubleshooting.md |
| 显示并翻页查看 11 个状态画面；判读系统状态、格式、音频、对讲、网络、IP 流、告警；配置状态画面显示哪些摄像机设置项；区分"未连接占位符"与真实故障 | references/capabilities/ccu-status-screen.md | references/capabilities/ccu-panel-diagnostics.md、references/capabilities/ccu-diagnosis-menu.md |
| 查板卡自诊断结果与累计开机时间；查型号、序列号与各软件/PLD 版本；查电源单元与风扇运行状态；查所连摄像机的型号与 ROM 版本 | references/capabilities/ccu-diagnosis-menu.md | references/capabilities/ccu-panel-diagnostics.md、references/capabilities/ccu-status-screen.md |
| 设定摄像机麦克风增益与音频输出电平；配置生产商/工程师对讲接口与侧音；配置前面板对讲（麦克风类型、增益、PGM 混音）；发送测试音与配置 IP 音频/对讲格式 | references/capabilities/ccu-audio-intercom.md | references/capabilities/ccu-trunk-prompter.md、references/capabilities/ccu-specs-reference.md |
| 配置串行 TRUNK 通道模式与接口类型；配置提示机通道数；配置 NETWORK TRUNK 模式与数据速率；配置 HD/UHD 提示机的数据速率、帧同步与信号源 | references/capabilities/ccu-trunk-prompter.md | references/capabilities/ccu-audio-intercom.md、references/capabilities/ccu-format-lookup.md |
| 进入/退出本机菜单并更改设定；输入字符串（如 BAR CHARACTER）；分配可编配按钮与前面板显示；处理菜单锁定、菜单恢复与摄像机菜单切换 | references/capabilities/ccu-menu-operation.md | references/capabilities/ccu-web-menu.md、references/capabilities/customization.md |
| 查三型号与选件板的规格参数（电源/电流/温度/质量/尺寸）；查接口清单与信号规格；查"固定为…"的不可改项汇总；查使用环境与保养红线 | references/capabilities/ccu-specs-reference.md | references/capabilities/ccu-transport-setup.md、references/capabilities/specs-reference.md |
| 规划 RCP 面板 + CCU 主机 + 摄像机的整系统连接；核对两端 CNS 模式、CCU 编号与 IP 的一致性；建立选件与两端能力的映射（SFP50/SDI50/SM50/UHD35/CNFG50/SNMP50）；按正确顺序完成整系统投运与验收 | references/capabilities/system-integration.md | references/capabilities/network-setup.md、references/capabilities/ccu-transport-setup.md、references/capabilities/system-troubleshooting.md |
| 面对"系统不通/画面没信号/面板拧不动"先定故障层级；联合判读两端灯语与状态画面；用错误消息表与 DIAGNOSIS 缩小范围；区分面板侧控制权问题与主机侧链路/格式问题 | references/capabilities/system-troubleshooting.md | references/capabilities/led-diagnostics.md、references/capabilities/ccu-panel-diagnostics.md、references/capabilities/ccu-status-screen.md、references/capabilities/ccu-diagnosis-menu.md |

**非能力类查询**：
- 书名/作者/章节/整书概览 → references/overview.md
- 术语解释 → references/glossary.md
- 决策规则速查（不需要原文依据时） → references/cheatsheet.md
- 完整意图与关键词索引（本表未覆盖的意图先查这里） → references/capability-index.md

## 加载规则

- 每次任务先读本文件，再按路由表加载 **1** 张能力卡；任务明确跨域时最多加载 2 张。
- 概览/书名类问题不加载能力卡，用「核心原则」与 overview.md 回答。
- 路由表与 capability-index.md 都无法命中的意图，明确告知超出本书范围，不要硬套。

## 边界与判停

- 用户未提供所连设备型号或选件安装情况，而该信息影响菜单项存在性时，先询问再执行
- 需要给出手册未载的处置步骤或参数数值时（如 SFP+ 模块兼容清单、电源电压切换方法、CABLE ALARM SHORT 处置），停止并声明缺口
- 安全关键数值或格式串与手册原文冲突时，以原文为准并停止改写
- 涉及第 67 页 HFR↔BNC Link 编配表（已知文本提取缺口）时，声明依据不完整
