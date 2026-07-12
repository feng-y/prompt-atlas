---
type: source
id: src-2026-07-12-human-rewrite-before-repo-compilation
status: active
evidence_status: original
origin: Prompt Studio conversation
captured: 2026-07-12
immutable: true
used_by:
  - principles/transferable-principles.md
  - summaries/delegation-readiness-roadmap.md
---

# Human rewrite before repo compilation

> 记录 Prompt Atlas 当前训练边界：先达到人能够自然写出的高质量改写，不提前把 repo-aware 编译当成主要价值。

## Provenance

- 原始位置 / URL：Prompt Studio 当前会话
- 作者或会话：用户关于 Harness 分析 Prompt 的连续纠偏
- 获取方式：原始对话摘录
- 许可或隐私边界：用户明确要求同步到 Prompt Atlas

## Content or excerpt

用户确认：

> 这个经验也同步到 prompt-atlas。先达成人改写的高度，编译的价值不高，因为实际的 repo 可能不是你理解的。

该判断来自前一轮讨论：一个完整的 Control Prompt 可能包含 repo grounding、任务展开、证据路径和停止条件，但这些内容若不是由真实 repo 内的 Agent 读取事实后形成，很容易建立在错误的 repo 理解上。

当前训练重点因此收敛为：

- 人先能把目标、当前状态、关键边界、关注点和期望结果表达清楚；
- AI 的改写优先保持在人可以理解、学习并逐步自行写出的高度；
- 不因为理论上可以“编译”出更完整的 Control Prompt，就提前加入未经 repo 验证的文件入口、架构判断、证据路线或执行机制；
- repo-aware 编译只有在执行 Agent 实际进入 repo、读取当前事实后才可能产生稳定价值。

## Processing notes

- 影响了哪些 wiki 页面：`principles/transferable-principles.md`、`summaries/delegation-readiness-roadmap.md`、`index.md`
- 仍待核验的部分：需要后续真实案例验证“人类可写改写”与“repo 内编译”之间的交接点
- log entry：2026-07-12 ingest | Human rewrite before repo compilation
