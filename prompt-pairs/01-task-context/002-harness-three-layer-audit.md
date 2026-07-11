# Harness：从“借鉴什么”变成明确的审视任务

**标签**：Task Context / Architecture / Review  
**证据状态**：依据多轮讨论重建，原始 Prompt 待补。

**来源**：[Prompt Atlas bootstrap conversations](../../sources/src-2026-07-10-prompt-atlas-bootstrap.md)

## Current Prompt（摘录）

> 对我的 harness 的启示借鉴是什么？如何引导或者基于 Fable 构建这层 harness？

## Problem Analysis

问题同时包含“理解文章”“评价现状”“设计下一步”，模型很容易输出一套通用 harness 框架。真正的困惑是：现有三层是否够用，以及 Fable 应该补哪里。

## Minimal Rewrite

> 我暂时把 repo harness 理解为 `Context Environment / Control Plane / Verification Feedback`。当前困惑不是要不要再建一套 workflow，而是怎样让 Fable 结合 repo reality 补齐这三层。请基于现有入口和验证能力审视缺口；允许质疑这个三层划分，但不要引入新 framework。最后给出优先级判断。

## Transferable Principle

引用外部方法时，先声明它只是 lens，再让模型回到 repo reality；否则“借鉴”很容易变成复制一套新框架。

## Final Prompt

### Goal

判断现有 repo harness 是否足以让 Fable 在真实任务中进入正确上下文、接受正确约束并从验证反馈中修复，而不是为了借鉴外部文章新建一套 workflow。

### Current Context

当前将 harness 暂分为 Context Environment、Control Plane、Verification Feedback；repo 已有入口与验证能力，但其稳定性和缺口尚未被统一判断。本轮是架构审视，不是实现。

### Design Intent

以 repo reality 为准，用三层划分作为观察视角；优先发现已有能力未成为稳定入口的问题。

### Boundary

不要引入新 framework，不要复制文章中的完整架构，不要把 workflow 重写当作默认答案。

### Immediate Task

审视三类 surface：AI 是否进入正确上下文、任务如何被约束和路由、失败如何被 replay 或 eval 反馈。识别当前最高杠杆缺口。

### Expected Output

输出三层能力判断、关键证据、一个最高优先级改进及其会改变的真实任务行为。

### Success / Stop Condition

当能说明最高杠杆改进为何优先于新建 workflow 时完成。若三层划分本身遮蔽关键问题，停止并明确提出需要人工确认的替代划分。
