# Slot 配置收敛：从字段列表转向 usage-first 责任判断

**标签**：Context / Evidence / Architecture / Refactor / Research  
**目标模型**：Fable / Claude Code / Codex  
**证据状态**：原文 + 对照改写；真实 repo 分析 Outcome 待回填  
**来源**：[最近工程 Prompt：自治空间、语义漂移与连续 ticket loop](../../sources/src-2026-07-23-recent-prompt-contract-lessons.md)

## Current Prompt

> `ModelInputConfig` 里的这些字段都是 slot 相关的数据，应该可以进一步分析每一个的使用场景、不需要的字段逻辑，以及是否可以聚合。

## Improvement

原始意图是合理的：不是立即重构，而是先理解历史 slot 数据为什么平铺在 `ModelInputConfig` 中，再判断哪些应删除、合并、迁移或保留。

第一次改写的问题是把“如何调查”写得太细，容易退化成 checklist-driven investigation。真正需要补足的不是步骤，而是判断合同：最终要解释责任边界；以真实生产/消费和生命周期作为 evidence；不能因为字段名字相似就假定同属一个 canonical 结构；也不能预设 `model_slot_opt` 已经完成替代。

## Minimal Rewrite

> 分析 `ModelInputConfig` 中现有 slot 相关状态的真实责任边界。重点基于字段的生产者、消费者、生命周期和配置来源，判断哪些仍是有效 canonical state，哪些只是派生索引、运行时辅助或历史兼容表达，以及新旧数据结构之间是否存在重复事实或替代关系。
>
> 目标不是机械减少字段或再套一层 `SlotConfig`，而是找出真正可以删除、合并或迁移的历史表达，同时保留 model-level / cross-slot 状态和真实兼容语义。所有结论都需要 repo evidence 支撑，无法证明的部分保留为 unknown。

## Why It Is Better

它把“逐字段检查”提升为一个结构判断问题，并明确了 evidence 与错误抽象的边界。模型仍然可以自主选择调查路径，但不能靠命名相似性或“结构更整洁”来证明重构成立。

## Transferable Principle

**Candidate**：做历史配置结构收敛时，先定义目标责任和 evidence bar，再让模型通过 usage/lifecycle 发现 canonical state；不要把字段清单直接变成执行步骤，也不要预设最终聚合结构。

## Outcome（执行后补）

- 实际发送版本：待回填
- 模型结果：待回填
- 返修轮次：待回填
- 证据 / verdict：待回填
- 下次只保留什么：待回填

## Final Prompt

分析 `model_server/model_server/data/model_config.h` 中 `ModelInputConfig` 的 slot 配置结构。当前这里平铺了 `slot_idx_map`、`remap_slot_map`、`seq_slot_idx_map`、`rehash_bucket_map`、`hash_bucket_map`、`ctx_slot_set`、`special_handle`、`slot_mapping`、`model_slot_opt` 等多类状态，看起来包含了不同阶段积累下来的 slot 配置、映射和处理数据。

这轮希望基于真实代码重新判断 `ModelInputConfig` 应该承担什么责任，以及这些字段中哪些仍有独立存在价值，哪些已经是重复表达、历史兼容或可以自然收敛的数据。`model_slot_opt` 有后续优先承载数据的演进意图，但不要预设它已经是最终 canonical representation；需要由真实的配置来源、生产者、消费者和生命周期证明。

重点关注每类状态究竟代表原始配置、派生索引、运行时辅助数据还是跨 slot / model-level metadata，以及新旧结构是否在表达同一个事实。可以删除、合并或迁移的判断必须有 repo evidence；同样，不要因为都与 slot 有关就机械放进新的 wrapper struct。仍被真实链路依赖、承担不同生命周期或兼容责任的数据应保留其边界。

结合 `load_slot_json*`、相关解析逻辑和下游消费链路形成完整判断。最终给出当前责任模型、字段去留/迁移/聚合结论、推荐的目标结构和一个语义不漂移的渐进收敛方向；无法从代码证明的部分明确保留为 unknown。