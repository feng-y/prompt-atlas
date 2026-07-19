---
type: source
id: src-2026-07-19-recent-harness-review-lessons
status: active
evidence_status: original
origin: Prompt Studio conversations, 2026-07-17 to 2026-07-19
captured: 2026-07-19
immutable: true
used_by:
  - prompt-pairs/06-review/004-structural-change-review-loop.md
  - prompt-pairs/12-verification/003-real-task-harness-smoke-test.md
---

# 最近三天：结构迁移 Review 与 Harness smoke test 经验

> 来源于最近三天围绕 DaVinci / Fable / Galaxy 真实任务的 Prompt 迭代，用于记录尚未完全经过多任务验证的工作经验。

## Provenance

- 原始位置 / URL：Prompt Studio 项目内 2026-07-17 至 2026-07-19 相关会话
- 作者或会话：用户与 ChatGPT 的 Prompt 设计、Review 与 Harness 讨论
- 获取方式：当前会话及项目近期上下文整理
- 许可或隐私边界：仅保留可迁移的方法与抽象，不复制内部代码实现或敏感业务数据

## Content or excerpt

### 1. Behavior-preserving structural change 的 Review 顺序

大型结构调整的首要目标不是普通 code quality，而是证明核心业务语义保持等价。稳定的审查顺序逐渐收敛为：

1. 原始意图与允许变化边界；
2. Semantic Equivalence：调用条件、执行路径、参数与数据传递、状态和生命周期、默认行为、fallback、异常路径、最终业务结果；
3. Migration Completeness：漏迁、新旧路径并存、部分调用方仍走旧逻辑；
4. Scope Integrity：额外 cleanup、顺手优化、无关重构和 scope expansion；
5. Observability Impact：log / metrics / tracing / latency measurement 可以有合理实现变化，但必须判断是否改变统计口径、告警、SLA、性能判断或诊断能力；
6. General Risk：异常、安全、资源生命周期、并发和其他回归风险。

发现中高风险问题后，修复本身也成为新的 Diff，必须重新接受同样的 Review。停止条件不是“没有任何问题”，而是一轮完整 Review 没有发现新的中高风险。无法验证的部分不能推断为安全，应保留为 remaining risks / unknowns。

### 2. 真实任务作为 Fable / Harness smoke test

验证 Harness 自主推进能力时，不应在 Prompt 中预设 `Wayfinder → to-spec → to-tickets → execution` 固定 pipeline。更有效的 smoke test 是给出一个真实复杂任务，观察 Fable 是否能基于当前 repo 和 Harness 自主找到导航、研究、设计、执行和验证能力并推进。

Smoke test 本身不应成为修改 Harness 的理由；只有真实任务暴露出明确阻塞时，才把它作为 Harness 改进证据。人工停止点应保留给真正需要 human judgment 的 decision，而不是阶段切换。

### 3. Progression 应基于 current state，而不是固定 pipeline

复杂任务经常自然经历 Wayfinder、spec、tickets 和 execution，但长期稳定的控制模型更接近 `Current State → Next Capability`。任务可能已经具备 spec 或 tickets，也可能 Wayfinder 后可以直接执行，或者在真正的 human decision 上停止。

如果未来补充 progression 能力，应优先复用现有 routing / handoff / case state；若确有稳定缺口，也应是薄的 progression/router，而不是重新拥有 Wayfinder、spec、tickets 或 execution 的 workflow owner。

### 4. 统一抽象与真实领域差异分开处理

Galaxy split 任务暴露出一个可迁移判断：结构收敛不等于消除所有差异。抽象应消除 accidental differences 和重复责任；真实的请求语义、input 来源、batch 维度和 split 适用边界应进入 repo knowledge。

例如 `user only` 与 `user + item`、FeatureResult 依赖与非 FeatureResult、dense 与 sparse 等差异，应先基于调用方和代码现实分类，再判断哪些自然进入统一抽象，哪些需要额外适配，哪些因真实业务语义应保留。目标是明确统一规则和有原因的场景差异，而不是为了形式统一强行迁移。

## Processing notes

- 新增一个 Review Prompt Pair：结构迁移的 evidence-driven fix/review loop。
- 新增一个 Verification Prompt Pair：用真实复杂任务做 Harness smoke test，不预设 pipeline。
- Progression 与“统一抽象 vs 真实差异”暂保留为 candidate knowledge，不直接提升为全局 principle 或 Harness contract。
- 后续需要用更多真实任务验证：固定 Review 顺序是否跨模块成立；Fable 是否能在不显式指定路径时稳定自主推进；progression 是否真的需要独立 skill。
