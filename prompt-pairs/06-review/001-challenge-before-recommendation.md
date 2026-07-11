# 方案评估：先建立最强反方，再给结论

**标签**：Review / Decision Context  
**证据状态**：由多次“评估下我的方案 / 质疑这个”对话归纳。

**来源**：[Prompt Atlas bootstrap conversations](../../sources/src-2026-07-10-prompt-atlas-bootstrap.md)

## Current Prompt

> 评估下我的方案。质疑这个。

## Problem Analysis

简洁，但没有说明评估对象、已锁定判断和真正担心的失败模式。模型可能给平均化的优缺点，而不是挑战核心假设。

## Minimal Rewrite

> 请先构造对这个方案最强的反方论证，重点检查它是否把 prompt 能力误当成 harness 能力、是否重复 Wayfinder 已有机制，以及 verification 是否真正闭环。然后给出你的最终判断：保留、最小调整或推翻。不要为了平衡而罗列一般性优缺点。

## Transferable Principle

“质疑”最好绑定到关键假设、证伪证据和翻案条件，而不是要求模型扮演抽象反方。

## Final Prompt

下面是我的当前方案和判断。请不要给一份平均化的优缺点清单，也不要为了显得平衡而保留所有可能性。

先区分其中哪些结论已有 repo evidence 支撑，哪些仍是我的假设。找出一个一旦不成立就会改变整个方案的关键前提，围绕它构造最强的反方论证，并说明需要什么证据才能证伪或证实。

重点检查这个方案是否把 Prompt 能力误当成 Harness 能力、是否重复 Wayfinder 已有机制，以及 verification 是否真正形成闭环。

最后明确给出保留、最小调整或推翻的判断，并说明当前最小的可逆验证动作是什么、出现什么结果时应该翻案。
