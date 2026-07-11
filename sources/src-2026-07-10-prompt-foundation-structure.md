---
type: source
id: src-2026-07-10-prompt-foundation-structure
status: active
evidence_status: original
origin: Prompt Atlas training conversation
captured: 2026-07-10
immutable: true
used_by:
  - ../guides/prompt-foundation-structure.md
  - ../templates/prompt-pair.md
  - ../CLAUDE.md
---

# Prompt foundation structure source

> 用户定义的第一阶段 Prompt 训练结构：目标不是写得高级，而是先保证模型进入正确的问题空间，并做到内容、边界与任务对齐。

## Core requirement

优先训练 `Goal → Context → Boundary → Immediate Task → Done`；不要从 Task 开始。完整结构还包括 Design Intent 与 Expected Output，但它们只在会改变判断或后续消费时加入。

## Promotion note

这是一条训练 schema 的原始依据，不是单个 Prompt Pair。后续所有 Phase 1 Final Prompt 应按此结构输出。