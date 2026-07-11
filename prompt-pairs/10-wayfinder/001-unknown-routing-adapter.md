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

## Transferable Principle

引入通用工具时，Prompt 要说明它在现有链路中的位置、输入合同和停止边界，而不是只描述它“应该更聪明”。

## Final Prompt

### Goal

降低任务入口依赖模型自我感知的风险，让 Wayfinder 在形成 SPEC 前能读取 repo 的 canonical context 并显式路由 unknown。

### Current Context

现有 Matt workflow 已包含 Wayfinder / Grill；当前短板是 discovery 阶段未必能稳定得到任务入口、架构边界、unknown 升级规则和 verification gate。

### Design Intent

将 Wayfinder 定位为 L3 的 spec-discovery intake：它建立 scope、branches、unknowns、verification 与 current slice，但不承担实现或长期记忆。

### Boundary

不要替换现有 Matt workflow，不要让 discovery 阶段消灭所有 fog，不要把 repo-owned knowledge 写进 Wayfinder 核心。

### Immediate Task

检查上述五类信息是否已有 canonical source；缺失时设计最小 adapter 或 context route，并说明 Grill 的最小介入点。

### Expected Output

给出最小适配方式、信息归属、最终可进入 to-spec 的 packet，以及仍应保留的 fog。

### Success / Stop Condition

当 Wayfinder 的输出能稳定进入 SPEC 且每类信息有归属时完成。若必须改变 Wayfinder 核心流程，停止并升级是否 fork 的人工决策。
