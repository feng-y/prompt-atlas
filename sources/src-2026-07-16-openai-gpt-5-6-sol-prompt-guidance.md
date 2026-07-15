---
type: source
id: src-2026-07-16-openai-gpt-5-6-sol-prompt-guidance
status: active
evidence_status: original
origin: https://developers.openai.com/api/docs/guides/prompt-guidance-gpt-5p6
captured: 2026-07-16
immutable: true
used_by:
  - README.md
  - guides/prompt-foundation-structure.md
  - AGENTS.md
  - templates/prompt-pair.md
---

# OpenAI Prompting Guidance for GPT-5.6 Sol

> OpenAI 官方关于 GPT-5.6 Sol / GPT-5.6 family 的 Prompt、工具、自治边界、检索、验证与停止条件指南。

## Provenance

- 原始位置 / URL：https://developers.openai.com/api/docs/guides/prompt-guidance-gpt-5p6
- 作者或会话：OpenAI Developers
- 获取方式：用户于 2026-07-16 提供官方页面全文
- 许可或隐私边界：公开技术文档；本记录只保存稳定摘要与来源，不复制整篇正文

## Content or excerpt

核心原文结论：GPT-5.6 更适合 outcome-first prompts。Prompt 应定义用户可见结果、重要约束、可用证据、成功标准和停止条件，并给模型空间选择有效路径。

稳定要点：

- 先删除重复规则、无效示例、不会改变行为的过程说明和无关工具。
- 保留结果、成功标准、停止条件、安全 / 业务 / 证据 / 权限约束、必要工具路由和输出合同。
- `ALWAYS` / `NEVER` / `must` 只用于真正 invariant；判断性行为使用 decision rule。
- 明确定义回答、研究、设计、实现、review 与外部写入之间的自治和审批边界。
- 检索、工具调用和循环应由证据缺口驱动；足够回答时停止。
- 长任务只在主要阶段和改变计划的发现处更新，不叙述常规调用。
- 完成前使用可用工具验证；不能验证时说明原因与次优检查。
- 迁移时先保持现有 reasoning effort 和工作 Prompt，逐项删减或做最小修复，并在代表性 eval 上比较。

## Processing notes

- 影响了哪些 wiki 页面：项目定位、Foundation、Agent lint、Prompt Pair 模板与索引
- 仍待核验的部分：官方给出的内部 eval 数字只作为方向性结果，不提升为本仓库通用结论；仍需用 Prompt Atlas 自身代表性任务验证
- log entry：`2026-07-16 ingest | GPT-5.6 Sol task-contract guidance`
