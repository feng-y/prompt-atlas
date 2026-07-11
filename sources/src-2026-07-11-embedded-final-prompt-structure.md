---
type: source
id: src-2026-07-11-embedded-final-prompt-structure
status: active
evidence_status: original
origin: ChatGPT project conversation
captured: 2026-07-11
immutable: true
used_by:
  - guides/prompt-foundation-structure.md
  - templates/prompt-pair.md
  - principles/transferable-principles.md
  - AGENTS.md
  - CLAUDE.md
---

# Embedded Final Prompt structure decision

> 本来源记录用户对 Prompt Atlas Final Prompt 形态的明确纠正：Foundation 是内容检查框架，不是最终 Prompt 的显式段落模板。

## Provenance

- 原始位置 / URL：ChatGPT 项目会话，未公开链接
- 作者或会话：用户与 ChatGPT
- 获取方式：用户明确要求基于此约束调整 repo 全部样例
- 许可或隐私边界：仅保存与 Prompt Atlas 写作规范直接相关的决定

## Content or excerpt

用户明确指出：

> 当前很多样例按照 `Goal → Decision Context → Control Boundary → Immediate Task → Observable Evidence` 这个模板来写，但是把段落结构也写到内容里面了。Final Prompt 应该是一个嵌入的 Markdown 结构，不包含实际的段落名称。

由此形成的约束：

- `Goal / Decision Context / Control Boundary / Immediate Task / Observable Evidence` 用于写作前检查和 review。
- Final Prompt 应将这些信息自然嵌入段落，而不是默认显示为 `### Goal`、`### Boundary` 等标题。
- 分析结构可以显式，最终可复制产物应自然、连续，并位于 Prompt Pair 页面末尾。
- 只有当任务本身需要正式合同、表格或分段交付时，才因使用价值保留标题，而不是为了展示 Prompt 模板。

## Processing notes

- 影响页面：Foundation guide、Agent/Claude entry、Prompt Pair template、principles、全部现有 Prompt Pair
- 不修改：原始 source 与 Current Prompt
- log entry：`[2026-07-11] schema | Embed foundation in Final Prompt`
