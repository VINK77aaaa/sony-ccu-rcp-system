# PIPELINE_STATE — sony-ccu-rcp-system（合并 bundle）

> cangjie-skill 流水线状态记录（**合并阶段 4–5 的权威状态文件**）。
> 阶段 0–3 的过程状态见两个来源工作目录：
> - `books/rcp-3500-3501-manual/`（RCP-3500/3501，阶段 0–5 已全部完成并交付）
> - `books/hdcu-5000-5500-3500-manual/`（HDCU5000/5500/3500，阶段 0–3 已完成）

## 基本信息

- **bundle_id**: `bundle.sony-ccu-rcp-system`
- **entry.name**（single 主入口）: `sony-ccu-rcp-system`
- **book.title**: Sony 摄像机控制系统使用说明书合辑（RCP-3500/3501 遥控面板 + HDCU5000/5500/3500 摄像机控制单元）
- **来源**: Sony 2019 两本官方说明书 — 5-017-036-61 (1)（56 页）+ 5-006-304-43 (1)（94 页）
- **bundle 目录**: `books/sony-ccu-rcp-system/bundle/`
- **输出模式（冻结）**: `single`
- **处理日期**: 2026-10-08

## 阶段进度（合并后）

| 阶段 | 名称 | 状态 | 产出 |
|---|---|---|---|
| 0 | 整书理解（两书各自） | ✅ 完成 | 两书各自 `BOOK_OVERVIEW.md` |
| 1 | 五路并行抽取（两书各自） | ✅ 完成 | RCP 118 条 + CCU 268 条候选 |
| 1.5 | 三重验证（两书各自） | ✅ 完成 | RCP 35/43/… + CCU 63/158/4/43 |
| 1.6 | 晋级门装配（合并） | ✅ 完成 | `verified.yaml`（31 能力）+ `destinations.json` |
| 2 | RIA++ 能力卡（合并） | ✅ 完成 | `cards/` 31 张（RCP 13 + CCU 18） |
| 3 | Zettelkasten 术语/链接（合并） | ✅ 完成 | `book/overview.md` + `book/glossary.md` |
| 4 | 压力测试（合并） | ✅ 完成 | `stage4/test-prompts.json`(85 例) + `_score.json` + `test-results.md`；**85/85 通过** |
| 5 | 编译与交付（合并） | ✅ 完成 | `dist/` + `DIGEST.md`(7,927 中文字) + 安装到 `~\.agents\skills\sony-ccu-rcp-system\` |

## 阶段 5 结果

- **编译**：`cangjie.py compile --bundle bundle --out dist --output single --yes` → run-20261008-190940-86a4cf；`dist/` 36 个文件；`validate_skill_pack.py` **0 errors**。
- **DIGEST.md**：7,927 中文字 / 39,044 字节；12 个二级章节（按两书骨架组织，非按能力卡列表）；19 条能力卡链接全部有效；含「陷阱与反例」10 条 + 「作者的局限」+ 「关键术语速查」+ 「如果只带走三句话」。
- **安装**：`~\.agents\skills\sony-ccu-rcp-system\`（用户级，与 RCP 原包同一位置），36 个文件，`BUILD_MANIFEST.json` 已生成（含全部 published_hashes 与 `bundle_sha256`）。安装后校验 **0 errors / 0 warnings**；抽检 name=`sony-ccu-rcp-system`、路由表 31 行、能力卡 31 张。
- **取代旧包**：`rcp-3500-3501-panel` 已**移出**（非删除）至 `~\.agents\_superseded\rcp-3500-3501-panel`，避免同一 RCP 意图被两套 description 重复覆盖；移回即恢复。RCP 原 bundle 与全部过程产物**保留不动**。

## Bundle 组成（现状）

| 文件 | 规模 | 说明 |
|---|---|---|
| `verified.yaml` | 72,845 B | 31 能力；0 重复 id/slug；0 schema 违规；0 缺卡 |
| `destinations.json` | 1,981 B | 7 `promoted` + 24 `served_by`；budget 8/8 |
| `cards/*.md` | 31 张 | RCP 13 张逐字沿用 + CCU 18 张新写；均含 R/I/A1/A2/E/B 六段 |
| `book/overview.md` | 17,977 B | 两书骨架 + 跨书依赖链 + 咬合点四面表 + 8 条命题 + 缺口清单 + 能力版图 |
| `book/glossary.md` | 93,708 B | 128 条 = RCP 35（`g01`–`g35`）+ CCU 93（`h01`–`h93`）+ 第 0 节跨书对照 12 组 |

**晋级为独立 Skill 的 7 项**：`network-setup`、`mcs-operations`、`led-diagnostics`、`daily-operation`、`engineer-mode-security`、`ccu-transport-setup`、`system-troubleshooting`。
**可发现入口**：1 router + 7 promoted = **8**（软预算 8，顶格）。

## 阶段 4 结果（摘要）

- **用例集**：`stage4/test-prompts.json` = **85 例**（46 触发/路由 + 39 任务执行，154 条断言）；覆盖 7 promoted 触发 + 24 router 可达 + 8 跨书近邻负例 + 2 越界负例 + 3 边界任务。
- **方式**：5 个独立 sub-agent 盲测（1 路由 + 4 任务分组），均看不到预期答案与断言；机械判分。
- **结果**：路由 **46/46**（兄弟混淆 **0**，近邻与越界负例 15/15）；任务 **39/39**，断言 **154/154**；关键真值抽查 **17/17** 逐字同源（零改写）；3 条边界用例均正确判停。
- **首轮失败 8 条断言**：全部经核对判定为**测试设计缺陷**（断言超出 prompt 提问范围 / 分隔符容差过严），非能力卡缺陷；按 methodology/06 §110 修测试并留审计（`stage4/assertion-fixes.json`），另拆出 5 条回归用例（`o32`–`o36`）由全新盲测 agent 重测通过。
- **能力卡零改动**：`cards/` 全部 31 张 mtime ≤ 19:04，早于本轮测试起始 19:09 → 无需回炉、无需重编译。

## 阶段 4 计划（针对合并后 31 能力）

必须覆盖**跨书近邻负例**（两本书各自都通顺、合并后易混淆的对）：

| 近邻对 | 判别要点 |
|---|---|
| `led-diagnostics`（RCP 面板灯语） vs `ccu-panel-diagnostics`（CCU 前面板灯语） | 问的是面板灯还是主机灯 |
| `network-setup`（面板组网/CNS/IP） vs `ccu-network-setup`（主机 LAN-COM/CNS/编号） | 问的是面板侧接入还是主机侧配置 |
| `file-backup`（RCP 文件与 USB 备份） vs `ccu-file-log`（CCU FILE 与日志） | 资产对象是摄像机图像参数还是整机菜单快照 |
| `specs-reference`（RCP 规格） vs `ccu-specs-reference`（CCU 接口规格） | 查哪一端的数值 |
| `paint-adjustment` / `white-black-balance`（面板调画质） vs `ccu-hdr-setup` / `ccu-system-format`（主机调信号） | 创作向调整 vs 输出向配置 |
| 单端卡 vs `system-integration` / `system-troubleshooting` | 是否跨两端整系统 |
| `mcs-operations`（控制权仲裁） vs `system-integration`（组网联调） | 运行时仲裁 vs 装机联调 |

## 阶段 5 计划（冻结）

1. `compile_single.py` 的等价 CLI：`cangjie.py compile --bundle bundle --out <安装目录> --output single --yes`
2. 安装为 `sony-ccu-rcp-system`，**取代**原 `rcp-3500-3501-panel`（避免同一 RCP 意图被两套 description 重复覆盖）。
3. 生成 `DIGEST.md`；`validate_skill_pack.py` 必须 0 errors。
4. RCP 原 bundle 与已安装的 `rcp-3500-3501-panel` **保留不动**（不销毁既有工作）。

## 待办 / 待用户决策

- ⬜ **`h13` / `h14` / `h83`（PsF / SQD-2SI / UHB）是否允许写入行业通用释义** — 手册只使用未定义；当前 `glossary.md` 已按原样标 `†` 并注明"来源非手册"。若不允许，则保持现状。
- ⬜ **是否授权回读原 PDF 第 67 页图形以补 `f31`（HFR ↔ BNC Link 编配表）** — 当前纯文本列对齐丢失，已在 `ccu-format-lookup` 卡的边界段声明依据不完整。
- ⬜ 跨书缝 **c**（RCP-3500/3501 供电来源两书描述不一致）需实际机型确认，已在 `book/overview.md` 与 `glossary.md` 第 0 节双处标注。
