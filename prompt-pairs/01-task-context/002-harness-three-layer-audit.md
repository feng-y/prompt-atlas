# Harness：从“借鉴什么”变成明确的审视任务

**标签**：Task Context / Architecture / Review  
**证据状态**：依据多轮讨论重建，原始 Prompt 待补。

## Current Prompt（摘录）

> 对我的 harness 的启示借鉴是什么？如何引导或者基于 Fable 构建这层 harness？

## Problem Analysis

问题同时包含“理解文章”“评价现状”“设计下一步”，模型很容易输出一套通用 harness 框架。真正的困惑是：现有三层是否够用，以及 Fable 应该补哪里。

## Minimal Rewrite

> 我暂时把 repo harness 理解为 `Context Environment / Control Plane / Verification Feedback`。当前困惑不是要不要再建一套 workflow，而是怎样让 Fable 结合 repo reality 补齐这三层。请基于现有入口和验证能力审视缺口；允许质疑这个三层划分，但不要引入新 framework。最后给出优先级判断。

## Expert Lens

> 先把外部文章当作观察视角，而不是目标架构。用它检查当前 repo 的三类 surface：AI 能否进入正确上下文、任务如何被约束和路由、失败如何被 replay/eval 反馈回来。重点找“已有能力没有成为稳定入口”的地方，而不是重新发明 workflow。若三层划分遮蔽了关键问题，请直接挑战；最终只保留一个当前最高杠杆改进，并说明它将改变哪个真实任务的行为。

## Transferable Principle

引用外部方法时，先声明它只是 lens，再让模型回到 repo reality；否则“借鉴”很容易变成复制一套新框架。
