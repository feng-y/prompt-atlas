# 架构 Review：按原始意图判断，而不是做普通 Code Review

**标签**：Review / Architecture / Refactor  
**目标模型**：Codex / GPT-5.6  
**证据状态**：原文；ModelCurator 重构已执行，Review 结果待回填。

## Current Prompt

> Review the completed ModelCurator refactor from the perspective of legacy module evolution.
>
> Do not perform a normal code review.
>
> Instead, judge whether this change actually improves the module as a long-lived maintainable component.
>
> Review from these perspectives:
>
> - Has the real responsibility of ModelCurator become clearer?
> - Are primary, supporting, lifecycle, observer, integration and optimization responsibilities better separated?
> - Has data ownership become more coherent? Are unnecessary fields removed, encapsulated or relocated appropriately?
> - Does the public surface better match what consumers actually need, while exposing fewer internal details?
> - Is the dependency direction clearer and easier to evolve?
> - Did the refactor reduce accidental complexity instead of merely moving it?
> - Are there remaining structural smells such as shallow modules, leaked seams, poor locality, change propagation, duplicated knowledge or dependency disorder?
> - Does the new structure improve AI operability: canonical entry, locality, ownership clarity, navigation and verification?
> - Are there important unknowns or residual technical debt that should be addressed in future iterations?
>
> Do not focus on naming, formatting or small implementation details.
>
> Conclude with overall assessment, major improvements, remaining architectural gaps, the five highest-priority next improvements, and confidence with supporting evidence.

## Problem Analysis

这份 Prompt 已经明确阻止模型回落到命名、格式和局部实现细节，并将 Review 对象切换为存量模块演进结果。

最需要补强的是判断基准：模型仍可能主要比较新旧实现，而没有回到本轮重构的原始目标。这样容易得到“比之前更好”的相对结论，却无法回答责任、边界、数据 ownership、依赖和 AI-operability 是否真的达到预期。

只改一处时，最有价值的是明确：**Review against the original intent, not against the previous implementation or the diff.**

## Minimal Rewrite

> Review the completed `ModelCurator` refactor as an architecture evolution result, not as a normal code diff. Judge it against the original intent: whether responsibility, data ownership, public boundary, dependency direction, locality, verification seams and AI operability genuinely improved. Use code, consumers and verification evidence to identify real gains, moved complexity, remaining structural gaps and the highest-value next actions. Ignore naming, formatting and low-impact implementation details.

## Why It Is Better

它先锁定了 Review Object：被评估的是“模块架构演进是否成立”，而不是“这份代码有没有普通问题”。

随后把判断基准从旧实现和 diff 切换到原始意图，减少模型对历史结构的锚定。责任、边界、数据 ownership、依赖方向、locality、验证 seam 和 AI-operability 都需要代码及消费者证据支撑，避免输出一份泛化的架构优缺点清单。

## Transferable Principle

先定义 Review Object，再定义 Review Criteria；架构 Review 应对原始意图和可观察改善负责，而不是只对旧实现或 diff 负责。

## Outcome（执行后补）

- 实际发送版本：待回填
- 模型结果：待回填
- 返修轮次：待回填
- 证据 / verdict：待回填
- 下次只保留什么：待回填

## Final Prompt

Review the completed `ModelCurator` refactor as an architecture evolution result, not as a normal code review.

Judge the implementation against the original intent, not merely against the previous implementation or the diff. Determine whether the change genuinely made `ModelCurator` easier to understand, maintain, evolve and verify.

Focus on whether:

- its core responsibility and supporting responsibilities are clearer;
- data ownership and lifecycle are more coherent;
- unnecessary fields or residual state were removed, encapsulated or relocated appropriately;
- the public surface reflects what real consumers need while exposing fewer internal details;
- dependency direction, locality and canonical entry points are clearer;
- the new abstractions concentrate complexity instead of moving it or creating shallow modules;
- observer, integration, compatibility and optimization concerns no longer obscure or control the core behavior;
- test and replay seams genuinely cover the changed paths;
- a representative future change would require less code reading, fewer modification points and less implicit knowledge.

Use concrete code, consumer and verification evidence. Identify important unknowns and residual debt, but do not focus on naming, formatting or low-impact implementation details.

Conclude with:

1. overall verdict: achieved, partially achieved or not achieved;
2. the strongest evidence of real architectural improvement;
3. the most important gaps or cases where complexity was only moved;
4. the five highest-value next improvements, ordered by impact;
5. confidence level and the evidence or unknowns behind it.