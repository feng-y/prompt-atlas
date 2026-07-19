# Harness Smoke Test：用真实复杂任务验证自主推进，而不是预设 Pipeline

**标签**：Verification / Harness / Wayfinder / Loop / Boundary  
**目标模型**：Fable  
**证据状态**：原文；Galaxy split 真实任务已用于 Prompt 设计，最终 smoke test Outcome 待回填。

## Current Prompt

> 按 Wayfinder → to-spec → to-tickets 产出，然后 handoff 给 Harness loop 完整执行 tickets。

## Improvement

这条表达描述了用户常见的复杂任务路径，但把一个经验路径写成 smoke test 的预设 pipeline，会掩盖真正想验证的能力：Fable 能否根据当前任务状态和 repo reality 自主找到下一项合适能力并持续推进。

改版后保留真实任务的目标、边界和完成标准，但不把 Wayfinder、spec、tickets 或 handoff 写成必须经过的成功条件。Smoke test 观察实际路由，而不是通过 Prompt 直接指定路由；同时禁止为了通过 smoke test 主动修改 Harness，只有真实阻塞才形成后续改进证据。

## Minimal Rewrite

> 把这个真实复杂任务作为一次 Fable / Harness smoke test。请基于当前 repo 和 Harness 自主推进，使用已有的导航、研究、设计、执行和验证能力完成任务，不预设固定流程，也不需要我逐阶段触发。不要为了通过 smoke test 修改 Harness；只有遇到真正需要人工判断的 decision 或明确的 Harness 阻塞时再停下来。最终除任务结果外，说明自主推进在哪里工作正常、哪里仍需要人工介入。

## Why It Is Better

它把验证对象从“是否按指定 pipeline 执行”改成“是否能在真实任务中自主选择并使用已有能力”。这样才能区分 Harness 真正具备 progression 能力，还是仅仅服从了 Prompt 中手写的阶段编排。

## Transferable Principle

**Candidate**：验证 Harness 自主推进能力时，用真实复杂任务作为 probe，观察 `Current State → Next Capability`；不要在 smoke test Prompt 中预设固定 pipeline，也不要为了通过 probe 修改 Harness。

## Outcome（执行后补）

- 实际发送版本：待回填
- 模型结果：待回填
- 返修轮次：待回填
- 证据 / verdict：待回填
- 下次只保留什么：待回填

## Final Prompt

请把下面这个真实复杂任务作为一次 Fable / Harness smoke test 来执行。

基于当前 repo 和 Harness 自主推进任务。先从真实代码、调用链和现有知识入口理解问题，主动收敛会影响设计或实现的重要 unknown；在此基础上使用 repo 已有的能力完成必要的分析、设计、实现和验证，并持续推进到任务完成。

不要预设必须经过 Wayfinder、to-spec、to-tickets 或任何固定 pipeline。已有中间产物和当前 case 状态应影响下一步选择；能够直接执行的任务不应为了流程完整而增加阶段，真正需要 human judgment 的 decision 则应明确停下来。

不要为了让这次 smoke test 看起来成功而修改 Harness。只有真实任务推进过程中出现稳定、可复现的 Harness 阻塞时，才把它作为后续 Harness 改进证据。

过程中不需要我逐阶段触发。最终除任务本身的实现与验证结果外，说明 Fable 是否能够从任务描述自主找到并使用合适的导航、研究、设计、执行和验证能力，哪些地方工作正常，哪些地方仍然依赖人工介入，以及是否暴露出明确的 Harness 缺口。
