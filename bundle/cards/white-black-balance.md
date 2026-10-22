> 吸收单元: f15, p26, p34, p35, ce10, ce20

# 白/黑/闪光平衡手动调节（WHITE·BLACK·FLARE 旋钮 RGB 按序 + ABSOLUTE 绝对/相对模式）

## R — 原文

（带引号者为原文直接引用；未带引号者为依据 verified 单元整理的原文要点摘录，页码为原文所在页。）

- ABSOLUTE 定义："此按钮使用绝对值模式 (亮起)和相对值模式 (未亮起)之间的 WHITE、BLACK、FLARE 和 DETAIL旋钮更改手动调节模式。在绝对值模式下,旋钮指示值变为设定值。在相对值模式下,旋钮指示角度和设定值不匹配"（p13）。
- 七种自动退回（p13，"在下列情况中将自动选择相对值模式"清单摘录）：通电中／面板激活状态改变时／PARA 或主/从模式时／自动设定（电平、白色和黑色）完成后／读取场景文件时／按 FLARE 切换调节模式时／用 RCP Assign 更改受控 CCU 时。
- BLACK/FLARE 双用途（p13，摘录）：FLARE 灯灭时该旋钮调黑平衡；按 FLARE 点亮后调闪光平衡；两者均按 R→G→B 顺序调节。
- 主/从白平衡冲突消解（p10，摘录）：Master 与 Subordinate 均设 ON 时优先执行主设备设定，从设备白平衡跟随主设备。
- 适用边界："可用于在旧有连接中使用 CNU (命令网络单元)的系统。LAN 连接不可用"（p8）。

## I — Interpretation

手动白/黑/闪光平衡是"一组旋钮 + 一层模式 + 一个顺序"的作业：

1. WHITE 旋钮调白平衡；BLACK/FLARE 是同一颗旋钮的双面——FLARE 灯灭调黑平衡、灯亮调闪光平衡，用 FLARE 按钮切换；DETAIL 旋钮同受 ABSOLUTE 管辖。
2. 一律按 R→G→B 三通道顺序调，不跳通道。
3. ABSOLUTE 决定旋钮刻度是否可信：亮=绝对值，刻度即设定值；灭=相对值，刻度和实际值脱钩。关键在它会被七种事件**自动**打断退回相对值——做完自动设定、读完场景文件、切了 FLARE、改了 RCP Assign 等之后，刻度"对不上"是设计行为，不是旋钮坏了。
4. 多机白平衡联动（主/从）是 CNU 旧有连接的遗留功能，LAN 组网下不存在，冲突时主设备说了算。

## A1 — Application Example

原书未提供案例。以下为一条明确标记的**合成演练**（按 p13/p14 规则可复算，非作者经历）：

- 输入：操作者报"读完场景文件 3 之后，BLACK 旋钮刻度和监视器黑位对不上了，旋钮是不是坏了"。
- 执行：①对照 p13 七条清单→命中"读取场景文件时"→判定系统已自动退回相对值模式（预期行为，非故障）；②需要刻度-数值对应关系时重按 ABSOLUTE（灯亮=绝对值恢复）；③需调闪光平衡→按 FLARE 使灯亮；④按 R→G→B 顺序逐通道调 BLACK/FLARE 旋钮，同时看监视器黑位。
- 预期：ABSOLUTE 亮时旋钮指示值=设定值；黑平衡/闪光平衡由 FLARE 灯态区分；RGB 按序执行后三通道黑位一致。
- 原书未交代实际结果（未说明）。

## A2 — Future Trigger

使用情境：
1. 多机位肤色/白场不一致，要手动微调各机 WHITE（"2 号机偏绿帮我拉一下"/"white looks green, tweak R/G/B"）。
2. 黑位漂移或镜头闪光（flare）问题（"黑位发灰"/"black balance off"/"镜头炫光要压"）。
3. 旋钮刻度和实际值对不上（"旋钮是不是坏了"/"knob scale doesn't match the value"）。
4. 想让多台机白平衡跟一台走（"主从白平衡"/"master/subordinate white balance"）。
5. 做完 AWB/读完场景文件后手动微调手感不对（"调多少变多少不对劲"）。

语言信号（中英）：白平衡 white balance、黑平衡 black balance、闪光平衡 flare、BLACK/FLARE 旋钮、R/G/B 顺序、ABSOLUTE、绝对值 absolute、相对值 relative、刻度对不上、主从 master/subordinate。

与相邻能力的区分（初稿，阶段 3 回填）：
- daily-operation：AWB/ABB 自动调整按钮、光圈/快门/增益/滤镜/测试信号归那边；本卡只管手动 RGB 平衡旋钮与 ABSOLUTE 模式机制。
- paint-adjustment：Paint>White 菜单参数（ATW Setting、WB R/B 涂装参数）与 Black Gamma 归那边；ATW 长开的追踪出错失败模式也记在 daily-operation（ce26）。
- mcs-operations：主/从功能的多控制器仲裁语境归那边；本卡只讲白平衡语义与 CNU/LAN 边界。
- maintenance-correction：Black Set（增益切换黑电平漂移）与 Black Shading（空间黑斑）虽都带"黑"字，归那边，勿在本卡调。

## E — Execution

输入契约：
- 必需 (a) 调节对象：白平衡（WHITE）/黑平衡/闪光平衡（BLACK/FLARE）；(b) 当前 ABSOLUTE 灯态（亮=绝对值/灭=相对值）——操作前看灯确认，不得按假设模式拧旋钮；(c) 若涉主/从联动：组网是否为 CNU 旧有连接——必问；LAN 组网直接判停（ce10）。
- 缺 (a) 先问"调白、黑还是闪光"；缺 (b) 请现场报灯态。

步骤：
1. 模式核对：ABSOLUTE 灯灭或近期发生过七事件之一（通电/面板激活改变/PARA 或主从/自动设定完成/读取场景文件/按 FLARE 切换/RCP Assign 更改 CCU）→ 必处于相对值；需绝对值则重按 ABSOLUTE 至灯亮（p13）。
2. 对象分支：调黑平衡→FLARE 灯灭状态下操作；调闪光平衡→先按 FLARE 亮灯（p13）。**判停分支**：调完闪光平衡要回黑平衡时，再次按 FLARE 会再次触发自动退回相对值→回到步骤 1 重校模式。
3. 顺序调节：按 R→G→B 逐通道调旋钮，边调边看监视器（p13）。
4. 主/从联动（仅 CNU 旧有连接）：Multi 菜单设 Master/Subordinate；两端均 ON 时以主设备设定为准（p10）。LAN 组网→告知功能不可用，替代路径=逐台 AWB 或场景文件统一（ce10，替代动作为操作建议口径）。
5. 相对值模式约束：SENS 类定界操作与刻度直读均无效/失真，不在此模式下凭刻度判断数值（p14；ce20）。

输出契约：结果以监视器白场/黑位确认；报告注明"调节对象（白/黑/闪光）+ ABSOLUTE 灯终态 + 各通道方向"，避免交接歧义。

## B — Boundary

- 反场景：想跑自动白/黑平衡→daily-operation 的 AWB/ABB；调 Paint>White/ATW/Black Gamma 菜单参数→paint-adjustment；增益切换后黑电平漂移（Black Set）与黑斑（Black Shading）→maintenance-correction。
- 失败模式 ce20：相对值模式按绝对值手感拧旋钮——调节量偏离预期甚至反直觉；做完 AWB/ABB、读完场景文件、切过 FLARE、RCP Assign 换机后是高发时刻。
- 失败模式 ce10：在 LAN（BRIDGE/MCS）组网下设 Master/Subordinate——功能不工作（"LAN 连接不可用"为原文），别在菜单里反复找开关。
- 相邻失败模式（ce26，归 daily-operation 吸收）：ATW 持续追踪在不适配模式下可能报错漂移；本卡的手动微调正是其替代手段之一。
- 原书盲点（BOOK_OVERVIEW 批判节）：手册给了七条退回清单，但未给"退回后批量恢复多颗旋钮绝对值"的组合操作与顺序建议；"黑"相关概念三层（Black 黑平衡 / Black Set / Black Shading）正文易混，调黑前先确认对象。
- 型号差异：主黑电平调节环（RELATIVE 按钮）为 RCP-3500、主黑电平调节旋钮为 RCP-3501（p14）；"主黑电平调节功能在 RCP-3501 上不可用"（p25）——涉主黑电平先核对型号标注。
