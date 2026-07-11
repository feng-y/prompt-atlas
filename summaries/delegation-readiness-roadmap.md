# Delegation Readiness Roadmap

> 状态：**planned / not active**。当前训练主轴仍是 Prompt Alignment；本页只保存后续扩展方向，不改变现有 Foundation、Prompt Pair 结构或学习顺序。

## 当前主轴：Prompt Alignment

Prompt Atlas 现阶段继续训练一件事：把模糊任务描述提升为清晰、自然、可验证的 Decision Context。

当前固定检查仍然是：

- Goal / Why：真正要解决的问题与预期变化；
- Current Context：影响判断的当前状态；
- Boundary：本轮范围、不可越过的约束与决策边界；
- Immediate Task：这一轮模型需要完成的具体动作；
- Success / Stop Condition：可观察证据、完成标准与停止位置。

这些维度继续作为内部检查模型，不机械变成 Final Prompt 的可见标题。

## 为什么记录下一阶段

来源 [5.6 Sol is underhyped for general work](../sources/src-2026-07-11-sol-general-work-and-delegation.md) 提出了一个超出表达质量的问题：模型理解任务之后，是否已经具备跨工具、跨系统、长时间完成真实工作的条件。

这说明需要区分两个问题：

1. **Prompt Alignment**：模型是否进入了正确的问题空间；
2. **Delegation Readiness**：任务是否已经可以安全、持续、可验证地交给 Agent 执行。

现阶段只训练第一个问题。第二个问题先进入路线图，不提前并入基础 Prompt 模板。

## 后续计划

### Stage 1 — Prompt Alignment（当前）

目标：稳定产出内容对齐、边界对齐、任务对齐的 Final Prompt。

继续积累：

- 真实 Current Prompt → Minimal Rewrite → Final Prompt；
- Prompt 是否减少澄清轮次、错误问题空间和边界漂移的证据；
- Decision Context 原则在软件工程与非软件场景中的迁移情况。

停止条件：基础结构能够被稳定使用，而不是只在单个案例中写得更完整。

### Stage 2 — Delegation Readiness 识别（后续引入）

目标：在不改变 Final Prompt 主体结构的前提下，判断一个任务当前缺的是表达，还是执行条件。

计划观察六个维度：

| 维度 | 核心问题 |
| --- | --- |
| Context access | Agent 能否访问真实且足够的工作上下文？ |
| Execution surface | 它需要操作哪些 repo、插件、网页或本地应用？ |
| Permission | 哪些动作可自主完成，哪些必须确认？ |
| State | 长任务中断、失败或跨会话后如何继续？ |
| Verification | Agent 如何提供可复核的完成证据？ |
| Escalation | 遇到什么情况必须停止并交还给人？ |

本阶段的产物优先是轻量检查表、案例标注或 readiness verdict，而不是把六个字段强塞进每个 Prompt。

### Stage 3 — Control Prompt / Harness handoff（远期）

目标：当任务已对齐且具备委托条件时，把 Prompt 交给实际执行环境。

需要通过真实案例再决定哪些信息属于：

- Prompt 自身；
- repo-owned context；
- tool / plugin contract；
- permission gate；
- workflow state；
- verification / replay / eval；
- human escalation。

只有反复出现、能降低未来委托成本的规则，才提升到 `harness/` 或 `patterns/`。

## 进入下一阶段的 Gate

在以下条件出现前，不把 Delegation Readiness 提升为当前训练主轴：

- Prompt Alignment 已有足够多真实 Prompt Pair，而非主要依靠概念说明；
- 至少出现 3 个“Prompt 已清楚但任务仍无法可靠执行”的真实案例；
- 能明确区分 Prompt 缺口与工具、权限、状态、验证缺口；
- 新检查不会让 Final Prompt 退化成冗长的 Agent 配置表。

## 当前约束

- 不修改 [Prompt Foundation Structure](../guides/prompt-foundation-structure.md)。
- 不新增可见的 Final Prompt 固定栏目。
- 不因为 Sol、Ultra 或 multi-agent 概念重构 Prompt Atlas。
- 不把未经真实任务验证的模型分工或 Harness 结论提升为 principle。
- 近期只在新案例中记录：问题来自 Prompt Alignment，还是来自 Delegation Readiness。

## 下一次可执行动作

当出现第一个“Prompt 已经对齐，但执行仍被上下文、权限、工具或验证阻塞”的真实任务时，建立一个 Case Study，记录：

`Aligned Prompt → missing execution condition → minimal environment fix → evidence → verdict`

在此之前，本页保持为计划，不生成新的训练模块。
