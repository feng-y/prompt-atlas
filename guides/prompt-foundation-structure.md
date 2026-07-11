# Prompt Foundation Structure

> Phase 1 的目标不是写出“高级 Prompt”，而是让模型进入正确的问题空间，至少做到内容对齐、边界对齐与任务对齐。

**来源**：
- [Prompt foundation structure source](../sources/src-2026-07-10-prompt-foundation-structure.md)
- [Embedded Final Prompt structure decision](../sources/src-2026-07-11-embedded-final-prompt-structure.md)

## Phase 1 foundation

写 Prompt 时，先检查五类信息是否已经清楚：

1. **Goal / Why** — 真正想解决什么问题，为什么现在值得处理。
2. **Decision Context** — 已经确认了什么、当前卡在哪里、哪些事实会改变判断。
3. **Control Boundary** — 哪些方向不能走，什么必须保留或优先复用。
4. **Immediate Task** — 本轮只回答或完成什么，哪些留到后续。
5. **Observable Evidence** — 需要什么产物或证据，何时停止或升级人工决策。

如果这五项清楚，Prompt 的基础内容通常已经及格。若只能改一个地方：**不要从任务列表开始，先说明真正的问题和当前判断。**

## Foundation is a review model, not a visible template

这五类信息用于组织思考和检查遗漏，不要求 Final Prompt 显式写成五个或七个栏目。

默认不要在成稿中机械使用：

```text
### Goal
### Current Context
### Boundary
### Immediate Task
### Success / Stop Condition
```

这种结构容易让 Prompt 变成表单填空，也会让模型平均对待每个栏目。最终可发送版本应根据任务关系自然组织 Markdown：通常先说明目标与当前问题，再写必要边界和本轮任务，最后交代可观察的完成证据。

只有当任务本身需要正式合同、多人交接或逐项返回时，才因为实际消费需要使用标题或列表；不能仅因为 Prompt Atlas 用这些维度做分析，就把标签暴露到成稿里。

## Natural Final Prompt example

```markdown
DaVinci 当前不是缺少更多文档，而是需要确认现有 repo harness 是否真的能够支撑 L3：让 Fable 在明确需求下自助完成任务，并只进行有限、可控的学习改进。

请从 `CLAUDE.md` 开始，沿它指向的架构边界、workflow 路由和验证入口理解当前机制，判断这些入口与 repo reality 是否一致。把这次工作视为 repo harness alignment，而不是文档整理或知识体系重建。

已有结构能够承载的就继续沿用，只处理会真实影响任务进入、unknown routing 或 verification feedback 的不一致。不要预设具体改造方案，也允许你质疑我对 L3 的理解。

本轮完成时给出当前 L3 支撑能力的判断、对应的 repo 证据、最值得调整的一处，以及为什么现阶段不需要更大的改造。
```

这段成稿仍然包含 Goal、Decision Context、Boundary、Immediate Task 与 Evidence，但这些信息由语义关系承载，而不是由教学标题承载。

## Drafting flow

1. 先用 foundation 五项检查当前 Prompt 缺少什么。
2. 只补会改变模型判断的内容，不为凑齐栏目增加废话。
3. 将信息重写为自然、连续、可直接发送的 Markdown。
4. 必要时使用列表，但列表服务于任务执行或交付，不服务于展示模板。
5. 最后重新检查五项是否在语义上存在，而不是检查标题是否存在。

## Basic self-check

写完后只检查：

1. 模型是否知道真正想解决什么？
2. 是否知道当前已经确认什么、真正的困惑是什么？
3. 是否知道哪些方向不能走或必须保留？
4. 是否知道本轮只需要完成什么？
5. 是否知道用什么证据判断完成，什么时候应该停止？
6. Final Prompt 是否自然、完整、可直接发送，而不是分析字段的拼接？

任何 Prompt Pair 的 `Final Prompt` 都必须位于页面最后一节，并且是唯一可直接发送的版本。Foundation 五项必须在内容上足够清楚，但默认不得要求以同名标题显式出现。
