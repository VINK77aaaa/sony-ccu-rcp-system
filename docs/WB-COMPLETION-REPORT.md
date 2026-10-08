# WB 完成报告 — sony-ccu-rcp-system（Sony CCU + RCP 合辑技能包）

- 完成日期：2026-10-08
- 流水线：cangjie-skill v2.5.0（阶段 0 → 5 全部完成）
- 目标：把《摄像机控制单元 HDCU5000/5500/3500 使用说明书》（Sony 2019，5-006-304-43 (1)，94 页）走完整条蒸馏流水线，并与已交付的 RCP-3500/3501 技能包**合并为单一 bundle**，编译安装为一个技能。

## 1. 交付物清单

| 交付物 | 路径 | 规模 |
|---|---|---|
| **已安装技能包** | `~\.agents\skills\sony-ccu-rcp-system\` | 36 文件；0 errors / 0 warnings |
| 构建清单 | 同上 `BUILD_MANIFEST.json` | 36 个 published_hashes + bundle_sha256 + decision |
| **精华长文** | `books/sony-ccu-rcp-system/DIGEST.md` | 7,927 中文字 / 39,044 字节，12 章，19 条卡链接全有效 |
| 编译事实源 | `books/sony-ccu-rcp-system/bundle/verified.yaml` | 31 能力 / 72,845 字节 |
| 能力卡 | `.../capabilities/cards/*.md` | 31 张（RCP 13 逐字沿用 + CCU 18 新写），均含 R/I/A1/A2/E/B 六段 |
| 去向映射 | `.../capabilities/destinations.json` | 7 promoted + 24 served_by；可发现入口 8/8 |
| 随包概览 | `.../capabilities/book/overview.md` | 17,977 字节 |
| 随包术语表 | `.../capabilities/book/glossary.md` | 128 条 / 93,708 字节 |
| 压力测试 | `books/sony-ccu-rcp-system/stage4/` | test-prompts.json(85 例) / _score.json / test-results.md / assertion-fixes.json / parts/ |
| 编译产物 | `books/sony-ccu-rcp-system/dist/` | 36 文件 |
| CCU 单书过程产物 | `books/hdcu-5000-5500-3500-manual/` | BOOK_OVERVIEW / candidates(268) / verified(63) / references(158) / needs-review(4) / rejected(43) / coverage-audit / GLOSSARY(93) / PIPELINE_STATE |
| 流水线状态 | `books/sony-ccu-rcp-system/PIPELINE_STATE.md`、`books/hdcu-5000-5500-3500-manual/PIPELINE_STATE.md` | 全阶段完成 |

## 2. 各阶段结果

| 阶段 | 结果 |
|---|---|
| 0 整书理解 | CCU 书骨架 7 章 + 18 项原书任务；**关键结构发现**：所有输出/返回格式都是 `CABLE TYPE × FIBER TRANSMIT RATE × SYSTEM × CAMERA FORMAT` 的派生查表结果。已获用户确认（"大致正确，越详细越好"）。 |
| 1 五路并行抽取 | 268 条候选（框架 38 / 原则 80 / 案例 17 / 反例 40 / 术语 93） |
| 1.5 三重验证 | 63 verified / 158 reference / 4 needs_review / 43 rejected = 268（无静默丢弃）；18 项任务全覆盖 |
| 1.6 晋级门 | 18 个新能力全部过门；**7 promoted**（5 RCP + `ccu-transport-setup` + `system-troubleshooting`）；可发现入口 8/8 |
| 2 RIA++ 能力卡 | 18 张新卡（5 路子代理并行）+ 13 张 RCP 卡逐字沿用 = 31 张 |
| 3 Zettelkasten | 合并 `overview.md`（含跨书依赖链图 + 咬合点四面表 + 合辑级缺口清单）+ `glossary.md`（128 条 + **跨书术语对照 12 组**） |
| 4 压力测试 | **85/85 通过**（详见下） |
| 5 编译与交付 | single 编译 → 安装 → DIGEST → BUILD_MANIFEST；取代旧包 |

## 3. 压力测试结果（阶段 4）

- 用例集 **85 例**：46 触发/路由（7 promoted 触发 + 24 router 可达 + 8 跨书近邻负例 + 2 越界负例）+ 39 任务执行（154 条机械断言）。
- 方式：**5 个独立 sub-agent 盲测**（1 路由 + 4 任务分组），均未参与蒸馏、看不到预期答案与断言。
- 结果：**路由 46/46**（兄弟混淆 **0**，近邻与越界负例 15/15）；**任务 39/39，断言 154/154**；关键真值抽查 **17/17** 逐字同源（零改写）；3 条边界用例（缺输入/手册留白）均正确判停、未编造。
- **首轮 8 条断言失败**：逐条回原文核对后**全部判定为测试设计缺陷**（断言超出 prompt 提问范围 / 分隔符容差过严），非能力卡缺陷。按 methodology/06 §110 修测试、留审计（`stage4/assertion-fixes.json`），并把被误挂的 5 项内容**另立回归用例**（`o32`–`o36`）由全新盲测 agent 重测通过。
- **能力卡零改动**：`cards/` 全部 31 张 mtime 早于本轮测试起始 → 无需回炉或重编译。

## 4. 已知缺口（如实列出，未补造）

1. **`f31` · 第 67 页 HFR ↔ BNC Link 编配表**：纯文本列对齐丢失（提取为乱码），须回查原 PDF 图形。已在 `ccu-format-lookup` 卡边界段声明依据不完整。
2. **`h13` / `h14` / `h83`（PsF / SQD-2SI / UHB）**：手册只使用未定义。`glossary.md` 已标 `†` 并注明"释义含行业通用知识、来源非手册"。
3. **手册故意留白**：多处"请联系 Sony 维修代表或销售代表"（SFP+ 型号清单、电源电压切换、选件板安装步骤、`CABLE ALARM SHORT` 处置）→ 作为能力卡边界交付。
4. **跨书缝 5 条**：①无统一"两端编号 ↔ 机位"对照表；②"重启所有摄像机系统"作用域未定义；③**RCP-3500/3501 供电来源两书描述不一致**；④错误与权限两端不对称；⑤选件↔能力映射每本书都是单端的。
5. **新增跨书缺口（合并阶段发现）**：**CNS 模式集合不对等** —— 面板侧四模式（含 PC 控制）/ 主机侧三模式（无 PC 控制）。

## 5. 待用户决策

- ⬜ 是否允许为 `h13` / `h14` / `h83` 写入**行业通用释义**（当前保持"手册未定义"标注）。
- ⬜ 是否授权回读原 PDF **第 67 页图形**以补 `f31`。
- ⬜ 跨书缝 ③（RCP 供电来源冲突）需按实际机型确认。

## 6. 安装与恢复

- 安装位置（用户级）：`~\.agents\skills\sony-ccu-rcp-system\`
- 旧包处置：原 `rcp-3500-3501-panel` **已移出**（非删除）到 `~\.agents\_superseded\rcp-3500-3501-panel`。
  - 理由：合并包已覆盖原 RCP 单书全部 13 项能力，同时保留会造成同一 RCP 意图被两套 description 重复覆盖（methodology/07 §72 二选一原则）。
  - 恢复：把该目录移回 `~\.agents\skills\` 即可。
- RCP 原 bundle（`books/rcp-3500-3501-manual/`）与全部过程产物**保留不动**。

## 7. 后续可选

- 持续进化：`darwin evolve books/sony-ccu-rcp-system/` —— 会用 `stage4/test-prompts.json` 做 ratcheting 自动进化。
- 重编译/更新前请比对 `BUILD_MANIFEST.json` 的 `published_hashes`，检测到本地手改不得静默覆盖。
