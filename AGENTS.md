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

## Prompt Pair as an evolution record

Prompt Pair 记录一次真实 Prompt 的提升过程，不承担完整的 Prompt review 教程。

页面只需要让读者看清：

- 原 Prompt 是什么；
- 最影响结果的问题与本轮关键改版是什么；
- 最小改写如何体现单一变化；
- 为什么这个变化更可能改善结果；
- 最终可直接发送的 Prompt 是什么。

复杂的 Foundation、Task Contract、自治、审批和工具路由判断放在 Guide 中，由作者在内部使用，不要求在每个 case 中逐项展开。已有 case 不需要仅为追求模板一致而批量重写；只有内容冗余或无法看清提升路径时再渐进收缩。

页面末尾的 `Final Prompt` 是唯一可发送产物。它应是自然、连续、可直接复制的 Markdown，不机械泄漏教学栏目。

## Lint

按用户要求或来源累计后运行。检查：

- source 是否没有 downstream page；
- Prompt Pair 是否缺 Current Prompt、清楚的改版说明、Minimal Rewrite、证据状态、Outcome 或末尾的 Final Prompt；
- case 是否为了展示方法而逐项复述 Foundation、Contract 或 Harness 分析，导致提升主线被淹没；
- Final Prompt 是否缺真正会影响任务结果的目标、上下文、边界或完成标准；
- 是否存在重复、矛盾、无效示例、无关工具或不必要的过程脚手架；
- 自治和审批边界是否清楚，是否从研究 / 设计静默越过到实现或外部写入；
- Final Prompt 是否唯一、完整、可直接发送，且没有混入分析或备选方案；
- principle / pattern 是否缺来源或重复验证；
- 孤立页、陈旧链接、相互矛盾的综合；
- 新来源是否改变旧结论。

先给健康报告。仅对无歧义的机械问题直接修复；矛盾、删改、提升或降级都要求用户判断。

## Write Rules

- 原始 Prompt 与 source 不得被改写；改写稿另存。
- Prompt Pair 的分析服务于展示提升过程，不追求覆盖所有 review 维度。
- 唯一可发送的 `## Final Prompt` 必须是页面最后一节。
- Foundation 用于内部检查，不用于强制 case 分析结构或 Final Prompt 的可见段落结构。
- Guide 解释方法，case 展示改版；不要把 Guide 内容复制到每个 case。
- 不把官方建议直接提升为已验证 principle；先在真实 Prompt 和代表性 eval 中验证。
- 使用标准 Markdown 与相对链接；不要加入 Obsidian 专属格式、RAG 或数据库。
- 改变 schema、索引或原则时，检查其他 Agent 的读取路径。
- ChatGPT 默认分析与建议；只有用户明确要求才写入。Codex / Claude Code 保留可审阅 Git 变更。

完成时说明：处理了哪些来源、更新了哪些 wiki 页面、证据状态与下一位 Agent 的继续入口。
