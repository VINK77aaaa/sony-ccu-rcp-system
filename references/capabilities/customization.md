> 吸收单元: f21, f22, f23, f24, p46, p47, p60, ce16, ce17

# 自定义配置（SW Customize / Assign Knob / Menu Customize / Custom Menu SW / Status Customize / VR Setting）

## R — 原文

（带引号者为原文直接引用；未带引号者为依据 verified 单元整理的原文要点摘录，页码为原文所在页。）

- 保存铁律："如果未保存就退出菜单,则功能分配不会反映出来。"（p21；同句见 p23/p28，全手册共 5 处）。
- 分配通用骨架（p20-22，摘录）：进入分配画面后可分配控件指示灯全亮→按目标控件→用最左侧调节旋钮选功能（选中变琥珀色）→[Enter] 后出现 *→可重复分配→[Save]→确认画面再 [Save]。
- 着色项目前置顺序（p23，摘录）："先记录进自定义着色菜单,然后配置自定义按钮 (CUSTOM1 至 5)"；受限项目清单共 22 项（Skin Detail…Gamma Table）。
- Menu Customize 编辑（p22，摘录）：底部列表选项目（变琥珀）→SELECT 在顶部列表定位→[Insert] 插入/[Line] 插分割线；删除=SELECT 选中→[Delete]；删分割线=选中其上方项目按 [Line]；[Save]×2 收尾。
- 状态画面（p26-27，摘录）：菜单和所有自定义着色按钮灯灭时显示；[Status Display OFF]=空白画面；Menu Type 六种：Control Value Only / With Optical Level / With 4 Control Knobs / Opt Lvl and 2 Knobs (R) / (L/R) / (L)——可用旋钮数由所选类型决定。
- 旋钮灵敏度（p24-25，摘录）：VR Setting 仅相对值模式下生效；选项卡 White/Blk/Flr、Detail、Iris/M.Black；可选 1/1、1/2、1/4；主黑电平调节功能在 RCP-3501 上不可用。

## I — Interpretation

自定义体系回答的是"把高频功能搬到顺手位置"，五条流水线一个收尾：

1. SW Customize 给自由按键（F 键等）派功能；Assignable Knob 给调节旋钮派功能；Custom Menu SW 给 CUSTOM1-5 派着色菜单项——三者共用同一套骨架：亮灯选控件→最左旋钮选功能（琥珀色）→Enter 打星号→Save 两段。
2.CUSTOM1-5 有前置依赖：22 个受限着色项目必须先在 Menu Customize 里记录进自定义着色菜单，然后才能配置按钮——顺序反了不成立。
3. Status Customize/Knob Customize 把"待机状态画面"变成个人仪表板：先选版式（六种 Menu Type），再给 Knob 1-4 派功能——能派几个旋钮由版式决定。
4. VR Setting 调相对值模式的旋钮步进（1/1、1/2、1/4），只对相对值模式有意义。
5. 全体系一条铁律：没按完两段 Save 就退出=全部白做——手册用五处重复警告强调这是最高频的坑。

## A1 — Application Example

原书未提供案例。以下为两条明确标记的**合成演练**（按 p20-23 规则可复算，非作者经历）：

演练 1（正例+失败分支，f21 演练口径）：
- 输入：把 GATE 分配给 F1。
- 执行：SW Customize→按 F1→最左旋钮选 GATE（变琥珀色）→[Enter]（F1 旁出现 *）→[Save]→确认画面再 [Save]。
- 预期：退出后按 F1 生效。失败分支：改完不按 Save 直接退出菜单→分配不生效（p21 警告句）。

演练 2（顺序依赖，f22 演练口径）：
- 输入：把 Gain 开放进 CUSTOM PAINT 菜单并分配给 CUSTOM1。
- 执行：先 Menu Customize（底部列表选 Gain→SELECT 顶部定位→[Insert]→[Save]×2）；再 Custom Menu SW 把 CUSTOM1 分配给 Gain→Save×2。
- 预期：顺序颠倒（先配 CUSTOM1）则分配不成立——p23 强制顺序；完成后 CUSTOM1 直达 Gain。

## A2 — Future Trigger

使用情境：
1. 把常用功能放到顺手位置（"把 GATE 放到 F1 上"/"assign a function to a button"/"自定义旋钮"）。
2. CUSTOM PAINT 菜单加项目（"自定义着色菜单里能不能加 Gain"/"menu customize"）。
3. 状态画面改成自己的仪表板（"待机画面能显示 4 个旋钮吗"/"status screen customize"）。
4. 旋钮手感不对（"旋钮太灵敏"/"knob sensitivity 1/2"）。
5. 改完自定义没生效（"分配了怎么没反应"→大概率没保存，ce16）。

语言信号（中英）：自定义 customize、分配 assign、SW Customize、Assignable Knob、CUSTOM1-5、CUSTOM PAINT、Menu Customize、状态画面 status screen、Knob Customize、灵敏度 sensitivity、琥珀色 amber、保存 Save、不生效 not applied。

与相邻能力的区分（初稿，阶段 3 回填）：
- engineer-mode-security：自定义大多要在工程师模式下配置，"怎么进工程师模式/安全代码"归那边；安全限制（Page/Item Permission）管"哪些功能可见/可用"，自定义管"功能放在哪"，两者都在 Config 但语义不同，勿混。
- daily-operation：自定义完成后的日常使用（按 F1、转旋钮）归那边。
- paint-adjustment：被分配的着色项目本身（Gain/Skin Detail 等参数语义）归那边。
- file-backup：自定义资产的持久化靠 USB 备份 [RCP Config]，备份/恢复操作归那边。

## E — Execution

输入契约：
- 必需 (a) 目标控件（F 键/CUSTOM1-5/Assignable Knob/Knob 1-4）；(b) 要分配的功能名——若属 22 项受限着色项目，须走 Menu Customize 前置；(c) 工程师模式已进入（未进入先转 engineer-mode-security，判停）。
- 缺 (a)(b) 先问清；功能不在可分配清单时如实告知，不臆造。

步骤：
1. 通用分配（SW Customize/Assignable Knob/Custom Menu SW 同骨架）：进入分配画面→确认可分配控件灯全亮→按目标控件→最左调节旋钮选功能（选中变琥珀色）→[Enter]（出现 *）→需多个重复→[Save]→确认画面再 [Save]（p20-22）。
2. **判停铁律**：两段 [Save] 未按完不退出；未保存退出=分配不生效（p21/p23/p28）——用户报"不生效"时先查是否漏了第二段 Save。
3. 着色项目前置分支：目标功能属 22 项清单→先 Menu Customize 记录（步骤 4）再回来配置 CUSTOM1-5；顺序颠倒不成立（p23）。**判停**。
4. Menu Customize 编辑：底部列表选项目（变琥珀）→SELECT 顶部列表定位→[Insert] 插入该项目下方/[Line] 插分割线；删除=SELECT 选中→[Delete]；删分割线=选中其上方项目按 [Line]→[Save]×2（p22）。
5. 状态画面：Status Customize→Menu Type 六选一（先定版式——可用旋钮数由类型决定，选 Control Value Only 则几乎无可分配旋钮）→Knob Customize→Select Knob (1-4)→最左旋钮选功能→[Enter]→[Save]×2；重置=Default Setting→[OK]→[Save]（p26-28）。
6. 灵敏度：RCP Config>VR Setting→选项卡（White/Blk/Flr、Detail、Iris/M.Black）→按下 1/1、1/2 或 1/4（仅相对值模式生效；RCP-3501 上无主黑电平项）（p24-25）。
7. 重置：各分配画面 [Default All]→[OK]→[Save]×2（p20-22）。
8. 验证：退出菜单后实际触发一次目标控件确认生效。

输出契约：报告"控件→功能"分配表；每条注明已两段保存并实测生效；涉 Menu Customize 的报告插入位置（页/行）。

## B — Boundary

- 失败模式 ce16：改完不按 Save 就退出菜单——手册在 p21×3/p23/p28 共五处重复同一警告句，是全手册强调密度最高的坑；"不生效"先查保存。
- 失败模式 ce17：跳过 Menu Customize 直接把着色项目分配给自定义按钮——违反 p23 强制顺序；失效表现原书未明示，按"分配不成立"从严处理。
- 边界：CUSTOM1-5 只能派 22 项清单内的着色项目；状态画面可分配旋钮数由 Menu Type 决定（p27），先选版式再派旋钮。
- 口径边界：Display/Sound 等用户界面设定普通模式可配（p23）；其余自定义项多在工程师模式（p45 清单口径）。
- 型号差异：MB Knob（主黑电平旋钮改配）仅限 RCP-3501（p47）；主黑电平灵敏度设定在 RCP-3501 上不存在（p25，与 daily-operation 吸收的 ce37 同源互证）。
- 原书盲点（BOOK_OVERVIEW 批判节）：task-11 标注"未保存退出即丢失是高频坑"；手册给了逐项分配流程但无"批量检查当前分配"的总览画面，交接设备时需逐画面核对或靠 USB 备份对账（file-backup 相邻）。
- 反场景：想让某菜单"消失/只读"→那是安全限制（engineer-mode-security），不是自定义；自定义按钮按了没反应且已确认保存→先查工程师模式权限与所连摄像机支持范围。
