# sony-ccu-rcp-system

把 Sony 两本官方使用说明书蒸馏成的一个 **AI Agent 技能包**：RCP-3500/3501 遥控面板（控制端）+ HDCU5000/5500/3500 摄像机控制单元（被控端），共 **31 项能力**，按用户意图路由到对应能力卡执行。

> 这不是书摘，是一条蒸馏流水线（[cangjie-skill](https://github.com/VINK77aaaa) 阶段 0→5）的产物：268 条候选 → 三重验证 → 31 项能力 → 85 条压力测试用例实测通过。

## 它解决什么

演播室里，"面板拧不动""画面没信号""HDR 输出不对"这类问题的排查，往往要在**两本厚手册**之间来回翻。这个技能包把两端合并成**一条链**：

```
系统级决策（型号 + 选件）
   ├─ 面板侧：CNS 组网模式 → 面板 IP / RCP 编号 → 控制权仲裁 → 日常调整 → 参数资产
   └─ 主机侧：CABLE TYPE → SYSTEM / CAMERA FORMAT / 传输速率 → 输出/返回格式（派生查表）
                          → GENLOCK / PTP 同步 → 网络与 IP → 诊断
```

关键结构发现：**主机侧所有输出/返回格式都不是自由设定，而是 `CABLE TYPE × FIBER TRANSMIT RATE × SYSTEM × CAMERA FORMAT` 的派生查表结果**。能力卡围绕这条链组织，而不是围绕手册目录。

## 安装

仓库根目录就是一个可直接安装的 single 模式技能。把它放进宿主环境的 skills 目录即可：

```bash
git clone https://github.com/VINK77aaaa/sony-ccu-rcp-system.git
cp -r sony-ccu-rcp-system ~/.claude/skills/          # Claude Code
# 或 ~/.agents/skills/、<project>/.claude/skills/ 等宿主约定目录
```

安装后只有一个可发现入口 `sony-ccu-rcp-system`，31 张能力卡作为 `references/capabilities/*.md` 内部路由。

**触发示例**（说人话即可）：

- "新到一台 RCP-3500，要接进现有摄像机系统，该选哪个连接模式？"
- "HDCU5500 上 1080/59.94P 时 SDI-OUT3 能出哪些格式？"
- "面板上的 NETWORK 灯在闪，CCU 前面板的 NETWORK 灯也在闪，含义一样吗？"
- "整套系统不通，画面没信号，第一步该看哪一层？"

## 目录结构

| 路径 | 是什么 |
|---|---|
| `SKILL.md` | 技能入口：触发范围、7 条核心原则、31 行能力路由表、判停条件 |
| `references/capabilities/*.md` | **31 张能力卡**（R/I/A1/A2/E/B 六段：原文依据 / 自述 / 书中配置示例 / 未来触发 / 执行步骤 / 边界） |
| `references/overview.md` | 随包概览：两书骨架、跨书依赖链、咬合点速查、合辑级缺口清单 |
| `references/glossary.md` | 术语表 **128 条**（RCP 35 + CCU 93），含**跨书术语对照 12 组** |
| `references/cheatsheet.md` / `capability-index.md` | 一句话规则速查 / 完整意图索引 |
| `BUILD_MANIFEST.json` | 构建清单：36 个文件哈希 + bundle 哈希 + 输出模式决策 |
| `DIGEST.md` | **给人读的精华长文**（约 7,900 字，12 章，含 10 条陷阱与作者局限） |
| `bundle/` | **可复现的编译事实源**：`verified.yaml` + `destinations.json` + 31 张源卡 + `book/` |
| `tests/` | 阶段 4 压力测试：85 条用例、机械判分明细、测试报告、断言修正审计、盲测原始回答 |
| `docs/` | 流水线状态、完成报告、编译运行记录 |

## 能力版图（31 项）

| 面 | 面板侧（13） | 主机侧（16） | 跨书（2） |
|---|---|---|---|
| 控制 / 组网 | 组网连接与配置、MCS 多机操作、工程师模式与安全代码 | 传输方式决策、系统格式、网络与 IP、IP Live 与第三方协议 | 整系统组网与联调 |
| 信号 / 画质 | 摄像机日常操作、白黑闪光平衡、Paint 图像调整、场景文件 | 输出/返回格式派生查表、HDR 配置、同步 GENLOCK-PTP、音频与对讲、干线与提示机 | — |
| 资产 / 操作 | USB 备份与初始化、自定义 | CCU 文件与日志、本机菜单操作、Web 菜单 | — |
| 观测 / 排障 | 面板灯语诊断、维护校正 | 前面板灯语诊断、状态画面判读、DIAGNOSIS 硬件诊断 | 整系统联合排障 |
| 速查 | 规格速查、环境红线 | 接口规格与环境速查 | — |

其中 7 项在 compact pack 模式下会被晋级为独立技能（`network-setup`、`mcs-operations`、`led-diagnostics`、`daily-operation`、`engineer-mode-security`、`ccu-transport-setup`、`system-troubleshooting`）。

## 压力测试

`tests/` 里是完整可查的证据，**不是自我评分**：

- **85 条用例** = 46 触发/路由 + 39 任务执行（154 条机械断言）
- **5 个独立 sub-agent 盲测**（看不到预期答案与断言）
- **路由 46/46** —— 含 **8 条跨书近邻负例**（面板灯语 ↔ 主机灯语、面板网络 ↔ 主机网络、面板文件 ↔ 主机文件、面板规格 ↔ 主机规格、单侧排障 ↔ 整系统排障、面板画质 ↔ 主机 HDR、控制权仲裁 ↔ 投运联调）+ 2 条越界负例，**兄弟混淆 0**
- **任务 39/39，断言 154/154**；关键真值抽查 17/17 与能力卡**逐字同源**（数值/单位/格式串零改写）
- 3 条边界用例（缺输入 / 手册留白）均**正确判停、未编造处置步骤**
- 首轮有 8 条断言失败，经回原文核对**全部判定为测试设计缺陷**（断言超出 prompt 提问范围 / 分隔符容差过严），修测试并留审计，另拆 5 条回归用例重测通过 —— 明细见 `tests/assertion-fixes.json` 与 `tests/test-results.md`

## 重新编译（可复现）

`bundle/` 是编译的唯一事实源。改动能力卡后重新编译：

```bash
python3 scripts/cangjie.py compile \
  --bundle bundle \
  --out dist/sony-ccu-rcp-system \
  --output single --yes
```

编译前请比对 `BUILD_MANIFEST.json` 的 `published_hashes`，检测到本地手改不要静默覆盖。

## 已知缺口（如实列出，未补造）

1. **第 67 页 HFR ↔ BNC Link 编配表**：PDF 纯文本提取时列对齐丢失，须回查原图。已在 `ccu-format-lookup` 卡边界段声明依据不完整。
2. **`PsF` / `SQD-2SI` / `UHB`**：手册只使用未定义，术语表中标 `†` 并注明"释义含行业通用知识、来源非手册"。
3. **手册故意留白**：多处"请联系 Sony 维修代表或销售代表"（SFP+ 型号清单、电源电压切换、选件板安装步骤、`CABLE ALARM SHORT` 处置）→ 作为能力卡边界交付。
4. **跨书缝 5 条**：无统一"两端编号 ↔ 机位"对照表；"重启所有摄像机系统"作用域未定义；**RCP-3500/3501 供电来源两书描述不一致**；错误与权限两端不对称；选件↔能力映射每本书都是单端的。
5. **CNS 模式集合不对等**：面板侧四模式（含 PC 控制）/ 主机侧三模式（无 PC 控制）——合并时才暴露的缺口。

## 来源与版权

见 [NOTICE.md](NOTICE.md)。本仓库是对 Sony 官方使用说明书的**独立技术整理**，与 Sony 无关联；引文均标注页码，未随仓库分发手册全文。

## 说明

- 文档中出现的本机绝对路径已匿名为 `~`；`dist/` 前缀已按仓库根布局重写。
- **本仓库未附开源许可证**（默认保留所有权利）。如需他人复用，请自行添加 LICENSE。
