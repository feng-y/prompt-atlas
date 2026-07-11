# FeatureTable：从迁移方案进入 bounded goal loop

**标签**：Loop / Migration / Verification  
**证据状态**：方案与主要约束可追溯；完整最终 prompt 待回填。

**来源**：[Prompt Atlas bootstrap conversations](../../sources/src-2026-07-10-prompt-atlas-bootstrap.md)

## Current Prompt（摘录）

> FeatureTable context table 与 global table 统一的方案已经写好，状态是 readiness 已判定、决策已锁定、尚未开工。给我一个 loop prompt 推进方案。

## Problem Analysis

如果只说“loop 推进”，模型可能重新规划、一次性跨过 A/B/C、把未知扩散到全局，或把“持续工作”误解为无停止条件的重复。

## Minimal Rewrite

> 基于现有迁移方案，不重做 plan。把 A/B/C 三个 slice 转成可连续推进、可在 unknown 处停下、可用 replay 判定的 goal loop。先只启动 Slice A；每轮执行 `inspect → patch → build → replay → evaluate`，PASS 才进入下一 slice。只有会改变 locked decision 的 unknown 才升级给我。

## Transferable Principle

Goal loop 至少需要四个合同：当前 slice、单轮动作、可观察 stop condition、改变决策时的 escalation rule。

## Final Prompt

### Goal

在不重做既有迁移 plan 的前提下，让 FeatureTable 统一迁移按可恢复、可停止、可由 replay 判定的 bounded goal loop 推进。

### Current Context

readiness 已判定、关键决策已锁定；迁移分为 A：config merge，B：SessionData registration SOT，C：access-layer getter。当前尚未开工，风险集中在生命周期、ownership 与 replay 语义。

### Design Intent

按已锁定 plan 和最小 slice 推进；用 build 与 replay 作为真实 gate，让 unknown 保持 slice-local。

### Boundary

不要重做 plan，不要跨 A/B/C 提前推进，不要提前删除 remote_dict.conf，不要顺手重构邻接代码；不得改变 SessionData clear 生命周期顺序或 remote/global ownership。

### Immediate Task

仅启动 Slice A。每轮执行 inspect → patch → build → replay → evaluate，并在开始前声明预期 replay diff。

### Expected Output

输出 Slice A 的当前证据、最小 patch、build 与 replay verdict、下一轮路由，以及会改变 locked decision 的 unknown。

### Success / Stop Condition

只有 Slice A 取得 PASS 才能进入 Slice B；证据不足为 RETRY 或 BLOCK。若发现改变 locked decision、生命周期顺序或 ownership 的问题，立即停止并升级人工判断。
