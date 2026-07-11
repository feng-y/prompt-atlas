# Fable：从“整理文档”进入 repo L3 对齐

**标签**：Task Context / Architecture / Boundary  
**证据状态**：历史对话摘录，可追溯；最终版本需回填原会话完整文本。

**来源**：[Prompt Atlas bootstrap conversations](../../sources/src-2026-07-10-prompt-atlas-bootstrap.md)

## Current Prompt（摘录）

> 现在要做的是让 fable 进行 repo 的一致性对齐，从 CLAUDE.md 以及 ARCHITECTURE.md 如何进入渐进式感知 L3。你不要想着大改现有的知识体系，引导式 prompt，让 fable 自己处理。至少要说明 harness 会 L3 的适配，引导也要有导向，但不要给 Fable 设置非常具体的目标。

## Problem Analysis

意图其实很清楚：不是改业务代码，也不是重写知识库，而是让 Fable 自己判断 repo harness 与 L3 的差距。问题在于：

- “一致性对齐”缺少判断对象，模型可能退化成文档整理。
- “不要具体目标”与“至少说明 L3 适配”并不冲突，但原表达没有把二者组成决策边界。
- 没有明确这一轮先判断、再最小调整，容易直接进入大改。

## Minimal Rewrite

> 请从 `CLAUDE.md`、`ARCHITECTURE.md` 和现有 `docs/workflow` 判断：repo 当前如何支撑 L3（明确需求自助完成 + bounded learning），哪些入口与 repo reality 仍不一致。让 Fable 自行推进最小对齐，不重建知识体系，也不要预设具体改造方案；先给出判断、证据和最值得调整的一处。

## Why It Is Better

它补的不是步骤，而是 Decision Context：工作性质、观察面、允许挑战的空间、最小变更原则与最终判断都清楚了。

## Transferable Principle

当你不想过度约束模型时，不要删掉方向；改为说明“判断对象 + 允许挑战 + 最小边界 + 最终要做的判断”。

## Final Prompt

DaVinci 当前不是缺少更多文档，而是需要确认现有 repo harness 是否真的能够支撑 L3：让 Fable 在明确需求下自助完成任务，并只进行有限、可控的学习改进。

请从 `CLAUDE.md` 开始，沿它指向的架构边界、workflow 路由和验证入口理解当前机制，判断这些入口与 repo reality 是否一致。把这次工作视为 repo harness alignment，而不是文档整理或知识体系重建。

已有结构能够承载的就继续沿用，只处理会真实影响任务进入、unknown routing 或 verification feedback 的不一致。不要预设具体改造方案，也允许你质疑我对 L3 的理解。

本轮完成时给出当前 L3 支撑能力的判断、对应的 repo 证据、最值得调整的一处，以及为什么现阶段不需要更大的改造。
