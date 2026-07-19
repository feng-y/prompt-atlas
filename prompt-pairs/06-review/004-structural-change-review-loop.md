# 结构迁移 Review：语义等价优先，修复后重新审查完整 Diff

**标签**：Review / Refactor / Verification / Boundary / Loop  
**目标模型**：Fable / Codex / Claude Code  
**证据状态**：原文；来自大型结构调整 Review Prompt 的连续迭代，真实跨任务 Outcome 待回填。

## Current Prompt

> 重新审查实现：检查边界、异常、安全与回归。发现问题就给证据、修复、跑测试/Lint/类型检查，再复查 Diff。重复，直到一轮没有新的中高风险；无法验证的部分列为剩余风险。

## Improvement

原 Prompt 已经有清晰的 `Review → Fix → Verify → Re-review` 循环和停止条件，但它把通用代码风险放在了最前面，没有显式定义大型结构调整最重要的判断优先级：先证明核心业务语义等价，再确认迁移完整、修改未越界，最后才进入通用风险检查。

改版后还补上两个关键边界：observability 允许合理变化但不能默认忽略其语义影响；每次修复都会产生新的 Diff，因此修复后必须重新接受完整的等价性和 scope Review。

## Minimal Rewrite

> 重新审查当前实现，把它视为一次 behavior-preserving structural change。先基于修改前后的真实调用链验证核心业务语义是否等价，再检查迁移完整性、scope expansion 和 observability 影响，之后检查异常、安全与其他回归风险。发现中高风险问题就给出证据、修复并运行相关验证；每次修复后重新审查完整 Diff。重复，直到一轮完整 Review 没有新的中高风险。无法验证的部分明确保留为 remaining risks / unknowns。

## Why It Is Better

它没有增加更多机械步骤，而是纠正了 Review 的判断层级：结构迁移首先对 semantic equivalence 负责。Fix 也不再被视为 Review 之后的单向动作，而是重新进入同一 Review contract，避免“修复问题时制造新的漂移”。

## Transferable Principle

**Candidate**：Behavior-preserving structural change 应先验证 Semantic Equivalence，再检查 Migration Completeness、Scope Integrity 和 Observability Impact；任何 Fix 都应重新进入完整 Review，直到一轮无新增中高风险，未验证部分保留为 residual risk。

## Outcome（执行后补）

- 实际发送版本：待回填
- 模型结果：待回填
- 返修轮次：待回填
- 证据 / verdict：待回填
- 下次只保留什么：待回填

## Final Prompt

重新审查当前实现。本次修改属于结构调整，Review 的首要目标是确认它是否保持核心业务语义等价，而不是进行普通的代码质量检查。

先理解本次修改的原始目标和预期变化边界，再基于修改前后的真实代码、调用方和执行路径检查核心行为。重点确认调用条件、关键执行顺序、参数和数据传递、状态与生命周期、默认行为、fallback、异常路径以及最终业务结果是否发生非预期变化。不要仅根据代码看起来被等价搬迁来判断，应沿真实调用链和 consumer 验证行为是否保持一致。

检查迁移是否完整，包括遗漏的调用方或派生实现、新旧逻辑并存、部分路径仍走旧实现、条件或默认值在迁移过程中发生变化，以及本应统一收敛却仍残留的重复责任。

检查完整 Diff 是否保持在本次结构调整的目标边界内。识别额外 cleanup、顺手优化、无关重构或其他 scope expansion，并判断它们是否是完成本次修改所必需的。不要因为修改本身合理就忽略其超出原始目标所带来的额外风险。

log、metrics、tracing 和 latency measurement 等 observability 行为不要求机械保持实现一致，但需要检查其实际语义变化。明确区分纯观察实现差异与会影响统计口径、告警、SLA、性能判断或线上诊断能力的变化；后者应按实际风险处理，而不是默认视为允许漂移。

在完成上述等价性、迁移完整性和修改边界检查后，再检查异常处理、安全、资源生命周期、并发以及其他潜在回归风险。

发现中高风险问题时，给出具体代码、调用链或行为证据，直接完成必要修复，并运行当前 repo 可用且与修改相关的测试、Lint、类型检查及针对性验证。

每次修复后，将新增修改重新视为当前 Diff 的一部分，再次检查完整 Diff 和受影响调用链，确认修复解决了原问题，同时没有引入新的业务逻辑漂移、迁移缺口或范围扩大。

持续执行 Review → Evidence → Fix → Verify → Re-review，直到完整一轮审查没有发现新的中高风险问题。不要为了达到停止条件处理低价值问题或进行无关优化。

最终明确给出核心业务语义是否保持等价及主要证据、发现并修复的中高风险问题、迁移遗漏或新旧路径并存、observability 变化及影响、scope expansion、实际验证结果，以及因环境或证据不足仍无法确认的 remaining risks / unknowns。

最终 verdict 应回答当前修改是否有足够证据被认为是一次 behavior-preserving structural change。无法验证不等于已经安全，证据不足的部分必须显式保留为剩余风险。
