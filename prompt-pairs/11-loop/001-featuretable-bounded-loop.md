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

FeatureTable context table 与 global table 的迁移方案已经完成 readiness 判断，核心决策也已经锁定。请把现有 plan 作为 source of truth，不重新规划，也不要扩大到邻接重构。

按 A（config merge）→ B（`SessionData` registration SOT）→ C（access-layer getter）的顺序推进，但当前只启动 Slice A。每个 slice 开始前先确认预期语义和 replay diff，然后循环执行 `inspect → patch → build → replay → evaluate`。只有 build 与 replay 证据都支持 PASS 时，才进入下一 slice；证据不足只能 RETRY 或 BLOCK，不能凭代码审查宣布完成。

Unknown 默认保持在当前 slice 内解决。只有当它会改变已经锁定的决策、`SessionData::clear()` 生命周期顺序、remote/global ownership 或既定 verification strategy 时，才停止并升级给我。

不要提前删除 `remote_dict.conf`，也不要顺手修改不属于当前 slice 的代码。每轮报告实际 patch、build/replay 结果和当前 verdict；全部 slice 通过后再给出最终完成判断。
