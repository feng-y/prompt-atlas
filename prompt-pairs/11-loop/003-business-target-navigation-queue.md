# Fable：业务目标导航队列逐项推进

**标签**：Loop / Task Context / Harness / Architecture  
**目标模型**：Fable  
**证据状态**：原文；运行结果待补

**来源**：[Fable repo navigation, repair and value validation](../../sources/src-2026-07-11-fable-navigation-repair-validation.md)

## Current Prompt

> FeatureTable 已经处理了。现在需要让 Fable 探测并处理其他目标。不要过长的 Prompt，先读取业务目标导航文件，然后逐个分析。

## Problem Analysis

用户需要的不是一次性“整体架构分析”，而是把已有导航文件当作动态目标队列，让 Fable 每次选择一个未处理目标，独立进入 repo，完成 probe、必要修复和状态更新。

如果缺少队列边界，Fable 容易一次性遍历完整清单、复用导航文件里的答案、生成新的业务知识体系，或在一个目标尚未验证时提前扩展到其他目标。

## Minimal Rewrite

> 先读取业务目标导航文件，把它作为待检查队列。跳过已处理的 FeatureTable，从最高优先级未处理目标开始，每次只处理一个；从 `CLAUDE.md` 独立进入，检查 anchor、owner、unknown routing、verification 和人工纠正点。高价值 Harness 缺口最小修复并复测后，再更新状态进入下一个目标。

## Why It Is Better

它把导航文件从“长期真相”降级为任务队列，同时给出单目标串行推进、独立导航、修复验证和停止条件。Prompt 足够短，不替 Fable 预设完整分析过程，也避免把所有业务面一次性摊平。

## Transferable Principle

大型 repo 的整体感知应由一系列独立、高信息增益的目标 probe 累积，而不是由一次性全景总结完成。

## Outcome（执行后补）

- 实际发送版本：
- 已处理目标：
- 新发现的高价值 Harness 缺口：
- 队列重排或删除：
- 当前停止原因：

## Final Prompt

先读取“Fable 业务面导航检查目录”，把它作为待检查目标队列。FeatureTable 已处理，跳过。

从优先级最高的未处理目标开始，每次只处理一个。从 `CLAUDE.md` 独立进入 repo，检查第一个 anchor、真正 owner、unknown routing、实际 conf / schedule / RPC 对应的 verification gate，以及仍需人工纠正的位置。

若发现会重复影响后续任务的高价值 Harness 缺口，做最小修复，并在新上下文中重新进入同一目标；有明确改善才保留，否则回滚。局部业务细节只保留为当前观察，不写入长期知识。

完成后更新检查状态，再进入下一个目标。不要一次性分析完整清单；剩余问题主要需要业务裁决，或继续探测已不再增加导航价值时停止。
