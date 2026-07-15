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

## Prompt Pair final artifact

分析部分用于学习；页面末尾的 `Final Prompt` 才是唯一可发送产物。使用 [Prompt Foundation Structure](guides/prompt-foundation-structure.md) 检查 Goal / Outcome、Decision Context、Available Evidence、Constraints / Approval Boundary、Immediate Task、Success Criteria 与 Stop Rules 是否在语义上足够清楚。

这些维度不是默认成稿标题。Final Prompt 应是自然、连续、可直接复制的 Markdown。先删除重复规则、无效过程说明和无关工具，再补最小的行为差异信息。只有任务本身需要正式合同、多人交接、结构化返回或 Harness 消费时，才因实际使用价值采用标题或列表。

Prompt 是 Task Contract，不是 execution script。不要把模型已经能可靠完成的搜索、思考、工具选择和 review 步骤写死；但必须保留真实 invariant、权限边界、验证要求和停止条件。

## Lint

按用户要求或来源累计后运行。检查：

- source 是否没有 downstream page；
- Prompt Pair 是否缺 Current Prompt、Minimal Rewrite、证据状态、Outcome 或末尾的 Final Prompt；
- Final Prompt 是否缺目标、当前判断、可用证据、必要约束、即时任务、成功标准或停止规则；
- 是否把 evidence 写成无条件固定读取顺序，或把 judgment rule 错写成 ALWAYS / NEVER；
- 是否存在重复、矛盾、无效示例、无关工具或模型已可靠具备的过程脚手架；
- 自治和审批边界是否清楚，是否从研究 / 设计静默越过到实现或外部写入；
- Final Prompt 是否机械泄漏教学栏目；
- Final Prompt 是否唯一、完整、可直接发送，且没有混入分析或备选方案；
- principle / pattern 是否缺来源或重复验证；
- 孤立页、陈旧链接、相互矛盾的综合；
- 新来源是否改变旧结论。

先给健康报告。仅对无歧义的机械问题直接修复；矛盾、删改、提升或降级都要求用户判断。

## Write Rules

- 原始 Prompt 与 source 不得被改写；改写稿另存。
- Prompt Pair 的学习分析在前；唯一可发送的 `## Final Prompt` 必须是页面最后一节。
- Foundation 用于检查内容，不用于强制 Final Prompt 的可见段落结构。
- 不把官方建议直接提升为已验证 principle；先在真实 Prompt 和代表性 eval 中验证。
- 使用标准 Markdown 与相对链接；不要加入 Obsidian 专属格式、RAG 或数据库。
- 改变 schema、索引或原则时，检查其他 Agent 的读取路径。
- ChatGPT 默认分析与建议；只有用户明确要求才写入。Codex / Claude Code 保留可审阅 Git 变更。

完成时说明：处理了哪些来源、更新了哪些 wiki 页面、证据状态与下一位 Agent 的继续入口。
