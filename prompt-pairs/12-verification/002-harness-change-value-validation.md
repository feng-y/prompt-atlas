# Fable：Harness 修改的正向价值与负向回归验证

**标签**：Verification / Review / Harness / Loop  
**目标模型**：Fable  
**证据状态**：原文；运行结果待补

**来源**：[Fable repo navigation, repair and value validation](../../sources/src-2026-07-11-fable-navigation-repair-validation.md)

## Current Prompt

> 已经让 Fable 修改了，现在需要让 Fable 运行一些测试验证修改的价值，以及是否有负向价值。

## Problem Analysis

修改完成并不等于 Harness 得到改善。若继续使用修改过程中已经分析过的目标，Fable 很容易复述既有结论，无法证明新入口、路由或验证规则具有跨目标价值。

验证需要使用未参与修改过程的 holdout 目标和新上下文，同时检查正向收益与负向回归：是否更快进入正确 owner，也是否出现过早收敛、错误合并、额外读取、局部经验泛化或压制必要人工判断。

## Minimal Rewrite

> 从导航目录选择 2–3 个未参与修改的目标，在新上下文中分别从 `CLAUDE.md` 进入。比较 anchor、owner、unknown routing、verification 和人工纠正点，同时主动检查错误收敛、知识污染、额外读取与必要 unknown 被压制。根据证据决定保留、收窄或回滚。

## Why It Is Better

它把“测试一下”转成 holdout validation，避免用训练样本证明自己；同时把负向价值列为一等验证对象。最终 verdict 依赖行为差异，而不是文档完整度或最终答案看起来合理。

## Transferable Principle

Harness 修改必须通过未参与修改过程的独立目标验证，并同时证明收益与无明显负向回归。

## Outcome（执行后补）

- Holdout 目标：
- 正向改善：
- 负向影响：
- 人工纠正变化：
- retain / narrow / rollback verdict：
- 是否具备跨目标证据：

## Final Prompt

基于刚才的 Harness 修改，从“业务面导航检查目录”中选择 2–3 个未参与修改过程的目标，使用新上下文分别从 `CLAUDE.md` 独立进入。

比较修改后的第一个 anchor、真正 owner、unknown 自解路径、verification gate 和人工纠正点，判断是否比修改前更准确、更早收敛。

同时主动检查负向价值：是否错误合并不同业务或请求路径、过早锁定 owner / scope / gate、增加无关读取、把局部经验固化为通用规则，或压制必要的 unknown 与人工裁决。

不要以最终答案看起来正确作为通过标准。根据可观察行为和证据给出 `retain / narrow / rollback`，并说明当前证据是否足以证明跨目标价值；证据不足时只保留为 hypothesis，不继续扩写 Harness。
