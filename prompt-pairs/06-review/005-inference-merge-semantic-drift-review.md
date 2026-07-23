# Inference 接入 Review：新增实现成立，同时保护稳定 merge 语义

**标签**：Review / Evidence / Boundary / Verification  
**目标模型**：Fable / Claude Code / Codex  
**证据状态**：原文 + 对照改写；真实分支 Review Outcome 待回填  
**来源**：[最近工程 Prompt：自治空间、语义漂移与连续 ticket loop](../../sources/src-2026-07-23-recent-prompt-contract-lessons.md)

## Current Prompt

> review 下分支对于 inference 的实现逻辑，实现总结，同时对原有的 merge 模块无逻辑漂移。

## Improvement

这个 Prompt 同时包含两个不同但必须一起成立的结果：一是新 inference 实现本身正确且完整，二是它接入后没有改变稳定 merge 模块的既有业务语义。

如果只写“review inference + merge 无漂移”，模型很容易退化成普通 diff review，或者把所有修改混在一个 correctness 判断里。改版需要把新路径 correctness 与稳定模块 semantic preservation 分开，同时明确哪些差异属于允许的结构/observability 变化，哪些属于真实业务漂移或 scope creep。

## Minimal Rewrite

> Review 当前分支的 inference 实现，并总结它的入口、核心数据流、主要责任和与现有 merge 的协作方式。除了判断新实现是否完整、正确，还要以基线行为为参照验证 merge 的触发条件、输入语义、处理顺序、默认/异常路径和输出结果是否保持等价。
>
> 将 inference 自身 correctness、merge semantic drift、可接受的 log/metrics/latency 等非业务差异、scope creep 和仍未验证的 unknown 分开报告，最后明确当前分支是否可以认为“新 inference 实现成立，同时原有 merge 业务语义保持不变”。

## Why It Is Better

它定义了两个独立 acceptance surfaces，并要求分别举证，避免“新功能看起来能跑”掩盖对稳定模块的回归，也避免把结构适配误判成业务漂移。

## Transferable Principle

**Candidate**：当新能力接入一个已有稳定模块时，Review 应分别证明“new path correctness”和“existing path preservation”，而不是用一个笼统的 overall correctness 合并两类证据。

## Outcome（执行后补）

- 实际发送版本：待回填
- 模型结果：待回填
- 返修轮次：待回填
- 证据 / verdict：待回填
- 下次只保留什么：待回填

## Final Prompt

Review 当前分支中 inference 相关实现，并给出一份能够解释真实执行逻辑的实现总结。需要说明这次实际新增或调整了什么，inference 从哪里进入现有链路，核心数据如何流转，各主要组件承担什么责任，以及它最终如何与原有 merge 模块协作。

这次 Review 的另一个硬目标是确认稳定的 merge 业务语义没有因为 inference 接入发生非预期变化。请以基线代码和真实调用链为证据，对比 merge 前后的触发条件、输入集合与过滤语义、处理顺序、默认行为、fallback、空输入和异常路径以及最终结果。不要因为代码被移动、接口被适配或结构看起来等价就直接判定无漂移；执行时机、共享状态和生命周期变化也需要纳入判断。

将结论明确区分为：inference 实现自身的 correctness 风险、merge 的真实 semantic drift、允许范围内的结构或 log / metrics / latency 等非业务差异、超出本次目标的顺手优化或 scope creep，以及目前无法由代码或验证证明的 unknown。与本次 inference / merge 变化无关的历史问题不作为主要 Review 结论。

最终先给出简洁的 Inference Implementation Summary，再给出 Merge Semantic Drift Review 和 supporting evidence，并明确 verdict：当前分支是否可以认为 inference 实现成立，同时原有 merge 业务语义保持不变；如果不能，指出阻止这一结论的具体漂移或未验证风险。