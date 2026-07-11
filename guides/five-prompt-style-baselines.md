# Five Prompt Style Baselines

> 五类方法共享同一个 Prompt Foundation；它们训练的是不同的控制能力，而不是五套外观不同的模板。

**来源**：[Five Prompt style baselines](../sources/src-2026-07-11-five-prompt-style-baselines.md)

## Shared foundation

所有 Final Prompt 都先用下面五类信息检查完整性：

`Goal / Why → Decision Context → Control Boundary → Immediate Task → Observable Evidence`

这些维度只用于组织思考和 review。最终成稿应是自然、连续、可直接发送的 Markdown，不应机械写成 `Goal`、`Context`、`Boundary`、`Evidence` 或 `Loop` 等教学栏目。

五类方法之间的差异是：**分别强化哪一部分信息，以及用什么机制控制模型。**

| 学习基线 | 主要强化 | 适用阶段 |
| --- | --- | --- |
| Anthropic / Alex Albert | Why、Decision Context、Boundary、Immediate Task | 基础表达与单轮任务定义 |
| Matt Pocock | Destination、Fog、Frontier、Grill、Spec 边界 | 模糊任务与多轮 discovery |
| Simon Willison | Fact、Evidence、Inference、Hypothesis、Experiment | 研究、排障与事实核验 |
| Lilian Weng | Failure layer、Harness hypothesis、probe、retain / rollback | 重复失败与系统改进 |
| Boris Cherny | Goal、current state、feedback loop、stop / escalation | 任务清晰且验证闭环稳定后 |

## 1. Anthropic / Alex Albert：从离散需求到 Decision Context

### 训练重点

- 先说明为什么处理这件事，而不是直接罗列任务。
- 只提供会改变模型判断的当前背景。
- 把边界作为任务定义的一部分，而不是结尾附注。
- 一轮只保留一个 Immediate Task。
- 用可观察产物或证据定义完成。

### 不要学成什么

不要把这些维度写成固定五段式，也不要为强模型预写完整思考流程。

### Natural Final Prompt

```markdown
当前需要解决的不是简单修改文档，而是让 repo 入口能够稳定地把 Fable 带入正确的架构和验证上下文。

现有 `CLAUDE.md`、`ARCHITECTURE.md` 和 workflow 已经提供了部分入口，但还不清楚它们是否对任务路由、unknown 处理和 verification 形成一致指引。

请检查这些入口之间的实际关系，找出当前最影响任务自助推进的一处不一致。本轮只做判断和最小对齐，不重建知识体系，也不进入业务代码修改。

完成时给出判断、repo 证据、建议调整点，以及为什么不需要更大的改造。
```

## 2. Matt Pocock：用少量强概念控制多轮行为

### 训练重点

- 用 Destination 表达长期希望抵达的状态。
- 用 Fog 保留还不能准确提问的未知区域。
- 用 Frontier 限定当前真正可推进的决策。
- 能从 repo 查明的事实由 Agent 自行查明；真正的取舍交给人。
- Discovery、Spec、Implementation 与 Review against Spec 保持边界。

### 不要学成什么

不要把 `Destination / Fog / Frontier` 变成固定栏目，也不要把模糊任务过早拆成实现 Ticket。

### Natural Final Prompt

```markdown
这项工作当前还不能稳定进入 SPEC，因为目标方向大致清楚，但仍有几个会改变方案的未知区域。

先明确最终希望抵达的状态，再区分已经能够准确讨论的决策和仍处于 fog 中的问题。事实能够从 repo 中查明的就自行查明，只有真正涉及取舍的部分再交给我决定。

本轮只建立共享地图和当前 frontier，不开始实现，也不要把所有未知强行拆成任务。

当当前可推进的决策、仍保留的 fog 和下一步唯一问题都清楚时停止。
```

## 3. Simon Willison：约束结论如何获得

### 训练重点

- 先构造最小复现或可靠反馈环，再解释原因。
- 区分代码或实验直接证明的事实、由事实支持的推断、尚未验证的假设。
- 优先使用源码、官方文档、规范、发布记录和可复现实验。
- 来源冲突时保留冲突，不为了答案整齐而自行合并。
- 最后指出下一项最能减少不确定性的实验。

### 不要学成什么

不要把流畅解释当作证据，也不要一次改变多个变量后再猜根因。

### Natural Final Prompt

```markdown
当前需要判断这个失败究竟来自版本行为、环境限制还是调用方式，而不是先给出一个听起来合理的解释。

先构造能够稳定复现问题的最小命令，确认当前环境下的真实表现；之后一次只改变一个变量，并记录每次结果。优先使用源码、官方文档、版本记录或实际实验，不用二手推测替代证据。

本轮不要直接修改生产配置，也不要把相关性当成因果关系。

最后分别说明已经确认的事实、由事实支持的推断、仍未排除的假设，以及下一项最能减少不确定性的实验。
```

## 4. Lilian Weng：从单次 Prompt 提升到 Harness

### 训练重点

- 不只修复本次错误，先判断失败发生在哪一层。
- 区分模型能力、上下文、路由、工具环境、验证反馈与停止条件。
- Harness 改动先形成假设，再选择真实 probe 和基线。
- 用指标比较改造前后，并提前定义 retain / rollback。
- 单个 case 默认只是 hypothesis，不直接晋升为长期规则。

### 不要学成什么

不要把所有 Agent 失败都归因于 Prompt，也不要因为单次成功就增加永久规则。

### Natural Final Prompt

```markdown
这个 Agent 失败不应只被当成一次 Prompt 写得不好。更重要的是判断系统为什么没有在执行前提供必要上下文，或没有在失败后给出足够反馈。

请把本次失败分别映射到模型能力、上下文、知识路由、工具环境、验证反馈和停止条件，判断主要缺口出现在哪一层。

本轮只提出一个最小 Harness 假设，并选择两个真实 case 建立改造前基线。不要因为单个 case 有效就晋升为长期规则，也不得通过降低验证要求获得表面改善。

完成时给出失败归因、最小改动、对比指标，以及保留或回滚该改动的条件。
```

## 5. Boris Cherny：任务清晰后再 Loop 化

### 训练重点

- Loop 之前必须先有清晰 Goal、当前状态和可执行验证。
- 每轮重新读取最新代码和反馈，不沿用过时假设。
- 一轮只处理当前 slice 中影响最大的一个偏差。
- 明确 `PASS / RETRY / BLOCK` 与人工升级条件。
- 并行 Agent 适合独立调查，不适合同时设计整套系统。

### 不要学成什么

不要把“持续推进”当成 Loop。没有反馈和停止条件的循环只是重复。

### Natural Final Prompt

```markdown
当前方案、任务边界和 replay 验证方式已经确定，现在需要把 Slice A 推进到可验证完成，而不是重新规划整个迁移。

每轮读取最新代码和验证结果，只选择影响当前 slice 的一个最大偏差，完成最小修改后运行 build 和 replay，再根据证据决定继续、重试或阻塞。不要提前进入后续 slice，也不要顺手处理相邻重构。

只要失败仍能由现有证据解决，就继续推进；当 replay 满足预期时结束。若发现问题会改变已锁定的范围、生命周期或 ownership，则立即停止并升级给我决定。
```

## How the five baselines compose

五类方法不是互斥的，但应按任务成熟度逐步叠加：

1. 先用 Anthropic 基线把任务表达清楚。
2. 任务仍模糊时，用 Matt 的概念管理 discovery，而不是直接实现。
3. 涉及事实判断、排障或研究时，用 Simon 的证据纪律约束结论来源。
4. 同类失败重复发生时，再用 Lilian 的视角判断是否应改 Harness。
5. 只有任务、边界和验证都稳定后，才用 Boris 的方式进入 Loop。

最终成稿仍然只有一份自然 Prompt。不要为了展示多个方法，把它拼成五套标题或重复说明。

## Review questions

写完 Prompt 后检查：

- Anthropic：模型是否理解真正问题、本轮边界和即时任务？
- Matt：当前可推进边界与仍保留的 fog 是否清楚？
- Simon：关键结论是否有事实、来源或实验路径？
- Lilian：这仍是单次 Prompt 问题，还是已经暴露 Harness 缺口？
- Boris：验证闭环是否足以支持自动循环和明确停止？

这些问题只用于 review，不要求全部出现在 Final Prompt 中。

## Evidence boundary

本文是 Prompt Atlas 当前的训练综合，不是五位作者或团队方法论的完整归档。后续收录官方材料时，应分别建立 source record，并区分原始事实、当前综合与推断。
