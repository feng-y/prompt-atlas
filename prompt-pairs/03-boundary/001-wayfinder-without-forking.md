# Wayfinder：增强控制面，但不 fork 工具

**标签**：Boundary / Wayfinder / Harness  
**证据状态**：历史对话可追溯。

## Current Prompt（摘录）

> wayfinder 需要调整么？wayfinder 本身就有 grill，怎么适配？我理解只是附加自己的约束把 unknown 路由带入？skill 大同小异，不需要自己构建，prompt 还是需要加强。

## Problem Analysis

已经包含关键判断，但问句连续叠加，模型容易逐题回答，忽略核心设计选择：是在 Wayfinder 内部修改，还是让 repo harness 提供外部约束。

## Minimal Rewrite

> 我们已经采用 Matt 的 Wayfinder / Grill，不打算 fork 或重写它。请判断 repo harness 还缺哪一层最小约束，才能让 Wayfinder 感知 unknown routing 与 verification loop；优先通过 repo context 或 guardrail 接入，而不是修改 Wayfinder 本身。先给最终判断，再说明必要改动与不该做的改动。

## Expert Lens

> 把 Wayfinder 保持为通用的 discovery shell。请检查当前 repo 是否已经向它暴露了四类信息：任务入口、架构边界、unknown 的升级路径、可执行的验证证据。若缺失，优先补 repo-owned adapter/context，而不是改变 Wayfinder 的核心流程。Grill 只负责澄清 intent；不要让它承担 repo knowledge 或 verification。最后判断：无需调整、只需附加约束，还是存在必须修改 Wayfinder 的真实缺口。

## Transferable Principle

表达“不要改工具”时，同时说明扩展点归谁所有。单纯禁止修改会让模型失去替代路径。
