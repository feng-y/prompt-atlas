# Prompt Atlas

从真实工作 Prompt 中训练表达能力：把“任务描述”提升为清晰、自然、可验证的 **Decision Context**。

本仓库不是 Prompt 模板合集，也不追求复杂的 Prompt Engineering 技巧。它记录真实 Prompt 的演化过程：

> Current Prompt → Problem Analysis → Minimal Rewrite → Expert Lens → Transferable Principle

## 训练目标

形成一种稳定的 Prompt 风格：

- 信息密度高，但不冗长
- 先建立 Why / Background / Boundary，再给 Immediate Task
- 提供足够控制，但不过度规定模型的过程
- 让 AI 作为 repo-aware 的共同设计者，而不是机械执行器
- 以可观察证据定义完成，而不是用“做完、优化好”代替验收

## 初稿索引

| 能力方向 | 已收录案例 | 状态 |
| --- | --- | --- |
| Task Context | Fable repo L3 对齐；Harness 三层审视 | 2 个初稿 |
| Boundary | 不 fork Wayfinder；保留模型判断空间 | 2 个初稿 |
| Immediate Task | Request 归一化定向 code-read | 1 个初稿 |
| Research | Blindspot skill 的条件触发 | 1 个初稿 |
| Success | 阶段输出如何被后续消费 | 1 个初稿 |
| Wayfinder | unknown routing + verification loop | 1 个初稿 |
| Loop | FeatureTable A/B/C bounded loop | 1 个初稿 |
| Verification | 以 replay 可观察边界拆 slice | 1 个初稿 |
| Review | 先反驳再判断方案 | 1 个初稿 |
| Background / Architecture / Refactor | 已在现有案例中交叉覆盖 | 待形成独立案例 |

入口：

- [Prompt Pair 案例](prompt-pairs/)
- [可迁移原则](principles/transferable-principles.md)
- [待补内容](summaries/gaps.md)
- [Prompt Pair 模板](templates/prompt-pair.md)
- [新增案例入口](inbox/README.md)

## 使用方式

1. 把准备发送给 ChatGPT、Codex、Claude Code 或 Fable 的真实 Prompt 放入 `inbox/`。
2. 先评 Prompt 本身，不直接完成任务。
3. 优先做 Minimal Rewrite：如果只改一处，改哪一处最值。
4. 再从专家视角给出更成熟的表达，并说明为什么变好。
5. 只有经过真实任务验证的规律，才晋升为 `principles/` 或后续 `patterns/`。

## v0.1 边界

现有案例优先覆盖 Fable / Claude Code、Wayfinder、unknown routing、repo harness、FeatureTable 迁移、request 归一化与 capture-replay。部分历史对话只保留了结论，没有完整的原始 Prompt 或最终改写，因此会明确标为“摘录”或“待补证据”，不会伪造 Prompt Pair。
