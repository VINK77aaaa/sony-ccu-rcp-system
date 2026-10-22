> 吸收单元: p17, p43, p55, p62, ce22, ce23, ce24, ce25, ce26, ce27（辅助: f22 自定义着色菜单入口, f29 Menu Control；参考素材: references.md Paint 菜单参考表）

# Paint 菜单图像调整 (RCP-3500/3501)

## R — 原文

- 门槛: "当控制面板处于工程师模式或 Page Permission 的 Full Paint 设为 ON 时"显示 Paint 菜单；"正常情况下,请将所需页面分配给 CUSTOM PAINT 按钮"。(第 16、20 页)
- Knee Max 门控: "仅当在工程师模式下或当启用 Knee Max Enable 功能时才能设定此项"。(第 33 页)
- Flare: "正向调节此旋钮,可根据物体亮度降低相应色彩的黑色电平。小心勿校正过度。"（两处重复，第 29、42 页）
- Noise Suppression: "过度控制可导致高分辨率灵敏度下降"。(第 34 页)
- Crispening: "正向调节此旋钮,…S/N 灵敏度增加,但分辨率灵敏度会下降"。(第 29-31 页，Detail 家族多处)
- Auto Knee: "启用自动拐点功能。忽略为 Knee Point/Slope 配置的设定"；Point Limit "设定通过自动拐点功能自动调节的拐点的下限。这样可让自动拐点功能不会影响低水平图像"。(第 33 页)
- ATW: "此功能可持续校正白平衡以便与拍摄期间的画面相匹配。根据所用模式,可能会发生错误。"（第 28-29 页）
- Skin DTL: "对于具有三个通道的型号,无法禁用 Skin DTL 功能。"（第 31 页）

## I — 自述

Paint 菜单是这台面板上图像精调参数的完整清单（白黑平衡、细节、肤色细节、矩阵、增益、伽马、黑伽马、拐点、快门、饱和度、HDR、实时色调等约 25 组），日常旋钮调不动的精细参数都在这里。它的使用分两层：一层是"门"——菜单本身默认隐藏，要靠工程师模式或 Full Paint 开放，常规做法是把常用页分配给 CUSTOM PAINT 按钮；另一层是"参数语义"——每组参数解决什么画面问题、调节方向是什么、有哪些对价。

调 Paint 的正确姿势不是背参数，而是带着画面问题来：肤色不好→Skin DTL；细节太肉/太糙→Detail 家族；高光压不住→Knee/White Clip；暗部发灰→Black Gamma；偏色不动白平衡→Matrix；整支片感→Gamma Table/HDR。每一步调节几乎都有对价（信噪比 vs 分辨率、自动 vs 手动控制权），卡片 B 段的失败边界必须先看。

## A1 — 书中未提供案例（合成演练）

原书未提供完整案例。一条明确标记的合成演练（可按原书规则复算）：

"人脸肤色偏红且显糙"：Paint → Skin DTL → 开启 Skin DTL 1 通道 → 画面中心对准人脸按 Auto Hue 1 自动测色相（第 31 页：捕捉画面中心想要测量的物体并执行）→ 用 Width 收窄范围 → Level 小幅正向柔化 → Gate 1 检查生效区域。预期：仅肤色区域轮廓减弱、其余不变；若整屏变化说明 Width 过大。

## A2 — 未来触发

**情境**：①画面偏色但 AWB 拉不回来，想动矩阵/多矩阵；②人脸肤色处理（光洁/细节柔化）；③细节锐度、轮廓、降噪的取舍；④高光过曝压拐点、暗部提黑伽马；⑤问"某个参数在 Paint 菜单哪一页/什么意思"；⑥HDR/Live Tone 输出调整。

**语言信号**：画面调色 / paint、肤色细节 / skin detail、轮廓锐度 / detail、伽马 / gamma、拐点 / knee、黑伽马 / black gamma、矩阵 / matrix、多矩阵 / multi matrix、HDR、实时色调 / live tone、参数在哪调。

**相邻区分**：面板 WHITE/BLACK/FLARE 旋钮的手动 RGB 平衡归 white-black-balance（本卡是 Paint 菜单里的 ATW/AWB 参数与精调）；AWB/ABB 按钮"按一下"归 daily-operation；Shading/白点/RPN 这类传感器与镜头校正归 maintenance-correction（本卡管风格，那边管硬件校正）。

## E — 可执行步骤

**输入契约**：先问清画面问题（哪个区域、什么不对）与约束（直播还是录制、能否牺牲分辨率/信噪比）。缺画面问题描述时先要样本或描述，不要盲调。

**0. 进门判停**：Category Select 找不到 [Paint] → 进工程师模式，或 Page Permission 开 Full Paint；日常用 CUSTOM PAINT 分配常用页（先在自定义着色菜单记录项目，再配 CUSTOM1-5，顺序不能反）。个别参数另有门控：Knee Max 需工程师模式或 Knee Max Enable。

**1. 菜单通法**：MENU → Category Select → [Paint] → 旋转 SELECT 旋钮翻页（页码/总页码显示）→ 按 SELECT 进项 → 选项卡切子菜单 → 四个调节旋钮改值 → [Exit] 返回。[Clear] 可逐项或整页清除（红框标记）。远程改摄像机/BPU/CCU 的菜单走 Config→Menu Control（f29）。

**2. 画面问题 → 菜单项决策表**（参考索引，语义压缩自原书 28-37 页）：
- 白平衡微调：White（RGB 增益 / ATW 持续追踪 / AWB 一次性 / Color Temp）
- 黑电平：Black（R/G/B、Master、ABB）；黑闪光污染：Flare（勿过度）
- 细节/锐度：Detail（Level/Limiter/Crispening/H-V Ratio/Frequency）→ HD/4K/8K Detail 同构；SD 输出在 Maintenance→SD Adj
- 肤色：Skin DTL（三通道、Phase/Width/Level、Auto Hue、Gate、Natural、Zoom Link、Y Limit）
- 色彩还原整体：Matrix（User/Preset/Multi 16 色相/Adaptive）；单色效果：Mono Color
- 灵敏度：Gain（Total/Step/M White）；伽马曲线：Gamma Table（Standard/Hyper/Special/User）
- 暗部：Black Gamma（Range 四档）；高光：Knee（Point/Slope/Auto Knee/Soft Knee/Knee Max）、White Clip
- 快门/帧率：Shutter（SLS/SHT/ECS）、FPS（Step/continuous、Comp）
- 闪光抑制：Flicker Reduction（ACM/Standard、电源频率）
- HDR 输出：HDR Operation（Setup/Knee/White Clip）、HDR Conversion（SDR↔HDR）、Live Tone Control 1/2
- 自动光圈细调在 Maintenance→Lens→Auto Iris Settings（归 maintenance-correction）

**输出契约**：每次调节回报"菜单路径 + 参数名 + 调节方向 + 画面预期变化 + 对价"；完成标准=用户确认画面问题缓解且无 B 段副作用。

## B — 边界

- **Flare 勿过度**（ce22）：正向过大压溃暗部层次；小步调节并盯黑位。
- **降噪两处对价**（ce23/ce24）：Noise Suppression 过度→分辨率灵敏度下降；Crispening 单边开大→真实细节被当噪声门限切掉。直播画质投诉先查这两处是否被拉满。
- **Auto Knee 抢控制权**（ce25）：ON 时手动 Knee Point/Slope 被忽略——"调了没用"先查它；开 Auto Knee 记得设 Point Limit 保低电平。
- **ATW 不是免维护**（ce26）：不适配模式下持续开启会追踪出错（白平衡自己漂）；长节目建议 AWB 一次性校准+手动微调（规避动作依手册语义推导）。
- **三通道型号 Skin DTL 关不掉单通道**（ce27）：该通道 Level 调 0 或用母开关整体开关（推导动作）。
- **菜单项可用性因所连摄像机而异**（p17 边界）：HD/4K/8K Detail、HDR 等仅当所连设备支持时显示；某项找不到先查设备支持，再查权限。
- 本卡不做传感器/镜头校正（Shading、RPN 白点、镜头补偿）——那是 maintenance-correction 的领地。
