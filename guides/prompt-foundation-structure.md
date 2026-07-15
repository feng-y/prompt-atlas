# Prompt Foundation Structure

> Phase 1 的目标不是写出“高级 Prompt”，而是让模型进入正确的问题空间，并拿到足够清楚的任务合同：知道要得到什么、依据什么判断、哪些不能越过、何时算完成。

**来源**：
- [Prompt foundation structure source](../sources/src-2026-07-10-prompt-foundation-structure.md)
- [Embedded Final Prompt structure decision](../sources/src-2026-07-11-embedded-final-prompt-structure.md)
- [OpenAI GPT-5.6 Sol prompt guidance](../sources/src-2026-07-16-openai-gpt-5-6-sol-prompt-guidance.md)

## Phase 1 foundation

写 Prompt 时，先检查七类信息是否清楚。它们不是必须全部展开的栏目，而是 review 维度：

1. **Goal / Outcome** — 用户最终需要什么变化或结果，而不是模型需要执行哪些步骤。
2. **Decision Context** — 已确认什么、当前卡在哪里、哪些事实会改变判断。
3. **Available Evidence** — 当前可以依赖哪些 repo、文档、数据、日志、结果或来源；不要把证据清单写成固定读取顺序。
4. **Constraints / Approval Boundary** — 哪些是真正 invariant，哪些动作需要批准，当前工作停留在研究、设计、实现还是 review。
5. **Immediate Task** — 本轮只回答或完成什么，哪些留到后续。
6. **Success Criteria** — 哪些产物、事实、验证或状态必须成立，才能认为任务完成。
7. **Stop Rules** — 何时继续检索、重试或验证；何时停止、收窄、报告 blocker 或请求最小缺失信息。

如果只能改一个地方：**不要从任务列表开始，先说明想得到的结果和当前判断。** 如果 Prompt 已经工作，优先删除重复指令和无效过程控制，而不是一次性整体重写。

## Contract, not execution script

Prompt Atlas 将 Prompt 视为 Task Contract，不是 execution script。

Prompt 应固定：

- 用户可见结果；
- 会改变判断的上下文与证据；
- 安全、业务、权限和范围约束；
- 必要的输出与验证合同；
- 成功和停止条件。

Prompt 通常不应固定：

- 模型已经能够可靠选择的思考步骤；
- 无条件的读取顺序、工具顺序和循环次数；
- 重复的“先分析、再反思、再 review”；
- 不会改变结果的示例、风格要求和绝对规则。

`ALWAYS`、`NEVER`、`must`、`only` 只用于真正不可违反的 invariant。对于是否搜索、是否继续读取、是否重试或使用工具，优先写成由证据缺口驱动的 decision rule。

## Foundation is a review model, not a visible template

这些维度用于组织思考和检查遗漏，不要求 Final Prompt 显式写成七个栏目。

默认不要机械输出：

```text
### Goal
### Current Context
### Available Evidence
### Constraints
### Immediate Task
### Success Criteria
### Stop Rules
```

这种结构容易让 Prompt 变成表单填空，也会让模型平均对待每个栏目。最终可发送版本应根据任务关系自然组织 Markdown：通常先说明目标与当前问题，再嵌入会改变判断的证据、边界和本轮任务，最后交代完成标准与停止规则。

只有当任务本身需要正式合同、多人交接、结构化返回或 Harness 消费时，才因实际消费需要使用标题或列表。

## Natural Final Prompt example

```markdown
DaVinci 当前不是缺少更多文档，而是需要确认现有 repo harness 是否真的能够支撑 L3：让 Fable 在明确需求下自助完成任务，并只进行有限、可控的学习改进。

请从当前 repo 已有入口和真实实现出发，判断 CLAUDE.md、架构边界、workflow 路由与验证入口是否能把一个明确需求稳定带到可验证结果。现有代码、文档和 replay 结果都是证据，但不要把固定文件顺序当作任务本身。

把这次工作限制在 repo harness alignment。可以读取、比较和提出最小改动；不要直接扩展为知识体系重建，也不要越过设计进入大范围实现。只有真实影响任务进入、unknown routing 或 verification feedback 的不一致值得处理。

完成时给出当前 L3 支撑能力的判断、关键 repo 证据、最值得调整的一处和相应验证方式。继续调查只应由关键证据缺口驱动；当新增读取不再可能实质改变结论时停止，并明确剩余未知。
```

## Drafting flow

1. 先用七项 review 当前 Prompt 缺少什么。
2. 先删重复规则、无效示例、无关工具和不会改变行为的过程说明。
3. 只补会改变模型判断或完成质量的最小合同信息。
4. 将信息重写为自然、连续、可直接发送的 Markdown。
5. 最后检查模型是否拥有合理自治，同时不会越过当前工作层和审批边界。
6. 对工作 Prompt 的迁移一次只改一组规则，并用同一批代表性任务复测。

## Basic self-check

写完后检查：

1. 模型是否知道用户真正需要的结果，而不是只有动作列表？
2. 是否知道当前判断和真正的困惑？
3. 是否知道可以依赖哪些证据，而没有被迫执行无意义的固定流程？
4. 是否清楚真实约束、权限边界和当前工作层？
5. 是否知道本轮只需要完成什么？
6. 是否知道什么事实、产物和验证构成成功？
7. 是否知道何时继续、何时停止、何时报告 blocker？
8. 是否存在重复、矛盾或不必要的绝对规则？
9. Final Prompt 是否自然、完整、可直接发送，而不是分析字段的拼接？

任何 Prompt Pair 的 `Final Prompt` 都必须位于页面最后一节，并且是唯一可直接发送的版本。Foundation 必须在语义上足够清楚，但默认不得要求以同名标题显式出现。
