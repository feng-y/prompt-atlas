---
type: source
id: src-2026-07-23-recent-prompt-contract-lessons
status: active
evidence_status: original
origin: ChatGPT project conversation
captured: 2026-07-23
immutable: true
used_by:
  - prompt-pairs/01-task-context/005-slot-config-usage-first-convergence.md
  - prompt-pairs/06-review/005-inference-merge-semantic-drift-review.md
  - prompt-pairs/11-loop/004-ticket-frontier-continuous-loop.md
---

# 最近工程 Prompt：自治空间、语义漂移与连续 ticket loop

> 记录 2026-07-21 至 2026-07-23 的真实工程 Prompt 讨论，用于保留最近一次 Prompt 质量纠偏与三个高价值案例的原始依据。

## Provenance

- 原始位置 / URL：Prompt Studio 项目内 ChatGPT 会话
- 作者或会话：用户与 ChatGPT；DaVinci / Mycroft / inference / harness 相关工程讨论
- 获取方式：当前项目会话原始输入与改写记录
- 许可或隐私边界：仅保留 Prompt 学习所需的工程表达，不复制无关内部实现细节

## Content or excerpt

### 1. 连续 ticket frontier

用户提供已经落盘的 05–09 tickets 与依赖图，并明确指出：这里应该是“一个个 loop 持续推进”，而不是每个 ticket 都重新等待人工 trigger。

核心约束包括：05 是唯一初始 frontier；06/07 被 05 阻塞；08 被 06/07 阻塞；09 被 08 阻塞。无真实 human-only blocker 时应根据本地 tracker 和依赖图自动继续。

### 2. `ModelInputConfig` 的 slot 数据收敛

用户指出 `ModelInputConfig` 中多个字段都与 slot 相关，希望进一步分析每个字段的真实使用场景、是否仍需要、字段逻辑以及是否可以聚合。

第一次改写把 investigation 写成了较细的逐项 checklist。用户随后明确反馈 Prompt 质量下降，并提醒应回到 GPT-5.6 风格的 outcome / context / constraints / 重点提醒 / output，而不是替模型规定调查步骤。

纠偏后的目标是：让模型基于 repo evidence 判断字段语义、生命周期、生产消费关系、新旧结构替代关系和聚合边界；不预设 `model_slot_opt` 必然是 canonical representation，也不机械创建新的 wrapper struct。

### 3. inference 实现与 merge 无漂移 Review

用户要求 review 当前分支的 inference 实现逻辑、形成实现总结，同时验证原有 merge 模块没有逻辑漂移。

核心 review 对象不是一般代码质量，而是两个 outcome：新 inference 路径是否成立，以及稳定 merge 语义是否被意外改变。需要区分新增实现自身 correctness、对已有 merge 的 semantic drift、可接受的 observability 差异、scope creep 和仍未验证的 unknown。

## Processing notes

- 影响了哪些 wiki 页面：三个 Prompt Pair；index；operations log
- 仍待核验的部分：三个 Prompt 的真实 runtime / branch outcome 尚未回填，因此仅形成 case-level candidate，不提升为全局 principle
- log entry：2026-07-23 ingest | Recent prompt contract lessons
