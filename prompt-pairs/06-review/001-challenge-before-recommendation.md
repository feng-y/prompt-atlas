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

### Goal

检验当前方案是否建立在错误或未证实的关键假设上，并得到可下注的判断，而不是获得平均化的优缺点列表。

### Current Context

当前已有方案与部分 repo evidence，但尚未明确哪些判断只是推测。特别需要检查 prompt 能力与 harness 能力是否混淆、Wayfinder 是否被重复建设、verification 是否闭环。

### Design Intent

先构造最强反方，再以可证伪证据决定保留、最小调整或推翻。

### Boundary

不要为了平衡罗列一般性优缺点，不要把抽象反对意见当结论，不要在缺少证据时假装方案已被证实。

### Immediate Task

区分事实与假设，找出一个一旦不成立就会改变方案的关键前提，并围绕它给出最强反例。

### Expected Output

输出关键假设、支持与反驳证据、最小可逆验证动作、最终 verdict，以及会让结论翻案的条件。

### Success / Stop Condition

当能够明确保留、最小调整或推翻，并说明依据时完成。若关键前提无法通过现有证据或小实验判断，停止并请求人工选择风险取舍。
