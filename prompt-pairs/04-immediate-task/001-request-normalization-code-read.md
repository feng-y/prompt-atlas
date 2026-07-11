# Request 归一化：先做可判定的 code-read

**标签**：Immediate Task / Refactor / Architecture  
**证据状态**：历史需求可追溯；字段清单需由 repo 证据生成。

**来源**：[Prompt Atlas bootstrap conversations](../../sources/src-2026-07-10-prompt-atlas-bootstrap.md)

## Current Prompt（摘录）

> 这些 feature_fetch_* 代码使用了哪些 request 字段？是否可以在 SessionData 初始化，也就是 reset_ 这部分逻辑时设置这些字段，然后在使用的地方对接口/method 的 request 解耦？已经对 request 做了归一化……

## Problem Analysis

原 Prompt 同时要求查字段、判断所有权、设计迁移和隐含实现。缺少本轮停点，模型可能在证据不足时直接建议改代码。

## Minimal Rewrite

> 请检查列出的 `feature_fetch_*` modules 实际读取的 request fields，并沿 `SessionData::reset_*` 初始化链路追踪这些字段能否成为 session-owned canonical data。当前只做 code-read 和迁移判断，不改代码。输出 `field → source → init point → consumer → migration verdict`，并标出仍需保留 raw request 的语义差异。

## Transferable Principle

重构类 Prompt 先把“改什么”改写成“按什么证据判断能不能改”，就能显著降低机械替换和过早实现。

## Final Prompt

DaVinci 已经对 request 做了部分归一化。这次工作的目标不是把所有旧 request 引用机械替换成 `unify_request`，而是判断哪些字段已经具备稳定的 session ownership，从而让下游 module 与具体接口 request 解耦。

请检查列出的 `feature_fetch_*` modules 实际读取了哪些 request fields，并沿 `SessionData::reset_*` 初始化链路追踪每个字段的原始来源、归一化位置、生命周期和所有 consumer。特别确认它们是否受 tag、streaming 或 item 语义差异影响。

本轮只做 code-read 和迁移判断，不修改代码。只有初始化时机与行为语义都等价时，才判定字段可以迁移到 session-owned canonical data；其余标记为 residual dependency，并说明它是真实业务差异还是尚未收敛的历史耦合。

最终按 `field → source → init point → consumer → migration verdict` 给出证据，并列出仍需保留 raw request 的位置及原因。
