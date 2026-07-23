# Ticket Frontier：从离散触发转向依赖驱动的连续 loop

**标签**：Loop / Boundary / Success / Stop / Verification  
**目标模型**：Fable / Claude Code / Codex  
**证据状态**：原文 + 对照改写；完整执行 Outcome 待回填  
**来源**：[最近工程 Prompt：自治空间、语义漂移与连续 ticket loop](../../sources/src-2026-07-23-recent-prompt-contract-lessons.md)

## Current Prompt

> 05–09 tickets 已经落盘并有明确依赖图。这里应是一个个 loop 持续推进。

## Improvement

当前任务已经完成拆票和依赖建模，真正的问题不再是 planning，而是 progression authority：模型是否可以在一个 ticket 完成后依据 tracker 和依赖图自动选择新的 frontier，而不是每轮都等待人工再次触发。

改版不需要规定一个固定 workflow，只需要明确三个控制点：每次只推进一个已解锁 ticket；完成必须由该 ticket 自己的 evidence 和 success condition 证明；关闭后重新计算 frontier，并在没有 human-only blocker 时继续。这样既避免一次性横跨多个 ticket，也避免把人工确认变成无意义的 progression gate。

## Minimal Rewrite

> 05–09 tickets 和依赖图已经是当前执行依据，不重新拆票，也不在每个 ticket 之间等待人工触发。每次只选择一个未阻塞 frontier，完成该 ticket 的修改、验证和 evidence 回写；只有满足其 success condition 后才关闭，并重新计算依赖图进入下一个 frontier。
>
> 无真实 human-only blocker 时持续推进；如果 repo evidence 否定 ticket 的前提，先更新该 ticket 的判断和 route，而不是机械执行原方案。不要把多个 ticket 合并成一次大范围整理。

## Why It Is Better

它把“持续工作”定义成依赖图上的状态推进，而不是无限循环或固定步骤。progression 由本地事实决定，human gate 只保留给真正需要人的 policy/ownership 决策。

## Transferable Principle

**Candidate**：已有 ticket graph 时，连续 agent loop 的关键不是增加 workflow，而是显式授权 `frontier → evidence-backed close → recompute frontier`；人工只在不可由现有证据解决的决策点介入。

## Outcome（执行后补）

- 实际发送版本：待回填
- 模型结果：待回填
- 返修轮次：待回填
- 证据 / verdict：待回填
- 下次只保留什么：待回填

## Final Prompt

当前 05–09 tickets 已经落盘，依赖关系和各自交付目标也已经确定。这一轮不重新做 ticket breakdown，也不需要在每完成一个 ticket 后等待人工再次触发；本地 tracker 和依赖图就是当前 progression authority。

从当前未阻塞 frontier 中一次选择一个 ticket 推进。每个 ticket 都应在自己的目标和边界内完成必要修改、验证与 evidence 回写，只有其 success condition 被实际证据满足后才关闭。关闭后重新计算依赖图并继续新的 frontier。初始依赖为 05 → {06, 07} → 08 → 09；06 和 07 在 05 完成后虽然都可以解锁，仍应分别形成独立、可验证的 loop，避免把多个 authority surface 的修改混成一个不可归因的大 diff。

不要机械执行 ticket 中已经被 repo evidence 否定的假设；如果新的事实改变了当前 ticket 的前提，应先修正该 ticket 的判断、范围或 route，再继续。也不要把 05–09 合并成一次总体清理，或借机扩展到无关文档和结构优化。

在没有真实 human-only blocker 时持续推进。只有出现无法通过 repo evidence 解决、确实需要人决定 policy、ownership 或 go/no-go 的问题时才暂停。最终停止条件是 09 完成并通过 owner-graph verification，或存在已经明确记录、无法自行消解的人类决策阻塞。