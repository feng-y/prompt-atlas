---
type: source
id: src-2026-07-18-behavior-preserving-refactor-review
status: active
evidence_status: original
origin: ChatGPT conversation
captured: 2026-07-18
immutable: true
used_by:
  - prompt-pairs/06-review/003-behavior-preserving-refactor-review.md
---

# Behavior-preserving refactor review Prompt 对照

> 用户提供了一条真实的结构迁移 Review Prompt，并要求分析其与改写版相比的缺陷，核心训练点是：如何把脑中的验收模型显式化，而不是只给出“禁止业务逻辑漂移”的结论性约束。

## Provenance

- 原始位置 / URL：Prompt Studio 当前会话，2026-07-18
- 作者或会话：用户与 ChatGPT 的 Prompt Atlas 训练对话
- 获取方式：用户直接提供原始 Prompt，并要求对比分析和同步到 Prompt Atlas
- 许可或隐私边界：仅记录本次 Prompt 与抽象化的改写分析；不记录未提供的代码、仓库实现细节或内部执行结果

## Content or excerpt

用户原始 Prompt：

> 当前分支是把 galaxy 请求从 Model 的派生类上移到 Mode 里面，并对所有的派生完成的迁移，本次修改结构调整，禁止导致业务逻辑漂移（部分 log/metrics/latency 微小变更允许）， 同时检查是否有其他扩大的修改 ，最后输出 review 结果，哪些逻辑漂移， 是否存在逾期未的顺手优化

对比讨论中确认的主要缺口：

- Goal 与 Boundary 已经明确，但“业务逻辑漂移”的判断依据仍隐含在用户脑中。
- “允许 log / metrics / latency 微小变化”没有进一步区分业务语义漂移与 observability drift。
- “检查扩大的修改”缺少 expected diff boundary，模型需要自己猜什么属于 scope creep。
- “所有派生完成迁移”被表述成已知事实，而不是需要 Review 验证的目标状态。
- 缺少最终 verdict：当前分支能否被视为一次基本等价的结构迁移。

## Processing notes

- 影响了哪些 wiki 页面：prompt-pairs/06-review/003-behavior-preserving-refactor-review.md；index.md；log.md
- 仍待核验的部分：Final Prompt 尚未在真实分支 Review 中执行，Outcome 与实际 verdict 待回填
- log entry：2026-07-18 ingest | Behavior-preserving refactor review
