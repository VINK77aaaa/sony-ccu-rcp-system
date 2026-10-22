> 吸收单元: f26, f27, f32, f33, p56, p57, p59, p63, ce28, ce29, ce30, ce31（辅助边界: ce22, ce24, ce34；缺口: ALAC/F Drop/Black Set/OHB Matrix 参数细节原书未展开）

# 维护校正：Shading / OHB / RPN / 镜头 (RCP-3500/3501)

## R — 原文

- Shading 自动校正: "这是 Auto Black Shading 功能。可自动调节每项 RGB、HV 和 SAW/PARA 参数。"（逐通道 R/G/B，第 40-41 页；White Shading 同构）
- 落盘铁律: "如果 2D Black Shading 未保存到 OHB 文件, 则在摄像机断电时不会进行保存。"（Black R/G/B + White R/G/B 六处重复，第 40-41 页）
- RPN 白点: "宇宙射线和其他噪声可能影响 CCD 图像传感器的像素, 导致显示屏上出现小白点。这是图像传感器的物理特性, 并非故障。"；"执行自动黑平衡调节可激活校正功能, 可能会减少这种现象的影响"。(第 45 页)
- 控制权: "在面板（本机）和摄像机之间切换变焦/对焦操作。（当 Active 为 ON 时, 无法在摄像机侧调整变焦/对焦。）"(第 42 页)
- 监视联动: PIX/WF Synchro ON＝"调节白斑或黑斑时"输出跟随调节显示屏 RGB 开关；OFF＝用 PICTURE MONITOR / WAVEFORM MONITOR 按钮独立选信号。(第 49-50 页)
- 模式选型: "亮度不均匀的白色物体以及无色差的情形必须使用此模式"（指 Auto White Shading Mode 的 RGB 模式）。(第 46 页)
- Iris Gain: "值越大,响应速度越快,但越可能发生振荡。"（第 42 页）

## I — 自述

这是面板上"传感器与镜头层"的周期性维护能力，和 Paint 菜单的画质风格调整是两回事。四件事：①Shading 校正——黑/白色差逐通道（R/G/B）自动或手动（H/V SAW/PARA 四参数）校正，做完必须 OHB Store 落盘，否则断电全丢（维护返工第一主因）；②RPN 白点校正——画面上的固定小白点是传感器物理特性不是故障，先 ABB 再 RPN 手动点对点校，别急着报修；③镜头族——自动光圈参数（Iris Gain 大了会"光圈呼吸"）、变焦/对焦控制权（Active ON 面板独占，摄像师机身失灵先查这）、ALAC/F Drop 补偿；④校正作业的监视联动——PIX/WF Synchro 决定监视器输出跟不跟调节画面的 RGB 切换。

做维护时的顺序意识：先确认控制权与监视路由，再动手校正，最后落盘（OHB Store / Save），一步不能少。

## A1 — 案例与演练

- 书中画面示例：RPN 校正画面坐标示例 H Cursor=1307 / V Cursor=888（第 45 页），展示光标定位后 [Enter] 锁定的画面形态（原书未交代实际校正结果）。
- 合成演练（明确标记，可复算）：G 通道 Black Shading 校正后断电不丢——Maintenance→Camera→Black Shading→G→Auto B Shading→File→OHB→OHB Store→断电重启→校正值仍在。跳过 OHB Store 则按原书判据丢失。

## A2 — 未来触发

**情境**：①换镜头/周期性维护要做黑白 Shading；②画面有固定小白点，有人要报修；③"光圈一跳一跳的"（自动光圈振荡）；④摄像师报"机身调不了焦/变焦"；⑤自动白色色差做完还是有偏差（模式选错）；⑥校正做完了怕断电丢。

**语言信号**：维护 / maintenance、黑黑平衡白平衡校正 / shading、色差、白点 / dead pixel / RPN、光圈振荡 / iris oscillation、OHB、镜头补偿 / ALAC、F drop、Zoom/Focus 控制权。

**相邻区分**：画质风格参数（伽马/拐点/肤色）归 paint-adjustment；白点的"要不要报修"甄别入口在 led-diagnostics（本卡承接其转介执行 RPN）；日常 Zoom/Focus 拍摄中的归属判断在 daily-operation（本卡是 Maintenance 菜单里的设定面）；面板设定备份归 file-backup（OHB Store 是存进摄像机 OHB 文件，不是 USB 备份）。

## E — 可执行步骤

**输入契约**：校正前确认——所连摄像机型号（决定菜单项是否显示与参数可用性）、当前控制权归属（MCS 下面板是否激活）、监视链路走哪路。缺型号信息先问，不要假设菜单项存在。

**1. Shading 校正（黑/白同构）**：
1. 前置：PIX/WF Synchro 设 ON（RCP Config→Mode→PIX/WF，工程师模式项），让监视器跟随调节画面的 RGB 切换；调完转纯监视设回 OFF。
2. Maintenance → Camera → Black Shading（或 White Shading）。
3. 逐通道（R/G/B）：[Auto B Shading]（自动调 RGB/HV/SAW-PARA 全参数）；需要手动时调 H SAW / H PARA / V SAW / V PARA。
4. **判停铁律：做完必须 File → OHB → [OHB Store]**。不落盘=断电即丢（六通道同此）。
5. 自动白色色差模式选型：亮度不均的白色物体或无色差情形必须用 RGB 模式；常规匹配用 RB Only（R/B 对齐 G）。

**2. RPN 白点校正**（前置：连接 CCU 的 PIX 监视器出现十字光标）：
1. 先 ABB（自动黑平衡）激活校正，能减少白点影响；残留再走手动。
2. Maintenance → RPN → 按目标通道 [R]/[G]/[B] 亮灯。
3. [H/V Cursor] 打开光标 → 旋转调节旋钮把光标移到白点 → [Enter] 锁定坐标。
4. [Save]（"调节值已记录到控制面板中"）；校第二点先 [Delete] 删旧值再重复。
5. [Exit] 退出。

**3. 镜头族**：Maintenance → Lens：Auto Iris Settings（Level 收敛等级 / APL Ratio / Iris Gain 响应-振荡权衡 / Pattern 检测区域）；Zoom/Focus → Active 切换面板与机身控制权（ON=面板独占）；Flare/V Mod Saw 校正（勿过度）。

**4. 其他**：Black Set（主增益变化时各色黑电平保持）、OHB Matrix、ATW Setting（Speed 收敛速度）、Microphone Gain（Ch1/Ch2）。

**输出契约**：每步回报"路径 + 通道 + 执行方式（Auto/手动）+ 是否已落盘（OHB Store / Save）"；任务完成标准=校正生效且落盘证据明确。

## B — 边界

- **未存 OHB 断电即丢**（ce28/p56）：维护返工第一主因；"做完自动校正就走人"等于没做。
- **Iris Gain 拉满→光圈振荡**（ce29）：画面亮度周期波动先回调 Iris Gain，不要先怀疑镜头。
- **Active ON 时机身必然失灵**（ce30/p59）：摄像师报修"机身调不了焦"先查这里，这是排他性规则不是故障。
- **白点不是故障**（ce34）：LCD 亮点与 CCD 白点都是物理特性；处置顺序固定为 ABB→RPN，直接报修属于误报。
- **手册未展开的参数级细节**（缺口）：ALAC、F Drop Comp（Drop Point/Roundness）、D.shade Comp、Black Set、OHB Matrix 的具体调节方法原书只给定义，需查所连摄像机/镜头设备手册，不得编造步骤。
- **接口名差异留痕**：PIX1/WF1（p49）与 PIX2/WF2（p50/53）以实机接口为准。
- RPN 原文"重复步骤 5 中的步骤"疑为笔误，按上下文语义（Delete→重复定位-Enter-Save）执行。
