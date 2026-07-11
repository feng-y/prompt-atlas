# DaVinci Harness：从迁移历史进入残留语义清理

**标签**：Task Context / Architecture / Boundary / Verification  
**目标模型**：Claude Code / Fable / Codex  
**证据状态**：原文；已 Review，尚未执行验证

## Current Prompt

> Davinci 的 harness 层在上一个 commit，从 core + workflow 调整为 core + path，上一个 commit 为了兼容，还保留部分 workflow 的框架以及文件 pointer。
>
> 请从 CLAUDE.md、ARCHITECTURE.md、harness/README.md 开始，理解 harness 的路由机制，判断 harness 入口限制在 harness/core，以及 docs/agents 的 Wayfinder 判断 harness 的控制面是否可进入、不依赖 workflow。
>
> 不改变 harness/core 以及 harness/path 的接口，主要是移除残留的 harness/workflow 兼容语义，进一步消除残留 gap。
>
> 本次完成时，要验证 harness 的 L3 完成度不会降低，harness 的可见性和控制面以及 Wayfinder 显示的控制面不变动，同时基于 smoke test 的 eval 测试验证 harness 的完成度。

## Problem Analysis

### 已经做得好的地方

- 背景、修改边界和验证要求都已提供，信息并不缺失。
- 明确要求保持 `harness/core` 与 `harness/path` 的接口不变，能够限制错误的架构扩张。
- 已经指出需要从 `CLAUDE.md`、`ARCHITECTURE.md`、`harness/README.md` 进入，并要求关注 Wayfinder、控制面和 L3 完成度。

### 最影响结果的一处问题

原 Prompt 按 commit 的时间顺序展开，而不是按当前设计问题展开。模型先看到“上一轮做了什么”，需要自行总结本轮真正要解决的是：`workflow` 是否已经退出 Harness 控制面，以及残留兼容语义是否仍在影响入口判断。

因此，原 Prompt 的主要问题不是缺少 Context，而是 Context 没有形成清楚的信息层级：历史、判断对象、修改任务和验证证据权重接近，需要模型重新排序。

### 如果只改一处，改哪里最值

把第一段从“迁移历史”改为“当前遗留问题”：先明确 Harness 架构已经稳定，本轮不是继续演进架构，而是清理 `harness/workflow` 的残留兼容语义，并证明 Workflow 已不再是进入控制面的必要条件。

## Minimal Rewrite

> 上一个 commit 已经完成 DaVinci Harness 从 `core + workflow` 向 `core + path` 的迁移，但为了兼容仍保留了部分 `harness/workflow` 框架和文件 pointer。本轮不是继续调整 Harness 架构，而是确认 Workflow 是否已经不再承担控制面职责，并清理剩余兼容语义，使 Harness 的真实入口与当前设计一致。
>
> 请从 `CLAUDE.md`、`ARCHITECTURE.md` 和 `harness/README.md` 开始理解路由机制，重点判断 Harness 的真实入口是否已收敛到 `harness/core`，以及 `docs/agents` 中 Wayfinder 所看到的控制面是否能够完全通过 Harness 进入、不再依赖 Workflow。
>
> 保持 `harness/core` 与 `harness/path` 的接口不变，只移除残留的 `harness/workflow` 兼容语义，进一步消除实现与设计之间的 gap。
>
> 完成后需要证明：Workflow 已不是 Harness 进入控制面的必要条件；Harness 的 L3 完成度没有降低；Harness 的可见入口、控制面以及 Wayfinder 所展示的控制面保持不变；并通过 smoke test 与 eval 给出验证证据。

## Why It Is Better

- “本轮不是继续调整 Harness 架构”明确了设计阶段，避免模型把清理任务扩张成新一轮架构重构。
- “Workflow 是否已经不再承担控制面职责”把隐含目标改成显式判断，后续 code read 和修改都能围绕同一个问题展开。
- “Workflow 已不是 Harness 进入控制面的必要条件”把设计成功标准与 smoke test/eval 证据分开：前者是需要证明的结论，后者是支持结论的证据。
- 信息从“迁移历史 → 多项动作”重排为“当前问题 → 判断对象 → 修改边界 → 验证结论”，减少模型重新组织 Prompt 的决策成本。

## Transferable Principle

当历史迁移信息很多时，不要从“上一轮做了什么”开始；先说明迁移后仍未闭合的设计问题，再把 commit 历史作为支持该判断的背景。

## Outcome（执行后补）

- 实际发送版本：待补
- 模型结果：待补
- 返修轮次：待补
- 证据 / verdict：待补
- 下次只保留什么：待补

## Final Prompt

上一个 commit 已经完成 DaVinci Harness 从 `core + workflow` 向 `core + path` 的迁移。当前真正需要处理的不是继续演进 Harness 架构，而是上一轮为了兼容仍保留了部分 `harness/workflow` 框架和文件 pointer，使实现中还存在 Workflow 参与控制面判断的残留语义。

请从 `CLAUDE.md`、`ARCHITECTURE.md` 和 `harness/README.md` 开始理解当前 Harness 的路由机制，判断真实入口是否已经收敛到 `harness/core`，以及 `docs/agents` 中 Wayfinder 所看到的控制面是否能够完全通过 Harness 进入、不再依赖 Workflow。重点找出仍会让 Agent、文档入口或路径判断把 Workflow 视为必要控制面的残留 gap。

Harness 当前的 `core + path` 设计与接口保持不变，不修改 `harness/core` 和 `harness/path` 的接口，也不引入新的路由层。本轮只清理残留的 `harness/workflow` 兼容框架、文件 pointer 和相关语义，使实现、文档入口与当前设计继续收敛。

完成时需要给出 repo 证据并验证：Workflow 已不再是进入 Harness 控制面的必要条件；Harness 的可见入口和控制面保持不变；Wayfinder 所展示和使用的控制面保持不变；L3 完成度没有降低。最后通过现有 smoke test 与 eval 验证清理后的 Harness 能力没有退化；如果现有测试无法覆盖上述判断，明确指出缺失的可观察证据，而不要用测试通过代替架构结论。