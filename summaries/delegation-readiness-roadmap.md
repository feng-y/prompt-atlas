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

当前首先追求的是**人类可写的高质量改写**：Final Prompt 应当是人能够理解、学习并逐步自行写出的表达，而不是提前生成一份依赖大量隐藏假设的完整 Agent 控制合同。

## 为什么记录下一阶段

来源 [5.6 Sol is underhyped for general work](../sources/src-2026-07-11-sol-general-work-and-delegation.md) 提出了一个超出表达质量的问题：模型理解任务之后，是否已经具备跨工具、跨系统、长时间完成真实工作的条件。

来源 [Human rewrite before repo compilation](../sources/src-2026-07-12-human-rewrite-before-repo-compilation.md) 又补充了当前边界：repo-aware 编译只有在 Agent 实际进入 repo、读取当前事实后才可能稳定地产生价值。若在外部对话中提前补写 repo 入口、架构判断和证据路线，结构越完整，错误理解反而可能被放大。

这说明需要区分三个问题：

1. **Prompt Alignment**：人是否把目标、当前状态、边界和本轮任务表达清楚；
2. **Repo Grounding**：执行 Agent 是否已经从真实 repo 中确认入口、已有能力与约束；
3. **Delegation Readiness**：任务是否已经可以安全、持续、可验证地交给 Agent 执行。

现阶段只训练第一个问题。后两个问题先进入路线图，不提前并入基础 Prompt 模板。

## 后续计划

### Stage 1 — Human-writable Prompt Alignment（当前）

目标：稳定产出内容对齐、边界对齐、任务对齐，并且人可以自然理解和模仿的 Final Prompt。

继续积累：

- 真实 Current Prompt → Minimal Rewrite → Final Prompt；
- Prompt 是否减少澄清轮次、错误问题空间和边界漂移的证据；
- Decision Context 原则在软件工程与非软件场景中的迁移情况；
- 改写是否仍保留人的原始判断，而不是替人补出未经确认的专业体系。

停止条件：基础结构能够被稳定使用，而不是只在单个案例中写得更完整。

### Stage 2 — Repo Grounding（后续引入）

目标：当任务真正进入 repo 后，由执行 Agent读取当前入口、代码、文档、Harness 与验证能力，确认 Prompt 中哪些判断成立、哪些需要修正。

本阶段不由外部改写者预先编译具体 repo 事实。产物优先是：

- 已确认的 repo anchors；
- 已有能力与真实缺口；
- 会改变任务边界的 unknown；
- 可执行的 evidence route；
- 对原 Prompt 的最小 grounded adjustment。

### Stage 3 — Delegation Readiness 识别（后续引入）

目标：在 Prompt 已对齐、repo 已 grounding 后，判断任务当前缺的是表达，还是执行条件。

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

### Stage 4 — Control Prompt / Harness handoff（远期）

目标：当任务已对齐、repo 事实已确认且具备委托条件时，再形成更完整的执行控制输入。

需要通过真实案例决定哪些信息属于：

- Prompt 自身；
- repo-owned context；
- tool / plugin contract；
- permission gate；
- workflow state；
- verification / replay / eval；
- human escalation。

只有反复出现、能降低未来委托成本的规则，才提升到 `harness/` 或 `patterns/`。

## 进入下一阶段的 Gate

在以下条件出现前，不把 repo 编译或 Delegation Readiness 提升为当前训练主轴：

- Prompt Alignment 已有足够多真实 Prompt Pair，而非主要依靠概念说明；
- 人类可写的 Minimal Rewrite 已经能够稳定保留目标、边界和当前困惑；
- 至少出现 3 个“Prompt 已清楚，但进入 repo 后必须调整”的真实案例；
- 能明确区分人的表达缺口、外部误解与 repo 内事实缺口；
- 新检查不会让 Final Prompt 退化成冗长的 Agent 配置表。

## 当前约束

- 不修改 [Prompt Foundation Structure](../guides/prompt-foundation-structure.md)。
- 不新增可见的 Final Prompt 固定栏目。
- 不要求人提前提供完整 repo grounding。
- 不在未读取真实 repo 时补写具体架构、文件入口或验证机制。
- 不因为 Sol、Ultra 或 multi-agent 概念重构 Prompt Atlas。
- 不把未经真实任务验证的模型分工或 Harness 结论提升为 principle。

## 下一次可执行动作

当出现第一个“人类改写已经清楚，但执行 Agent 进入 repo 后发现外部理解不准确”的真实任务时，建立一个 Case Study，记录：

`Human-writable Prompt → repo grounding correction → minimal prompt adjustment → evidence → verdict`

在此之前，本页保持为计划，不生成新的 repo 编译训练模块。
