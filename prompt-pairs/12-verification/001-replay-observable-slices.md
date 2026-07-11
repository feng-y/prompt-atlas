# Replay：按可观察边界拆分，而不是按文件拆分

**标签**：Verification / Slice / Refactor  
**证据状态**：历史对话可追溯。

**来源**：[Prompt Atlas bootstrap conversations](../../sources/src-2026-07-10-prompt-atlas-bootstrap.md)

## Current Prompt（摘录）

> replay 验证点后面和 KFC 相关的分开的改，其他的可以一起改了，使用 replay 验证。

## Problem Analysis

已经包含正确的拆分直觉，但“使用 replay 验证”没有说明预期差异、判定方式和失败路由，模型仍可能把 replay 当作最后补跑的测试。

## Minimal Rewrite

> 按 replay 的可观察边界拆批，而不是按文件拆。KFC 相关路径单独成 slice；其余共享语义改动合并推进。每个 slice 开始前声明预期 replay diff（no-diff 或可解释 diff），结束时用 build + replay 证据判定 `PASS / RETRY / BLOCK`。

## Transferable Principle

Verification 不只是末尾测试，它应该反向决定任务如何切片。好的 slice 是失败后仍能归因的最小语义单元。

## Final Prompt

### Goal

按 replay 可独立归因的语义边界拆分改动，使验证不仅发现差异，还能判断差异来自哪一个 slice。

### Current Context

KFC 相关路径与其他共享语义改动存在不同的 replay 风险。现有意图是分批修改并使用 replay，但尚未明确 baseline、预期 diff 与失败路由。

### Design Intent

让 verification 反向决定切片大小：每个 slice 应是失败后仍可归因的最小语义单元。

### Boundary

不要按文件数量或目录机械拆分，不要将 replay 留到最后补跑，不要把 no-diff 与 expected-diff 混在同一判断中。

### Immediate Task

将 KFC 路径单独作为 slice；其余共享语义改动按可观察边界合并。为每个 slice 先声明 baseline、输入集与预期 replay diff。

### Expected Output

输出 slice 划分、每个 slice 的 no-diff 或 expected-diff 分类、build + replay verdict 规则，以及失败后的 RETRY / BLOCK 路由。

### Success / Stop Condition

当每个 slice 的差异都能独立解释时完成。no-diff slice 出现未解释变化或 expected-diff 超出目标语义时停止，不进入下一 slice。
