# Prompt Atlas Agent Guide

## Start Here

每次任务先读 README.md、KNOWLEDGE_BASE.md 与目标目录的 README、模板或案例。不要把整个仓库一次性塞进上下文；从入口和任务层开始，按链接扩展。

## Knowledge Routing

- 原始或未审阅内容 → inbox/
- 完整 Prompt Pair review → prompt-pairs/
- 已重复验证的可迁移规律 → principles/ 或 patterns/
- 端到端任务证据 → case-studies/
- 稳定 context / guardrail / verification 合同 → harness/

不得把临时过程、单次推测或没有证据状态的总结写进长期层。

## Write Rules

- 保留原始 Prompt；改写稿不得覆盖原文。
- 每个新 Prompt Pair 使用 templates/prompt-pair.md，并标注证据状态。
- 每条长期知识说明来源、适用边界和提升理由。
- 只使用标准 Markdown 与相对链接；不要引入应用专属格式或数据库。
- 改变 README、路由规则或原则时，检查其他 Agent 的读取路径。

## Surface-specific behavior

- ChatGPT：默认分析与建议；仅在用户明确要求写入仓库时修改文件。
- Codex / Claude Code：在明确任务范围内编辑，保留可审阅 Git 变更；未经明确授权不直接合并。
- Obsidian：视为 Git 工作副本的 UI，不维护独立真源。

完成时说明新增或更新了哪些知识层、证据状态，以及下一位 Agent 从哪里继续。