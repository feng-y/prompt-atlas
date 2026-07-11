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

### Goal

增强 Wayfinder 在本 repo 中发现和路由 unknown 的能力，同时保持它作为通用 discovery shell，而不是 fork 出一套专用工具。

### Current Context

现有 Matt Wayfinder / Grill 已可用于 discovery；repo 侧尚需确认是否已向它暴露任务入口、架构边界、unknown 升级路径与验证证据。

### Design Intent

将 repo-specific 知识和约束放在 repo harness 的 adapter 或 context route 中，让 Wayfinder 保持通用。

### Boundary

不要 fork 或重写 Wayfinder，不要让 Grill 承担 repo knowledge 或 verification，不要创造平行 workflow。

### Immediate Task

判断缺失的最小约束是什么，并区分应由 repo 提供的 adapter/context 与必须修改 Wayfinder 的真实缺口。

### Expected Output

先给最终 verdict：无需调整、只需附加约束，或必须修改 Wayfinder；再列出必要改动和明确不该做的改动。

### Success / Stop Condition

当 verdict 有对应 repo evidence 且能指出唯一归属层时完成。若缺口涉及 Wayfinder 核心语义而非 repo 适配，停止并请求人工决定是否 fork。
