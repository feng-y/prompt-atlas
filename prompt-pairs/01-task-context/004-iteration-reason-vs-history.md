# Iteration Reason vs History：Replay Target Selection Gap

**标签**：Task Context / Decision Framing / Harness / Verification  
**目标模型**：Fable  
**证据状态**：原始表达与对照分析已记录；执行结果待补

## Current Prompt

> 当前不是重构 harness 以及大的架构调整，Fable 诊断出 harness 层 replay 选择缺失问题，从 harness 感知触发，定位 replay 层的 gap，然后修复。

## Problem Analysis

这段 Prompt 已经表达了三个关键判断：

- 当前不是 Harness 重构或大的架构调整；
- Fable 已发现 replay target selection 的缺口；
- 本轮应从 Harness 感知链路定位并修复 gap。

真正的问题不是信息缺失，而是信息仍按“作者想到问题的顺序”排列：先给 Boundary，再给发现，再给动作。模型需要自己重组为“为什么这一轮存在 → 当前系统失败在哪里 → 本轮边界 → 如何处理”。

这里最值得训练的不是增加更多上下文，而是调整第一段的 Decision Hierarchy：让模型先形成对本轮存在原因的正确判断，再把 Fable 的诊断、历史迁移和兼容背景作为 supporting context。

## Highest-leverage Change

第一段不要从“不是重构”或历史背景开始，而应先说明：

> Harness 当前在哪个真实任务路径上不能稳定工作，以及为什么这值得单独开启一轮修复。

Fable 是问题的发现来源，不是问题本身；Replay 是表现层，真正的风险是 verification 可能得到“PASS，但没有覆盖改动”的假阳性。

## Minimal Rewrite

> Fable 在真实需求分析中发现：Harness 虽然已经能够进入 replay 验证，但 replay target selection 不能稳定推导真正覆盖改动的目标，导致 verification 存在假阳性风险。
>
> 本轮不是继续重构 Harness，也不是调整整体架构，而是从 Harness 的感知与路由入口开始，定位这个 gap 出现在需求识别、unknown routing、replay mapping 还是 verification routing，并完成最小修复。

## Why It Is Better

改写没有引入新的任务，只重新组织了已有信息：

- 把“为什么这一轮存在”放到第一判断；
- 把 Fable 的发现降为 evidence，而不是主语；
- 把 replay 选择缺失解释为 verification 覆盖风险；
- 把“不是重构”从开场限制改成问题明确后的控制边界；
- 保留模型定位责任边界的空间，没有提前把根因锁死在 replay 配置层。

减少的模型决策成本是：模型不再需要先从 Boundary、Agent 诊断和修复动作中反推出真正的问题。

## Transferable Principle

在持续演进的工程项目中，Prompt 第一段优先建立 **Iteration Reason**：说明当前系统哪里不能稳定工作、为什么值得开启这一轮。Commit 历史、Agent 发现过程和兼容背景应作为 supporting context，而不是模型的第一判断。

## Outcome（执行后补）

- 实际发送版本：待补
- 模型结果：待补
- 是否直接进入 replay target selection：待补
- 是否减少无关架构分析：待补
- smoke / eval verdict：待补
- 下次只保留什么：待补

## Final Prompt

Fable 在真实需求分析中发现：当前 Harness 已经能够把任务送入 replay 验证，但还不能稳定推导真正覆盖改动的 replay target。这会带来最危险的 verification 假阳性：结果显示 PASS，但实际没有覆盖到变更。

这次不是继续重构 Harness，也不是做大的架构调整。请从 `CLAUDE.md`、`ARCHITECTURE.md` 和 `harness/README.md` 开始，沿 Harness 的真实感知、路由和验证入口理解这条链路，判断 replay target selection 的缺口究竟出现在需求识别、unknown routing、replay mapping 还是 verification routing。

不要预设根因，也不要直接从 replay 配置或文档修补开始。先用 repo 证据确认责任边界，再只修复导致 replay 目标选择不稳定的最小 gap；保持 Harness 现有控制面与接口不变，不扩大到整体架构演进。

本轮完成时，需要给出：gap 的准确位置及证据、最小修复、正确 replay target 的推导结果，以及基于真实 smoke / eval 的验证，证明 Harness 的 L3 完成度、可见性、控制面和 Wayfinder 所看到的控制面都没有退化。