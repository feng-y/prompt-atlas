# Wayfinder：增强控制面，但不 fork 工具

**标签**：Boundary / Wayfinder / Harness  
**证据状态**：历史对话可追溯。

**来源**：[Prompt Atlas bootstrap conversations](../../sources/src-2026-07-10-prompt-atlas-bootstrap.md)

## Current Prompt（摘录）

> wayfinder 需要调整么？wayfinder 本身就有 grill，怎么适配？我理解只是附加自己的约束把 unknown 路由带入？skill 大同小异，不需要自己构建，prompt 还是需要加强。

## Problem Analysis

已经包含关键判断，但问句连续叠加，模型容易逐题回答，忽略核心设计选择：是在 Wayfinder 内部修改，还是让 repo harness 提供外部约束。

## Minimal Rewrite

> 我们已经采用 Matt 的 Wayfinder / Grill，不打算 fork 或重写它。请判断 repo harness 还缺哪一层最小约束，才能让 Wayfinder 感知 unknown routing 与 verification loop；优先通过 repo context 或 guardrail 接入，而不是修改 Wayfinder 本身。先给最终判断，再说明必要改动与不该做的改动。

## Transferable Principle

表达“不要改工具”时，同时说明扩展点归谁所有。单纯禁止修改会让模型失去替代路径。

## Final Prompt

我们已经采用 Matt 的 Wayfinder 和 Grill，不希望 fork、重写或重新创建一套相似能力。当前要解决的是：Wayfinder 发现 unknown 后，能否自然使用 DaVinci repo 已有的知识入口、架构边界和验证能力，而不是继续依赖模型自行感知。

请把 Wayfinder 保持为通用的 discovery shell，检查 repo 是否已经向它稳定暴露任务入口、架构约束、unknown 的升级路径和可执行的验证证据。缺失部分优先由 repo-owned context、adapter 或 guardrail 承担，不要把 repo knowledge 和 verification 责任塞进 Wayfinder 核心流程。

Grill 只负责澄清会改变方案的 intent 与取舍，不承担代码事实发现或验证执行。

最后明确判断当前属于无需调整、只需增加 repo-local 约束，还是确实存在必须修改 Wayfinder 的缺口，并给出对应证据和最小改动范围。
