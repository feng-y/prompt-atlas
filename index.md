# Prompt Atlas Index

> 内容目录：先在这里定位，再读取少量相关页面；不要把整个仓库作为默认上下文。

## Start

- [Project entry](README.md) — 项目定位与使用方式
- [Knowledge Base Contract](KNOWLEDGE_BASE.md) — 来源、wiki 与提升规则
- [Agent Guide](AGENTS.md) — ingest / query / lint 操作
- [Operations log](log.md) — 最近发生过什么

## Sources

- [Prompt Atlas bootstrap conversations](sources/src-2026-07-10-prompt-atlas-bootstrap.md) — v0.1 案例的历史依据；证据状态为 excerpted
- [Embedded Final Prompt structure decision](sources/src-2026-07-11-embedded-final-prompt-structure.md) — Foundation 用于检查，Final Prompt 自然嵌入结构
- [Five Prompt style baselines](sources/src-2026-07-11-five-prompt-style-baselines.md) — 五类学习方向与统一自然成稿规则
- [Sol general work and delegation](sources/src-2026-07-11-sol-general-work-and-delegation.md) — Prompt 之后进入真实工作委托的方向性来源；外部产品与指标仍待核验

## Phase 1 training

- [Prompt Foundation Structure](guides/prompt-foundation-structure.md) — 用 Goal / Context / Boundary / Task / Evidence 检查内容，但不把它们机械写成成稿标题
- [Five Prompt Style Baselines](guides/five-prompt-style-baselines.md) — Anthropic、Matt、Simon、Lilian、Boris 分别强化什么，以及如何共享同一自然成稿结构

## Prompt Pair cases

- [Task Context: Fable repo L3 alignment](prompt-pairs/01-task-context/001-fable-repo-l3-alignment.md)
- [Task Context: Harness three-layer audit](prompt-pairs/01-task-context/002-harness-three-layer-audit.md)
- [Task Context: Harness workflow compatibility cleanup](prompt-pairs/01-task-context/003-harness-workflow-compatibility-cleanup.md)
- [Task Context: Iteration Reason vs History — replay target selection gap](prompt-pairs/01-task-context/004-iteration-reason-vs-history.md)
- [Boundary: Wayfinder without forking](prompt-pairs/03-boundary/001-wayfinder-without-forking.md)
- [Immediate Task: Request normalization](prompt-pairs/04-immediate-task/001-request-normalization-code-read.md)
- [Success: Output contracts](prompt-pairs/05-success/001-output-contracts.md)
- [Review: Challenge before recommendation](prompt-pairs/06-review/001-challenge-before-recommendation.md)
- [Research: Conditional blindspot skill](prompt-pairs/09-research/001-conditional-blindspot-skill.md)
- [Wayfinder: Unknown routing adapter](prompt-pairs/10-wayfinder/001-unknown-routing-adapter.md)
- [Loop: FeatureTable bounded loop](prompt-pairs/11-loop/001-featuretable-bounded-loop.md)
- [Verification: Replay-observable slices](prompt-pairs/12-verification/001-replay-observable-slices.md)

## Compiled knowledge

- [Transferable principles](principles/transferable-principles.md)
- [Prompt Atlas Map](maps/prompt-atlas.md)
- [Gaps and collection priorities](summaries/gaps.md)
- [Delegation Readiness Roadmap](summaries/delegation-readiness-roadmap.md) — planned / not active；保留 Prompt Alignment 主轴，只定义后续引入 Gate
- [Patterns](patterns/README.md) — empty until repeated validation
- [Harness knowledge](harness/README.md) — stable operating contracts only
- [Case studies](case-studies/README.md) — end-to-end evidence chains

## Templates

- [Prompt Pair](templates/prompt-pair.md)
- [Knowledge note](templates/knowledge-note.md)
- [Source record](templates/source-record.md)