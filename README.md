# Prompt Atlas

从真实工作 Prompt 中训练表达能力：把“任务描述”提升为清晰、自然、可验证的 **Task Contract**。

Prompt Atlas 既是 Prompt Studio，也是一个由 Agent 持续维护的垂直 LLM Wiki：来源保留为证据，案例与综合页被逐步编译、交叉链接和复核。

Prompt 的职责不是替模型编写执行脚本，而是定义足够清楚的目标、决策上下文、可用证据、约束、成功标准和停止条件。执行路径、工具选择与迭代方式，应在这些合同内由模型与 Harness 决定。

## Start here

- [Content index](index.md) — 查找具体页面时的第一入口
- [Knowledge Base Contract](KNOWLEDGE_BASE.md) — 来源、wiki 与提升规则
- [Operations log](log.md) — 最近的 ingest、promote、lint
- [Agent Guide](AGENTS.md) — 跨 ChatGPT / Codex / Claude Code 的操作合同
- [Prompt Atlas Map](maps/prompt-atlas.md) — 按当前目标导航
- [Prompt Foundation Structure](guides/prompt-foundation-structure.md) — 第一阶段的固定 review 骨架

## 训练目标

- 先定义用户真正需要的结果，而不是先罗列步骤
- 提供会改变判断的 Current Context 与 Available Evidence
- 只保留真实约束、权限边界和必要工具规则
- 明确本轮任务、成功标准和停止条件
- 给模型足够自治空间，但不让它越过研究、设计、实现或外部写入边界
- 以可观察证据和验证结果定义完成，而不是用“做完、优化好”代替验收
- 用代表性任务逐项验证 Prompt 改动，不整体重写一个已经工作的 Prompt stack

## 当前 Wiki

| 页面类型 | 作用 |
| --- | --- |
| [Sources](sources/README.md) | 不可改写的事实依据、历史摘录与外部材料 |
| [Prompt Pairs](prompt-pairs/README.md) | 原始表达 → 分析 → 最小改写 → Contract 变化 → 原则 → 可直接发送的 Final Prompt |
| [Principles](principles/transferable-principles.md) | 重复验证后的可迁移判断 |
| [Patterns](patterns/README.md) | 多个案例反复出现的结构或触发模式 |
| [Case Studies](case-studies/README.md) | Prompt 到真实结果的端到端证据 |
| [Harness](harness/README.md) | 稳定 context / guardrail / tool routing / verification 合同 |

## 使用方式

1. 新 Prompt 先进入 [inbox/](inbox/README.md)。
2. 被纳入判断依据的聊天、文章或执行结果，创建 [source record](templates/source-record.md)。
3. Agent 按 ingest 更新少量相关案例、原则或地图；不把每次会话直接写成永久知识。
4. 先以 [Prompt Pair 模板](templates/prompt-pair.md) 做 review。
5. 先删除重复过程指令，再只补会改变行为的最小合同信息。
6. 只有经过真实任务验证的规律，才提升到 principles 或 patterns。

## 边界

GitHub 是版本、协作与审计真源；`sources/` 是具体事实的证据真源。Obsidian 直接打开本仓库用于浏览和编辑，不维护独立数据。当前不使用向量库、RAG、MCP 或 Obsidian 专属格式；在规模真正需要前，由 `index.md` 完成导航。
