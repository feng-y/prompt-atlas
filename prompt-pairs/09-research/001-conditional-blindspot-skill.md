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

## Expert Lens

> 把文章当作候选 moves，而不是固定 workflow。先映射三个动作分别解决哪类 unknown：任务前的未知、决策中的歧义、实现中的偏离。再从 repo 的现有 intake、Wayfinder、plan 和 verification 入口判断谁已覆盖、谁仍缺失。只把重复出现且无法由现有机制承载的动作写入 skill；其余保留为按需 prompt。最终给出触发矩阵与一个最小 skill，而不是把整篇文章制度化。

## Transferable Principle

把方法写进 skill 前，先回答三个问题：它解决什么失败模式、何时触发、现有 harness 是否已经覆盖。

## Final Prompt

请把这篇文章中的 `blindspot pass`、`one-question interview` 和 `implementation notes` 视为三个候选动作，而不是一套默认在每个 session 全量运行的 workflow。

先判断它们分别解决哪类问题：任务开始前尚未暴露的未知、决策过程中会改变方案的歧义，还是实现阶段的偏离与交接。然后结合当前 repo 的 intake、Wayfinder、plan 和 verification 入口，确认哪些能力已经被覆盖、哪些失败模式仍然缺少稳定承载点。

只有当某个动作会重复出现、无法由现有机制承载，并且能够说明清楚触发条件、跳过条件和产物消费者时，才把它写入 repo-local skill；其余保留为按需 Prompt。

本轮只输出判断依据、触发矩阵和最小 skill 草案，不安装或修改现有 workflow，也不要把整篇文章直接制度化。
