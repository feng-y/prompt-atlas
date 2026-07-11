# 输出合同：让阶段结果能被后续消费

**标签**：Success / Planning / Verification  
**证据状态**：历史对话摘录，可追溯。

**来源**：[Prompt Atlas bootstrap conversations](../../sources/src-2026-07-10-prompt-atlas-bootstrap.md)

## Current Prompt（摘录）

> Prompt 大体上还好，一个问题是每一个 prompt 的输出没有约束，放在哪里，后面的怎么接。

## Problem Analysis

问题已准确指出“输出不能只是一段回答”，但还没有把它转成模型可以执行的产物合同。模型因此容易在每个阶段都产生看似完整、但无法被下一阶段引用或验证的 Markdown。

## Minimal Rewrite

> 保留现有阶段划分，但为每一阶段补一个最小输出合同：产物是什么、放在哪里、下一阶段如何消费、什么证据表示可以进入下一阶段。不要把每一步拆碎；重点保证 plan、implementation 与 replay verdict 能连续衔接。

## Transferable Principle

成功条件不仅是“本轮说清楚”，还包括“下一阶段无需重新猜测就能消费这个结果”。

## Final Prompt

### Goal

让流程的阶段输出成为下一阶段可直接消费、可独立验证的 packet，而不是只能服务当前轮思考的一段回复。

### Current Context

现有阶段划分已经存在，但各阶段产物、落点、下游消费者和进入下一阶段的证据不够明确，导致后续需要重新解释上游结论。

### Design Intent

保持阶段数量与现有 workflow 不变，只补最小输出合同，使 plan、implementation 与 replay verdict 连续衔接。

### Boundary

不要把每一步拆成细碎表单，不要把只服务当前思考的内容固化为长期文档，不要为了结构而增加新阶段。

### Immediate Task

为当前阶段定义最小 packet：deliverable、evidence、verdict、next consumer 与 route reason。

### Expected Output

给出各阶段产物的落点、下游读取方式、进入下一阶段的必要证据，以及无需固化的临时内容。

### Success / Stop Condition

当下一阶段无需重新猜测上游结论且 verifier 能独立检查证据时完成。若某阶段无法定义独立 consumer 或 evidence，停止并指出该阶段边界需要人工重定。
