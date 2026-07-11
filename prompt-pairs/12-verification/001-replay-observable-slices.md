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

这次改动请按 replay 是否能够独立归因来拆分，而不是按文件数量或模块边界拆批。KFC 相关路径单独作为一个 slice；其余共享相同预期语义的改动可以合并推进。若两组改动失败后无法判断是哪一组改变了行为，就必须继续拆开。

每个 slice 开始前固定 baseline、输入集和 expected diff classification，明确它应该是 no-diff 还是允许出现可解释差异。实现后先用 build 结果排除编译或基础设施问题，再比较 replay evidence。

No-diff slice 只要出现行为差异就不得继续；expected-diff slice 必须逐类解释变化，并证明没有超出目标语义。每个 slice 最终依据 build 与 replay 证据给出 `PASS / RETRY / BLOCK`，不要把 replay 留到全部修改完成后再补跑。
