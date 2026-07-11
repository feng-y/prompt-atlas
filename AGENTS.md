# Prompt Atlas Agent Guide

## Start Here

每次任务先读 `README.md`、`AGENTS.md`、`index.md`，再按 index 进入最少量的相关页面。不要把整个仓库一次性塞进上下文。

## Roles

- 人：选择来源、解释关注点、决定是否接受本轮综合。
- Agent：摘要、交叉引用、维护索引、标记矛盾与缺口。
- Source：事实依据；不得被 Agent 改写。
- Wiki：可更新的综合层；不得脱离 source 声称事实。

## Ingest

当用户提供新 Prompt、聊天摘录、文章或执行结果：

1. 判断它只是临时输入还是会成为判断依据。
2. 临时输入放 `inbox/`；判断依据先按 `templates/source-record.md` 注册到 `sources/`。
3. 读取 source 与 `index.md`，找出最多 1–3 个应更新的已有页面。
4. 新建或更新 Prompt Pair / Case Study / principle；保留证据状态，不伪造原文。
5. 更新 `index.md` 的一行摘要或链接。
6. 向 `log.md` 追加 `## [YYYY-MM-DD] ingest | Title`，说明来源、影响页面和未确认项。
7. 报告本轮没有提升的候选知识；不要自动提升。

## Query

先从 `index.md` 定位，再读相关 source 与 wiki 页面。输出时区分：source fact、current synthesis、inference、open question。查询结果只有在用户明确要求沉淀时才写回。

## Lint

按用户要求或来源累计后运行。检查：

- source 是否没有 downstream page；
- Prompt Pair 是否缺 Current Prompt、Minimal Rewrite、证据状态或 Outcome；
- principle / pattern 是否缺来源或重复验证；
- 孤立页、陈旧链接、相互矛盾的综合；
- 新来源是否改变旧结论。

先给健康报告。仅对无歧义的机械问题直接修复；矛盾、删改、提升或降级都要求用户判断。

## Write Rules

- 原始 Prompt 与 source 不得被改写；改写稿另存。
- 使用标准 Markdown 与相对链接；不要加入 Obsidian 专属格式、RAG 或数据库。
- 改变 schema、索引或原则时，检查其他 Agent 的读取路径。
- ChatGPT 默认分析与建议；只有用户明确要求才写入。Codex / Claude Code 保留可审阅 Git 变更。

完成时说明：处理了哪些来源、更新了哪些 wiki 页面、证据状态与下一位 Agent 的继续入口。