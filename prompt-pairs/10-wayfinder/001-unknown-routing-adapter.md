# Wayfinder：把 repo unknown 路由接入 discovery

**标签**：Wayfinder / Unknowns / Control Plane  
**证据状态**：依据既有方案归纳，最终 warmup prompt 原文待补。

**来源**：[Prompt Atlas bootstrap conversations](../../sources/src-2026-07-10-prompt-atlas-bootstrap.md)

## Current Prompt（摘录）

> 我就需要 Wayfinder 介入，因为现在主要靠 cc 自我感知，导致控制力过弱，这是最大的短板。Wayfinder 本身就有 Grill，怎么适配？我理解只是附加自己的约束把 unknown 路由带入？

## Problem Analysis

真正目标是增强 intake/control plane，而不是新增一套执行 workflow。原表达没有说明 Wayfinder 应消费什么 repo-owned 信息，也没有定义介入到哪里为止。

## Minimal Rewrite

> 目前最大的短板是任务入口依赖 CC 自我感知。我希望用 Wayfinder 增强 discovery，但不替换现有 Matt workflow。请让它在形成 SPEC 前显式读取 repo 的任务入口、架构边界、unknown 升级规则和 verification gate；输出最小适配方式，并判断哪些信息应由 repo harness 提供，而不是写进 Wayfinder。

## Expert Lens

> 将 Wayfinder 定位为 L3 的 spec-discovery intake：它负责把 intent 映射为 `scope / branches / unknowns / verification / current slice`，但不负责实现和长期记忆。请检查现有 repo 是否已经为这五项提供 canonical source；缺失时补 adapter 或 context route。Grill 只在会改变方案的问题上介入。最终产物应足以进入 `/to-spec`，同时保留 fog，不要求在 discovery 阶段消灭所有 unknown。

## Transferable Principle

引入通用工具时，Prompt 要说明它在现有链路中的位置、输入合同和停止边界，而不是只描述它“应该更聪明”。

## Final Prompt

DaVinci 当前最大的短板不是执行能力，而是任务入口和 unknown 推进仍过度依赖 Claude Code 的自我感知。我希望用 Wayfinder 增强 discovery，但不替换 Matt 已有的 SPEC、Ticket 和 execution workflow。

请把 Wayfinder 定位为进入 SPEC 之前的 discovery intake。它需要从 repo 的稳定入口获得任务范围、架构边界、当前 unknown、verification gate 和可推进的 current slice，但不负责实现、长期记忆或执行验证。

检查当前 repo 是否已经为这些信息提供 canonical source；缺失部分优先通过 repo-local context route、adapter 或 standing instruction 补齐。Grill 只处理会改变方案的意图和取舍，能够从代码、架构文档或验证结果查明的事实不要交给人回答，也不要求在 discovery 阶段消灭所有 fog。

最终给出最小 binding 方案、Wayfinder 与 repo harness 的职责边界，以及一份足以稳定进入 `/to-spec` 的 handoff 内容。
