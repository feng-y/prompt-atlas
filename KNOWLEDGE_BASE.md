# Prompt Atlas 知识库合同

Prompt Atlas 采用 Karpathy 式三层模型，但只服务 Prompt 表达训练与 Agent 协作。`README.md` 是项目入口，`index.md` 是内容入口。

## 三层模型

| 层 | 本仓库位置 | 所有者与规则 |
| --- | --- | --- |
| Source | `sources/` + `inbox/` | 人提供；`sources/` 不可改写，`inbox/` 是待处理队列 |
| Compiled wiki | `prompt-pairs/`、`principles/`、`patterns/`、`case-studies/`、`harness/`、`maps/` | Agent 维护结构、链接与综合；任何结论必须能回指来源 |
| Schema | `AGENTS.md`、`CLAUDE.md`、模板、本文 | 人与 Agent 共同演化；定义 ingest、query 与 lint |

GitHub 是版本、协作与审计真源；具体事实的证据真源是 source record，而不是 Agent 生成的综合页。

## 知识提升

`inbox → sources → prompt-pairs / case-studies → principles / patterns / harness`

- `inbox/`：原始 Prompt、临时摘录、未验证想法；可整理或丢弃。
- `sources/`：已纳入判断依据的不可变来源；保留原文、稳定摘录或可追溯定位。
- `prompt-pairs/`：已审阅案例，必须保留原始表达与证据状态。
- `principles/`、`patterns/`、`harness/`：只接受重复验证、可降低未来成本、非一次性且不重复的知识。
- `case-studies/`：保留真实任务的 Prompt → evidence → result → verdict。

## Operations

### Ingest

处理一个新来源时：注册 source record → 读取并讨论关键结论 → 只更新必要的 wiki 页面 → 更新 `index.md` → 向 `log.md` 追加记录 → 报告待确认项。一个来源可以影响多页；不得只新增摘要而不检查相关综合页。

### Query

回答前先读 `index.md`，再读最少量的相关来源与 wiki 页面。回答中区分来源事实、当前综合与不确定项。只有用户明确要求沉淀时，才把查询结果写回 wiki。

### Lint

按需运行健康检查：来源是否有 downstream links、案例是否缺证据状态、原则是否缺验证、是否存在孤立页、交叉引用是否过时、是否有新来源挑战旧结论。先报告；只有机械且无歧义的修复才可直接完成。

## 跨工具交互

| Surface | 读取入口 | 写入纪律 |
| --- | --- | --- |
| ChatGPT | README → index → 相关页 | 默认读与建议；明确授权后才写入 |
| Codex | README → AGENTS → index | 创建可审阅变更；除非明确要求，不直接合并 |
| Claude Code | README → CLAUDE → AGENTS → index | 在本地 repo 按同一 schema 操作 |
| Obsidian | 直接打开 repo 根目录 | 浏览、搜索、链接、人工编辑后 Git 同步 |