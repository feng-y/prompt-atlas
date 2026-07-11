# Fable：单目标导航探测与高价值修复

**标签**：Loop / Harness / Architecture / Verification  
**目标模型**：Fable  
**证据状态**：原文；运行结果待补

**来源**：[Fable repo navigation, repair and value validation](../../sources/src-2026-07-11-fable-navigation-repair-validation.md)

## Current Prompt

> 让 Fable 从 `CLAUDE.md` 进入 FeatureTable 需求。
>
> 观察它：
> - 第一个 anchor 找到什么；
> - 是否进入正确架构边界；
> - unknown 路由到哪里；
> - 是否找到 replay gate；
> - 在哪里仍需要人工纠正。

## Problem Analysis

这个 Prompt 已经定义了一个有效 probe，但只有观察，没有把观察结果转成可验证的 Harness 改进。Fable 可能识别出错误路由或人工纠正点，却只留下报告；也可能看到任何缺口就扩写文档，无法区分一次性业务细节与值得修复的通用问题。

最有价值的补充，是把单目标 probe 接到一个受控的 `observe → minimal repair → fresh rerun → retain / rollback` 闭环，并限制每轮只修一个会改变后续 route、scope、owner、gate 或 human boundary 的高价值缺口。

## Minimal Rewrite

> 让 Fable 从 `CLAUDE.md` 独立进入一个业务目标，观察首个 anchor、真正 owner、unknown routing、verification gate 和首次人工纠正点。若纠正点会重复影响后续任务，只选择一个最高价值 Harness 缺口做最小修复，并在新上下文中重新进入同一目标；行为确有改善才保留，否则回滚。

## Why It Is Better

它保留了原 Prompt 的弱引导特征，没有预先给出代码答案，却补上了价值筛选、最小修改、独立复测和回滚条件。模型不再以“发现了问题”或“文档更完整”作为成功，而必须证明导航行为发生了正向变化。

## Transferable Principle

真实目标既可以是需求执行入口，也可以是 Harness probe；修复只有在同一目标的新上下文复测中改善可观察行为时才成立。

## Outcome（执行后补）

- 实际发送版本：
- 首个 anchor / owner：
- 被修复的 Harness 缺口：
- 修复前后行为差异：
- retain / rollback verdict：

## Final Prompt

让 Fable 从 `CLAUDE.md` 独立进入 `<业务目标>`，不要预先提供代码入口。

观察第一个 anchor、真正的架构 owner、unknown 被路由到哪里、是否从实际执行路径找到 verification gate，以及第一次仍需要人工纠正的位置。

如果这个纠正点会重复影响后续任务，并会改变 route、scope、owner、gate 或 human boundary，只选择一个最高价值的 Harness 缺口做最小修复。然后使用新上下文重新进入同一目标，比较修复前后的导航行为。

只有首个 anchor、owner 判断、unknown 自解或 verification gate 出现可观察改善时才保留修改；没有改善、引入错误收敛或只是增加文档时回滚。局部业务细节不要提升为长期规则，剩余问题主要需要业务裁决时停止。
