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

### Goal

判断哪些 request 信息已经具备稳定的 session ownership，从而能安全地从原始 request 解耦，而不是机械替换所有 request 引用。

### Current Context

request 已完成归一化；多个 feature_fetch 模块仍读取 request 字段。需要沿 SessionData 初始化与消费链路确认字段来源、生命周期和语义差异。本轮只做 code-read 和迁移判断。

### Design Intent

优先建立字段级语义等价与 ownership 证据；只在初始化时机和语义都等价时收敛到 session-owned canonical data。

### Boundary

不要改代码，不要把 raw request 的真实业务差异误判为历史耦合，不要仅根据同名字段判断可替换。

### Immediate Task

逐字段追踪 feature_fetch 模块读取的 request fields：来源、归一化点、SessionData 初始化点、consumer 与残留语义。

### Expected Output

输出 field → source → init point → consumer → migration verdict；对不能迁移的字段说明它是业务差异还是尚未收敛的耦合。

### Success / Stop Condition

当每个被检查字段都有可审计 verdict 时完成。若字段生命周期或 tag / streaming / item 语义无法由代码证据确定，停止并列为需补充的 unknown。
