# Blindspot：从“每次自动运行”改为条件触发

**标签**：Research / Unknowns / Skill Design  
**证据状态**：原始 Prompt 可追溯。

**来源**：[Prompt Atlas bootstrap conversations](../../sources/src-2026-07-10-prompt-atlas-bootstrap.md)

## Current Prompt

> Read this article. Then write yourself a SKILL file from it, so you apply the blindspot pass, the interviews, and the implementation notes on every future session in this repo without me asking.

## Problem Analysis

它把知识提炼、skill 设计、触发策略和安装动作绑在一起，并要求“每次会话全部运行”。这会造成不必要的上下文与交互成本，也把不同阶段的动作混成一个固定流程。

## Minimal Rewrite

> 先从这篇文章提炼 `blindspot pass`、`one-question interview`、`implementation notes` 三种动作，并结合本 repo 判断各自在什么任务条件下触发。输出一个 repo-local skill 草案，但不要默认每次会话全部执行；把触发条件、跳过条件和产物落点写清楚。

## Transferable Principle

把方法写进 skill 前，先回答三个问题：它解决什么失败模式、何时触发、现有 harness 是否已经覆盖。

## Final Prompt

### Goal

把 blindspot pass、one-question interview 与 implementation notes 变成按任务条件触发的能力，而不是每个会话都强制执行的固定流程。

### Current Context

文章提供了三种有价值的动作；repo 已有 intake、Wayfinder、plan 与 verification 入口，尚未确认哪些动作已被覆盖、哪些是真实缺口。本轮是方法与触发策略设计。

### Design Intent

只固化重复出现且无法由现有 harness 承载的动作；将其余动作保留为按需 Prompt，避免知识和流程膨胀。

### Boundary

不要把整篇文章制度化，不要默认每个会话执行所有动作，不要新增平行 workflow。

### Immediate Task

分别判断三种动作解决哪类 unknown、适用什么任务条件、何时跳过、产物应落在哪里，并检查现有 repo 是否已覆盖。

### Expected Output

输出触发矩阵、已有覆盖与真实缺口、一个最小 repo-local skill 草案，以及不应固化的动作。

### Success / Stop Condition

当每个动作都有明确触发与跳过条件、且最小 skill 不重复现有机制时完成。若触发策略会改变现有 workflow 所有权，停止并请求人工决策。
