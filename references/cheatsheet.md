# 决策规则速查 — Sony 摄像机控制系统使用说明书合辑（RCP-3500/3501 遥控面板 + HDCU5000/5500/3500 摄像机控制单元）

| 能力 | 一句话规则 |
|---|---|
| 组网连接与配置 | 先按物理连线四选一定 CNS（只用 CCA-5→LEGACY；LAN 一对一→BRIDGE；混合拓扑/多机→MCS；HZC-RCP5→PC 控制），配置在工程师模式完成，编号与 IP 全系统唯一，更改 CNS 后必须重启所有摄像机系统。 |
| MCS 多机操作仲裁 | 面板能不能动先看灯——PANEL ACTIVE 亮才有整机操作权（全系统仅一台），IRIS/MB ACTIVE 独占光圈/主黑，PARA 是并行通道（IRIS/MB 激活时禁用），主设备断开时长按 PANEL ACTIVE 强制激活。 |
| 指示灯灯语诊断 | 先分层再查表——CAM PW 管电源、NETWORK 管本机与控制设备、CABLE 管摄像机与 CCU 链路、ALARM 管设备错误；状态与含义原样成对判读，报故障前先排除 LEGACY 正常态、权限态与坏点白点。 |
| 规格与接口速查 | 查询→原样回报，禁止换算——规格表/针脚表/电缆长度/线材规格均按原文数值、单位与页码回报，随附 Tally-MCS 禁用与型号差异提示，表中没有的字段答"原书未给"。 |
| 使用环境与保养红线 | 环境七红线逐条"触发→动作→后果"——冷凝断电、通信设备建议关机（建议级不升格）、电容约 5 年按工况折减、医疗设备勿近、接网先确认安全、软布清洁、LCD 坏点非故障；使用前确认运行正常。 |
| 摄像机日常操作（自动调整/光圈/快门/增益/ND-CC 滤镜/测试信号） | 动任何旋钮前先看灯——控制权灯亮才操作；自动调整看灯语（亮=进行中/灭=完成/闪=已停止）；滤镜灯灭先按上/下按钮夺取许可；监视器异常先查 BARS 优先级与 Zoom/Focus Active。 |
| 白/黑/闪光平衡手动调节（RGB 按序 + ABSOLUTE 绝对/相对模式） | 调白/黑/闪光平衡一律先看 ABSOLUTE 灯态、按 R→G→B 顺序；刻度对不上先对照七种自动退回场景（AWB 后/读场景文件后/切 FLARE 后等），重按 ABSOLUTE 恢复绝对值再调。 |
| 场景文件管理（面板 STORE 存取 / EXPAND 32 文件 / Dissolve） | 按编号前先看 STORE 灯——闪烁=写入覆盖待命（再按 STORE 取消）, 未闪烁=读取；1-5 号直达灯亮, 6 号起走 EXPAND（最多 32 个）；后悔再按同编号恢复访问前状态。 |
| USB 备份/恢复/初始化（RCP Config 与 Network Config / All Preset） | 完整备份=[RCP Config] 与 [Network Config] 各 Store 一次, 选号前必查列表避让已占用编号；All Preset 全量初始化（工程师模式）执行前必须已有备份。 |
| 自定义配置（SW Customize / Assign Knob / Menu Customize / Status Customize / VR Setting） | 自定义分配一律以两段 Save 收尾（未保存退出=不生效）；22 项着色项目必须先经 Menu Customize 记录、再配置 CUSTOM1-5 按钮, 顺序不可颠倒。 |
| 工程师模式、安全代码与权限 | 先查权限再查故障——File/Maintenance/Paint 菜单和十类设定都藏在工程师模式后（MENU→Config→RCP→Security→Engineer Mode），代码生命周期走 0359 三键入口，权限分 Page（全锁/只读/Full Paint）与 Item（七开关）两层。 |
| Paint 菜单图像调整 | 带着画面问题进 Paint——进门先查权限（工程师模式或 Full Paint），按"问题→菜单项"决策表定位（肤色→Skin DTL、细节→Detail、高光→Knee、暗部→Black Gamma、偏色→Matrix），每步先看对价再动旋钮。 |
| 维护校正：Shading / OHB / RPN / 镜头 | 维护三步走——先定控制权与监视路由（Zoom/Focus Active、PIX/WF Synchro），再逐通道 Shading 校正，最后必须 OHB Store 落盘；固定白点不是故障，ABB→RPN 两级处置。 |
| 传输方式决策与连接配置 | 先按物理线缆与所连摄像机型号五选一定 CABLE TYPE（FIBER CAMERA CABLE / COAX / COAX(HDCE) / SINGLE-MODE FIBER），再定 FIBER TRANSMIT RATE（HIGH/ULTRA），选件门槛与距离上限缺一不可。 |
| 系统格式配置 | SYSTEM（1.001(525)/1.000(625)）× FIBER TRANSMIT RATE（HIGH/ULTRA）× CAMERA FORMAT 三者互相约束，共同决定所有输出/返回格式的可选集；BIT DEPTH/CCU VIDEO CONVERT/FRAME CONVERT DELAY/HD-SD DELAY 各有前置条件。 |
| 输出/返回格式派生与查表 | 所有输出格式（OUTPUT FORMAT1-4/IP）与返回格式（RETURN FORMAT1-3/IP）都是 CABLE TYPE × FIBER TRANSMIT RATE × SYSTEM × CAMERA FORMAT 的派生查表结果（第 54/56/58/63 页），格式串必须原样保留；UHD-SDI A/B 为专用输出不可配返回格式。 |
| HDR / LIVE HDR 配置 | HDR MODE 的 LIVE HDR 让同一摄像机同时输出 HDR 与 SDR；HDR OETF 取 S-Log3 或 HLG，HDR/4K COLOR SPACE 取 BT709 或 BT2020；HDR 输出不支持部分绘制功能，且 HDR 与 720 返回互斥、RGB444 一律 SDR。 |
| 同步配置（GENLOCK + PTP） | GENLOCK MODE 三选一（HD / SD / NETWORK）；ST2110 系统必须选 NETWORK，此时不需要 REFERENCE IN 外部输入而改用 HKCU-SFP50 的 LAN1/LAN2 做 PTP（仅支持 ST2059-2）；相位范围随 HD/SD 不同，LOCK STATUS 四态判读。 |
| 网络与 IP 配置 | 按端口（LAN-COM / LAN1 / LAN2）分别设 IP、子网掩码、默认网关；LAN1/LAN2 链路速度必须相同否则无法正常操作；DHCP 的"自动 IP"仅适用于 LAN-COM；CNS MODE 三选一（LEGACY/BRIDGE/MCS）并设 CCU NO 与主设备 IP。 |
| IP Live / NMOS / 第三方协议配置 | IP Live（LSM）配置需 HKCU-SFP50，PORT 更改后必须重启本机；NMOS（IS-04/IS-05）仅当 IP Live PORT 设为 DISABLE 时可选；Ember+ 需 HZCU-CNFG50、SNMP 需 HZCU-SNMP50；TSL UMD 走 UDP 8900。 |
| Web 菜单远程运维 | 用 Chrome 访问本机 IP 打开 Web 菜单，可远程配置、看 CCU 信息列表与执行 OSD 操作；菜单锁定开关 ON 时无法用 Web 配置；SERVICE DISCOVERY 关闭可减少网络负载但本机不再被其他 CCU 发现。 |
| CCU 文件与日志管理 | CCU 文件最多 5 个，RECALL 会加载全部菜单设置但不含 LAN-COM 的 IP/子网/网关；USB 路径固定 /MSSONY/PRO/CAMERA/HDCU5000；日志最多保存 30 天，且更改 DATE&TIME 会删除本机全部日志。 |
| 前面板灯语诊断 | CCU 前面板用 CABLE ALARM（OPEN/SHORT）、CABLE CONDITION（4 级颜色）、NETWORK（4 态闪烁）、ALARM、FAN STOP、SIGNAL BAR、POWER（CAM/MAIN）一组灯语定位故障层级，配合错误消息表（CCU:XXX …）判断；手册只给现象不给处置。 |
| 状态画面判读 | 状态画面共 11 页（System Status / Multi Format1-4 / Multi Format IP / Audio / Intercom / Network / IP Stream / Alarm），需先把 SDI-OUT3/4 的 MONITOR 设为 M 或接 CHARACTER 接口；未连接摄像机时显示"-"或"Not Detected"属正常而非故障。 |
| DIAGNOSIS 硬件诊断 | DIAGNOSIS 菜单 D01–D06 提供板卡自诊断（VIF/TX/NET 的 OK/POWER ERROR/PLD ERROR/TEMP WARNING）、累计开机时间、型号与序列号、软件/PLD 版本、摄像机诊断、电源单元状态与风扇状态；均为只读观测，不提供处置。 |
| 音频 / 对讲配置 | A01–A07 七个音频/对讲页面：摄像机麦克风增益、音频输出电平与延迟、PRODUCER/ENGINEER 对讲接口（CLEAR COM/4WIRE/RTS）、前面板对讲（麦克风类型绑定增益）、测试音、以及需 HKCU-SFP50 的 IP AUDIO/IP INTERCOM 音频格式串。 |
| 干线 / 提示机配置 | M01/M02 两个页面：TRUNK LINE CHANNEL MODE（2CH MAX 75Kbps / 1CH MAX 150Kbps）与 INTERFACE（232C/422A）、PROMPTER CH；NETWORK TRUNK 模式三选一，且 FIBER TRANSMIT RATE=ULTRA 时固定为 NETWORK+VIDEO，HD PROMPTER 在 HDCU5000/5500 用 SDI-RET 时固定 DISABLE。 |
| 本机菜单操作与可编配按钮 | 用 DISP/MENU 控制杆、CANCEL/ENTER 控制杆与 CONTROL 旋钮操作本机菜单（含字符串输入 INS/DEL/RET/END/ESC）；菜单锁定开关控制操作区；可编配按钮取值 NONE/BARS/CAM POWER/FORCE LEGACY/OPTICAL SIGNAL；CAMERA MENU CTRL=ON 时 CCU 菜单不可用。 |
| 接口 / 规格 / 环境速查 | 三型号（HDCU5000/5500/3500）与四块选件板（HKCU-FB50/SDI50/SFP50/SM50）的电源、电流、温度、质量、尺寸、输入/输出接口清单，以及接口信号功能随 I/O 方向变化的取值规则、固定项汇总、SDI ANCILLARY DATA 标准年份与使用环境红线——全部原样收录，禁止换算。 |
| 整系统组网与联调 | RCP 面板与 CCU 主机是同一系统的两端：面板经 RCP/CNU 接口（CCA-5）连到 CCU 的 RCP/CNU 接口（并取电），两端的 CNS 模式、CCU 编号、主设备 IP 必须一致且全系统唯一；CCU 侧的传输方式与选件决定整系统格式能力；投运须按"改 CNS 重启所有摄像机系统 / 改 IP Live PORT 重启本机"的顺序收尾。 |
| 整系统联合排障 | 排障时先把现象归到"面板侧 / 主机侧 / 链路侧"三层：面板侧看 RCP 的 NETWORK/ALARM/CABLE/CAM PW 灯与激活状态，主机侧看 CCU 的 CABLE ALARM/CABLE CONDITION/FAN STOP 灯、状态画面 11 页与错误消息表、DIAGNOSIS 只读诊断，链路侧看两端 GENLOCK/PTP 与格式一致性；两端同名 NETWORK/ALARM 灯含义不同，是最易误判处。 |

> 速查只给结论；需要原文依据、案例或反例时读对应能力卡。
