# 输出合同：让阶段结果能被后续消费

**标签**：Success / Planning / Verification  
**证据状态**：历史对话摘录，可追溯。

## Current Prompt（摘录）

> Prompt 大体上还好，一个问题是每一个 prompt 的输出没有约束，放在哪里，后面的怎么接。

## Problem Analysis

问题已准确指出“输出不能只是一段回答”，但还没有把它转成模型可以执行的产物合同。模型因此容易在每个阶段都产生看似完整、但无法被下一阶段引用或验证的 Markdown。

## Minimal Rewrite

> 保留现有阶段划分，但为每一阶段补一个最小输出合同：产物是什么、放在哪里、下一阶段如何消费、什么证据表示可以进入下一阶段。不要把每一步拆碎；重点保证 plan、implementation 与 replay verdict 能连续衔接。

## Expert Lens

> 请把流程中的每个阶段输出视为一个可消费 packet，而不是一次性回复。对每个 packet 明确：`deliverable`、`evidence`、`verdict`、`next consumer` 与 `route reason`。只有当下一阶段无需重新解释上游结论、且 verifier 能独立检查证据时，才算完成。若某个输出只服务当前轮思考，不要固化为长期文档。

## Transferable Principle

成功条件不仅是“本轮说清楚”，还包括“下一阶段无需重新猜测就能消费这个结果”。
