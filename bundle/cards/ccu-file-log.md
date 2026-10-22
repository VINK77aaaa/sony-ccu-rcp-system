> 吸收单元: f21, f22, f37

# CCU 文件与日志管理 (HDCU5000/5500/3500)

## R — 原文

- "本机的所有菜单设置都可保存到 CCU 文件中。使用 RECALL 加载并应用保存的设置以简化设置操作。使用 RECALL 不会加载 LAN COM 接口的 IP 地址、子网掩码和默认网关设置。" (第 78 页)
- "STORE：将 CCU 文件保存到内存中。本机最多可保存五个 CCU 文件。在 STORE 屏幕上选择文件编号。" (第 78 页)
- "EXPORT TO USB：将 CCU 文件导出到 USB 闪存驱动器。还支持使用 Web 菜单进行导出。USB 闪存驱动器的路径为 "/MSSONY/PRO/CAMERA/HDCU5000"" (第 78 页)
- "FILE NAME1 至 5 … ASCII 代码, 1 至 32 个字符"；"CLEAR ALL：删除所有 CCU 文件。" (第 78 页)
- "LOG：ENABLE、DISABLE 启用或禁用保存日志文件。"；"CLEAR：删除本机内部存储的日志 (通过使用 EXEC 执行)。日志最多保存 30 天。当达到 30 天的最大值时,会从最旧的日志开始删除。" (第 78 页)
- "DATE (YEAR) … 设定日期和时间。当此项更改时,本机上存储的所有日志都会被删除。" (第 76 页，M04 DATE&TIME)
- "READ KEY FROM USB：通过使用 ENTER 执行操作。从 USB 闪存驱动器读取安装密钥。" (第 77 页，M09 OPTION)

## I — 自述

CCU 的"资产"分两类，各自有独立的存取通道，混用会出事。第一类是 **CCU 文件（CCU FILE）**：它是本机全部菜单设置的一张快照，存在本机内存里，**最多五个**（FILE INDEX 1 至 5），可 RECALL 加载、STORE 保存、EXPORT/IMPORT 走 USB、CLEAR ALL 整体清空。第二类是 **日志（LOG）**：记录本机运行事件，最多保存 **30 天**，超期从最旧的开始删；可 EXPORT TO USB 导出、CLEAR 清除，也可整体开关（ENABLE/DISABLE）。

最容易被误判的一条铁律：**RECALL 不会加载 LAN COM 接口的 IP 地址、子网掩码和默认网关设置**。也就是说换机恢复时，用 CCU 文件能还原几乎所有菜单设置，唯独 LAN COM 的三项网络参数必须**另外手工重配**。这条不对称性（STORE 存整机、RECALL 少网络）是换机/故障恢复时最容易漏掉的一步。

第二条硬风险来自日期时间：**更改 DATE&TIME 会删除本机上存储的所有日志**（第 76 页 M04 明文）。这不是"可能影响"，而是"更改即清空、不可逆"。因此只要历史日志还需要留证，正确顺序永远是"先 EXPORT TO USB 导出日志 → 再改日期时间"。

USB 路径是固定约定：CCU 文件与日志的 EXPORT/IMPORT 都落在 USB 闪存驱动器上的 **`/MSSONY/PRO/CAMERA/HDCU5000`**，三型号共用同一字符串。导入/导出还支持 Web 菜单通道（远程做），但路径约定不变。日志导出与清除是 EXEC 型（执行即生效），CCU 文件的 CLEAR ALL 同样是不可逆批量删除。

## A1 — 书中配置示例

**原书未给出 CCU 文件/日志的操作实例**（手册为查阅型菜单表，F01/F02 只有"设置值 + 说明"，无现象→步骤的完整演算）。以下为**合成演练（非原书内容）**，按第 76/78 页规则可复算：

- 输入：一台 HDCU5500 因主板故障需换机，要求把旧机配置迁到新机，并保留近一个月的日志用于事后追溯。
- 执行（迁移）：旧机 FILE <CCU FILE> F01 → FILE INDEX 选槽位 → EXPORT TO USB（落盘 `/MSSONY/PRO/CAMERA/HDCU5000`）；新机同路径 IMPORT FROM USB → FILE INDEX 选槽 → RECALL。
- 执行（日志）：旧机 F02 → EXPORT TO USB（路径同上）→ 再执行 CLEAR（可选）。
- 预期：新机菜单设置恢复；但 **LAN COM 的 IP/子网/网关不恢复**，须在 NETWORK 菜单手工重设（ce29）。
- 反例推演：若为"对齐时区"直接改新机 DATE&TIME，则新机上已导入/已产生的日志被清空（ce01）；非法日期还会触发 `CCU:SET DATE&TIME`（ce25）。两处机制不同：前者是"变更即清空"，后者是"非法值报错"。

## A2 — 未来触发

**情境**：

1. 换机/故障恢复："这台 CCU 的设置怎么搬到新机上 / 导出的文件放哪 / 恢复后网络怎么不通"。
2. 日志取证与导出："近一个月的日志怎么导出 / 日志能存多久 / 怎么清日志"。
3. 时区/日期校正："日期不对要改一下"——**此情境必须先触发本卡**，因为改日期会清空全部日志。
4. USB 导入导出："U 盘插上找不到文件 / 路径是什么 / 能不能用 Web 做"。
5. 批量清空："想把五个 CCU 文件全删了 / 清空日志"。

**语言信号**：中文——"CCU 文件 / 存文件 / 取文件 / RECALL / STORE / 导出 / 导入 / U 盘 / USB / 日志 / 导出日志 / 清日志 / 改日期 / 时区 / 备份 / 换机"；英文——"CCU file / recall / store / export to USB / import from USB / log / clear log / date and time / timezone / backup"。

**相邻区分**：

- **ccu-status-screen**：本卡管"把日志/文件导出落盘"，状态画面的 Alarm 页只负责"把告警读出来"，不落盘。要"看告警"→彼卡；要"导出/清日志"→本卡。
- **ccu-panel-diagnostics / ccu-diagnosis-menu**：灯与诊断给出"发生了什么"，本卡给出"如何把记录留证/恢复配置"。三者常在排障时串联，但职责不重叠。
- **RCP `file-backup`**：彼卡是 **RCP 面板侧** 的两类 USB 备份（[RCP Config] 不含网络 + [Network Config]）；本卡是 **CCU 主机侧** 的 CCU 文件（5 槽）与日志。二者路径与对象都不同，切勿混用。问"面板设置怎么备份"→彼卡；问"CCU 整机设置/日志"→本卡。
- **ccu-network**（网络与 IP 配置，如有独立卡）：RECALL 之后补配 LAN COM 的 IP/子网/网关，其配置动作归彼卡；本卡只负责"提醒它不会被 RECALL 带回来"。

## E — 执行步骤

**输入契约**（缺失先问，不猜）：①动作——RECALL / STORE / EXPORT / IMPORT / CLEAR ALL / 日志导出 / 日志清除 / 改日期；②对象——CCU 文件槽号（1 至 5）或"日志"；③USB 场景下——U 盘已插入前面板 USB 端口（第 11 页 q）；④若涉及改 DATE&TIME——须先确认"历史日志是否还需要"。缺槽号时先报占用情况再问，**不得默认选 1 号**；缺 ④ 确认时，**不得先改日期**。

1. **选通道**：CCU 文件 → FILE 菜单 `<CCU FILE>` F01；日志 → FILE 菜单 `<LOG>` F02；日期时间 → MAINTENANCE 菜单 `<DATE&TIME>` M04。
2. **CCU 文件存取**：FILE INDEX 选 1 至 5 → RECALL（加载）或 STORE（保存，最多五个）→ 可选 FILE NAME1 至 5 命名（ASCII，1 至 32 字符）。
3. **USB 导入导出**：EXPORT TO USB / IMPORT FROM USB，落点与来源路径均为 `/MSSONY/PRO/CAMERA/HDCU5000`（第 78 页）；也可经 Web 菜单执行同操作。
4. **日志管理**：LOG 设 ENABLE/DISABLE → EXPORT TO USB（EXEC 执行）→ CLEAR（EXEC 执行）。保留窗口为 30 天，超期从最旧删除。
5. **判停分支**：
   - 用户要在有取证需求时改 DATE&TIME → **先停**，要求先导出日志；导出确认后再改（ce01）。
   - 用户要 CLEAR ALL 或 CLEAR → **先停**，确认是否已有 USB 备份/导出；无备份则提示不可逆（ce03）。
   - 换机恢复后网络不通 → 定位为"RECALL 不含 LAN COM 网络设置"，转 ccu-network 补配（ce29）。
   - 设了非法日期 → 触发 `CCU:SET DATE&TIME`，先改正日期值（ce25）。
6. **验证**：RECALL 后抽查菜单设置是否生效；网络三项是否已手工补配；USB 上 `/MSSONY/PRO/CAMERA/HDCU5000` 下是否出现文件/日志。

**输出契约**：报告 = 动作 + 对象（槽号或"日志"）+ USB 路径（原样 `/MSSONY/PRO/CAMERA/HDCU5000`）+ 是否已导出备份 + 待补配项（LAN COM 网络三项）。

## B — 边界

- **不要用本卡**：读灯语（ccu-panel-diagnostics）、读状态画面（ccu-status-screen）、跑硬件诊断（ccu-diagnosis-menu）、补配网络 IP（ccu-network）、RCP 面板侧备份（RCP `file-backup`）。
- **手册警告的失败模式**：
  - 改 DATE&TIME → "本机上存储的所有日志都会被删除"（ce01，第 76 页）；非法日期另触发 `CCU:SET DATE&TIME`（ce25，第 88 页）。二者同源不同机制，须同时提示。
  - RECALL 不加载 LAN COM 的 IP/子网/网关（ce29，第 78 页）——换机恢复后漏配网络。
  - CLEAR ALL / CLEAR 为 EXEC 型不可逆批量删除，无回收（ce03，第 78 页）。
  - 日志仅保留 30 天，超期从最旧删（ce02，第 78 页）——"一个月后再取证"会失败。
- **诚实留白**：手册**未说明** CCU 文件的跨型号/跨固件兼容性，也未给出 RECALL 失败时的排查步骤；导入导出失败的原因（U 盘格式、路径、容量）原书均未展开。遇此类情况应如实告知留白，不编造处置。
- **型号差异**：USB 路径 `/MSSONY/PRO/CAMERA/HDCU5000` 三型号**共用同一字符串**（HDCU5500/3500 亦然，第 78 页）；CCU 文件上限五个、日志 30 天、RECALL 排除网络三项，三型号一致。M09 `READ KEY FROM USB` 涉及选件密钥读取，属选件安装范畴，本卡仅作路径关联提及。
- **作者盲点（阶段 0 批判）**：手册把"改日期清空日志"以 M04 注意事项形式**隐含**，未在日志菜单项说明中重复警示——下游须显式前置该警告；USB 路径约定散见三处（导出/导入/日志导出）却未集中说明。
