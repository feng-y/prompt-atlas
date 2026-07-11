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

### Goal

让 repo 的入口、架构与 workflow 能真实支撑 L3：明确需求可自助推进，并在有限范围内学习改进，而不是依赖 Fable 临场猜测。

### Current Context

当前已有 CLAUDE.md、ARCHITECTURE.md 与 docs/workflow 等入口，但尚未确认它们是否一致地向 Fable 暴露任务入口、架构边界、unknown routing 与验证反馈。本轮处于判断和最小对齐阶段，不是业务代码实现。

### Design Intent

优先让 Fable 成为 repo-aware 的共同设计者；保留既有知识结构，补齐真正影响 L3 行为的连接点。

### Boundary

不要重建知识体系，不要预设大改方案，不要把文档整理本身当成目标。已有结构能承载的能力应复用。

### Immediate Task

读取主入口、架构边界、workflow 路由与验证入口，判断 repo 当前如何支撑 L3，以及哪一处不一致最值得最小调整。

### Expected Output

给出当前能力判断、对应 repo 证据、一个最小对齐动作，以及暂不需要更大改造的理由。

### Success / Stop Condition

当能够基于证据指出一个真实影响任务进入、unknown routing 或 verification feedback 的缺口，并给出最小动作时完成。若发现会改变 L3 定义或需要重建知识体系，停止并升级人工判断。
