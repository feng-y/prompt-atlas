# Prompt Foundation Structure

> Phase 1 的目标不是写出“高级 Prompt”，而是让模型先进入正确的问题空间，至少做到内容对齐、边界对齐与任务对齐。

**来源**：[Prompt foundation structure source](../sources/src-2026-07-10-prompt-foundation-structure.md)

## Phase 1 default

默认训练且必须清楚的五项：

1. **Goal** — 真正想解决什么问题，为什么现在值得处理。
2. **Current Context** — 当前已有什么、缺什么、处于哪个阶段，以及模型判断必须知道的事实。
3. **Boundary** — 哪些方向不能走，什么必须保留或优先复用。
4. **Immediate Task** — 本轮只回答或完成什么，明确哪些留到后续。
5. **Done** — 必须产出什么、什么证据存在、何时停止或升级人工决策。

如果这五项清楚，Prompt 的基础结构即为及格。若只能改一个地方：**不要从 Task 开始，先写真正的问题和当前状态。**

## Full structure

| Section | Purpose | Add when |
| --- | --- | --- |
| Goal | 说明真正问题、价值和希望产生的变化 | 始终 |
| Current Context | 给模型作判断所需的当前事实 | 始终 |
| Design Intent | 多个合理方案之间的偏好 | 取舍会影响方案时 |
| Boundary | 缩小错误搜索空间 | 始终 |
| Immediate Task | 限定本轮唯一推进目标 | 始终 |
| Expected Output | 让结果能被后续消费 | 输出形态影响使用时 |
| Success / Stop Condition | 定义完成、继续和人工升级 | 始终 |

## Copy-ready skeleton

```markdown
### Goal
[真正想解决的问题、为什么现在处理、希望产生的变化]

### Current Context
[已有状态、缺口、当前阶段、判断必须知道的事实]

### Design Intent
[多个合理方案之间应偏向什么；没有额外取舍时可省略]

### Boundary
[不能改变什么、必须保留什么、优先复用什么、明确不做什么]

### Immediate Task
[这一轮唯一需要完成的问题或切片；哪些事情留到后续]

### Expected Output
[需要的判断、依据、方案、缺失信息或可执行产物；不必规定思考过程]

### Success / Stop Condition
[必须回答的问题、必要证据、何时继续、何时停止并升级人工决策]
```

## Basic self-check

写完后只检查：

1. 模型是否知道真正想解决什么？
2. 是否知道当前已有与缺少什么？
3. 是否知道哪些方向不能走？
4. 是否知道本轮只需要完成什么？
5. 是否知道什么时候可以停止？

任何 Phase 1 Prompt Pair 的 `Final Prompt` 必须使用此骨架。Design Intent 与 Expected Output 可以简短或在不影响判断时省略；其余五项不可省略。