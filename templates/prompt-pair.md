# [案例标题]

**标签**：Task Context / Background / Boundary / Immediate Task / Success / Review / Architecture / Refactor / Research / Wayfinder / Loop / Verification  
**目标模型**：ChatGPT / Codex / Claude Code / Fable  
**证据状态**：原文 / 摘录 / 重建 / 已验证

## Current Prompt

> 粘贴实际准备发送或已经发送的 Prompt。保留原貌，不先润色。

## Problem Analysis

- 已经做得好的地方
- 最影响结果的一处问题
- 如果只改一处，改哪里最值

## Minimal Rewrite

> 尽量保持原表达，只补最关键的 Decision Context。

## Why It Is Better

说明改写减少了模型的哪一部分猜测或决策成本，而不是只说“更清晰、更专业”。

## Transferable Principle

一句可迁移原则。

## Outcome（执行后补）

- 实际发送版本：
- 模型结果：
- 返修轮次：
- 证据 / verdict：
- 下次只保留什么：

## Final Prompt

Final Prompt 必须是页面最后一节，也是唯一可直接发送给目标模型的版本。Phase 1 默认使用以下强结构：

### Goal
[真正想解决的问题、为什么现在处理、希望产生的变化]

### Current Context
[已有状态、缺口、当前阶段、判断必须知道的事实]

### Design Intent
[多个合理方案之间应偏向什么；没有额外取舍时可简短说明]

### Boundary
[不能改变什么、必须保留什么、优先复用什么、明确不做什么]

### Immediate Task
[这一轮唯一需要完成的问题或切片；哪些事情留到后续]

### Expected Output
[需要的判断、依据、方案、缺失信息或可执行产物]

### Success / Stop Condition
[必须回答的问题、必要证据、何时继续、何时停止并升级人工决策]

Phase 1 最少不得省略：Goal、Current Context、Boundary、Immediate Task、Success / Stop Condition。不得混入分析、比较说明或多个备选版本。