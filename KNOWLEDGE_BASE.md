# Prompt Atlas 知识库合同

Prompt Atlas 是 Git-first、Markdown-only 的知识库：GitHub 是唯一真源；Obsidian 只是本地浏览与编辑界面；ChatGPT、Codex、Claude Code 读取并写回同一份 Markdown。README.md 是唯一项目入口。

## 知识路由

inbox → prompt-pairs → principles / patterns → case-studies

| 层 | 放什么 | 提升条件 |
| --- | --- | --- |
| inbox/ | 原始 Prompt、临时摘录、未验证想法 | 一产生即可；完成 review 后才归档 |
| prompt-pairs/ | 已审阅的 Prompt Pair | 有原文、分析、Minimal Rewrite、Expert Lens、原则与证据状态 |
| principles/ | 跨案例可迁移原则 | 重复验证，能降低未来判断成本 |
| patterns/ | 可复用结构或触发模式 | 同一机制在不同案例稳定出现 |
| case-studies/ | 一次端到端任务证据链 | 需要保留 Prompt → 结果 → verdict |
| harness/ | 稳定 context / guardrail / verification 合同 | 只收录 repo-level 稳定规则 |

只有已验证、可降低后续成本、不是一次性特例、且不会制造重复规则的内容，才能提升为 durable knowledge。

## AI-first Note Contract

新笔记使用 [模板](templates/knowledge-note.md)。标题应直接说明结论或对象；首段用一句话说明为何应被读取；记录 source、evidence 与 status；使用标准 Markdown 相对链接；不要把当前任务过程自动写入长期目录。

## 跨工具交互

| Surface | 读取入口 | 写入职责 |
| --- | --- | --- |
| ChatGPT | README → 本文 → 目标目录 | 评审 Prompt、起草候选知识；仅在明确授权后写入 |
| Codex | README → AGENTS.md → 目标目录 | 批量整理、结构校验、提交变更 |
| Claude Code | README → CLAUDE.md → AGENTS.md | 结合本地 repo 创建或更新知识资产 |
| Obsidian | 直接打开 repo 根目录 | 浏览、搜索、链接、人工编辑后用 Git 同步 |

## 最小验证

- 文件处于正确层级；
- status 与证据状态相符；
- README 或 map 能导航到它；
- 下一位人或 Agent 无需重建上下文就能消费；
- 一次性过程没有被误升为 principle / pattern。