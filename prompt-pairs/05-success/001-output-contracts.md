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

保留现有阶段划分，不需要把流程继续拆得更细。当前真正的问题是每一阶段虽然能产生内容，但产物放在哪里、由谁消费、依据什么进入下一阶段还不够清楚，导致后续 Agent 需要重新理解上游结论。

请把每个阶段输出设计成可消费的 packet，明确它应包含的 deliverable、支撑结论的 evidence、当前 verdict、下一位 consumer 和 route reason。只有下一阶段不需要重新解释核心决策、且 verifier 能独立检查证据时，才认为该阶段完成。

重点保证 plan、implementation 和 replay verdict 能连续衔接。只服务当前轮思考的内容不要固化为长期文档，避免为了完整而增加无消费者的产物。

最终给出各阶段的最小输出合同、建议落点、消费关系和进入下一阶段的可观察条件。
