# 结构迁移 Review：把“禁止逻辑漂移”变成可判断的等价性标准

**标签**：Review / Refactor / Boundary / Success / Verification  
**目标模型**：Codex / Claude Code / Fable / GPT-5.5  
**证据状态**：原文；Prompt 已完成对照改写，真实分支 Review Outcome 待回填。

## Current Prompt

> 当前分支是把 galaxy 请求从 Model 的派生类上移到 Mode 里面，并对所有的派生完成的迁移，本次修改结构调整，禁止导致业务逻辑漂移（部分 log/metrics/latency 微小变更允许）， 同时检查是否有其他扩大的修改 ，最后输出 review 结果，哪些逻辑漂移， 是否存在逾期未的顺手优化

## Improvement

原 Prompt 的 Goal 和 Boundary 已经比较明确：这是一轮 responsibility lifting / 结构迁移，业务行为应基本保持不变，并允许少量 observability 差异。

最影响结果的问题不是缺少结构，而是**验收模型仍然隐含**。模型知道“不能逻辑漂移”，却需要自己猜应该通过哪些维度判断等价；同时，“所有派生已完成迁移”更像一个已知事实，而不是需要 Review 验证的目标状态，“有没有扩大修改”也缺少明确的 expected diff boundary。

改版只补足会改变 Review 行为的判断合同：迁移前后的调用链、执行条件、参数传递、默认行为和异常路径应保持等价；业务语义漂移与 log / metrics / latency 等 observability drift 分开报告；额外重构、顺手优化和非必要行为调整视为 scope creep；最后必须给出 migration completeness 和整体 verdict。

## Minimal Rewrite

> 当前分支的目标是将 galaxy 请求相关逻辑从 Model 派生类上移并收敛到 Model 层，并完成所有派生类的对应迁移。请基于当前分支与基线代码的实际 diff 做一次 review。
>
> 这次修改本质上是结构调整，预期不改变原有业务行为。重点检查迁移前后的调用链、执行条件、参数传递、默认行为和异常路径是否保持等价，并验证是否存在派生类迁移遗漏或新旧逻辑并存。
>
> log、metrics、latency 统计上的微小变化可以接受，但需要单独指出。同时检查是否混入额外重构、顺手优化、行为调整或其他超出本次迁移目标的修改。
>
> 最后明确说明是否存在业务逻辑漂移、允许范围内的非业务差异、scope creep，以及当前分支能否视为一次基本等价的结构迁移。

## Why It Is Better

它没有替模型规定 Review 步骤，而是把原本隐含在用户脑中的**等价性判断标准**显式化，减少模型只做文本 diff 或普通 code review 的概率。

同时把业务语义漂移、observability drift、迁移完整性和 scope creep 分成不同结论面，使“允许部分变化”不再模糊，也让最终 Review 能回答真正的 go / no-go 问题。

## Transferable Principle

**Candidate**：当任务要求 behavior-preserving refactor 时，不要只写“禁止业务逻辑漂移”；应给出足够的 observable equivalence criteria，并明确 expected diff boundary、migration completeness 与最终 verdict，但不要把它扩写成固定执行步骤。

另一个需要持续训练的表达习惯：**不要把目标状态写成已知事实**。如果“所有派生类都已迁移”本身需要验证，应写成 Review 目标，而不是作为 Context 默认模型接受。

## Outcome（执行后补）

- 实际发送版本：待回填
- 模型结果：待回填
- 返修轮次：待回填
- 证据 / verdict：待回填
- 下次只保留什么：待回填

## Final Prompt

当前分支的目标是将 galaxy 请求相关逻辑从各个 Model 派生类上移并收敛到 Model 层，同时完成所有派生类的对应迁移。

请基于当前分支与基线代码的实际 diff 做一次 review。这次修改本质上是结构调整，预期不改变原有业务行为。重点检查迁移前后的调用链、执行条件、参数传递、默认行为和异常路径是否保持等价，并确认是否存在派生类迁移遗漏、新旧逻辑并存或迁移后行为只在部分类型上发生变化。

log、metrics、latency 统计上的微小变化可以接受，但需要与业务语义漂移分开指出；如果这些变化会影响计数语义、统计范围、关键 tag 或实际可观测结论，也需要明确说明。

同时检查当前 diff 是否混入超出本次迁移目标的修改，例如额外重构、顺手优化、无关 cleanup、非必要的抽象变化或业务行为调整。

最终给出明确结论：哪些地方存在业务逻辑漂移；有哪些属于可接受的 log / metrics / latency 等非业务差异；是否存在迁移遗漏或新旧逻辑共存；是否存在超出本次目标的 scope creep；以及当前分支是否可以视为一次基本等价、可接受的结构迁移。
