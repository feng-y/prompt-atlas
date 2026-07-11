---
type: source
id: src-2026-07-11-five-prompt-style-baselines
status: active
evidence_status: original
origin: ChatGPT project conversation
captured: 2026-07-11
immutable: true
used_by:
  - guides/five-prompt-style-baselines.md
---

# Five Prompt style baselines

> 本来源记录用户对五类 Prompt 学习方向及其统一成稿规则的明确判断。

## Provenance

- 原始位置 / URL：ChatGPT 项目会话，未公开链接
- 作者或会话：用户与 ChatGPT
- 获取方式：用户明确要求同步到 Prompt Atlas
- 许可或隐私边界：仅保留与 Prompt 训练方法有关的判断，不保存无关会话内容

## Content or excerpt

### 五类训练方向

- Anthropic / Alex Albert：先纠正离散需求表达，学习 Why、Boundary、Immediate Task。
- Matt Pocock：学习如何用少量强概念控制多轮行为。
- Simon Willison：加强事实、证据、推断和实验的表达。
- Lilian Weng：把单次 Prompt 提升到 Harness 和系统改进。
- Boris Cherny：在任务已经清晰且验证闭环稳定后，再学习 Loop 化。

### 统一成稿规则

五类方法共享同一个底层检查模型：

`Goal / Why → Decision Context → Control Boundary → Immediate Task → Observable Evidence`

人物或方法之间的差异，只改变 Prompt 中需要强化的信息重点和控制机制，不改变 Final Prompt 的表面模板。

Final Prompt 应自然嵌入这些信息，不应为了展示某种风格而机械出现 `Goal`、`Context`、`Boundary`、`Evidence` 或 `Loop` 等教学栏目。必要的领域概念，例如 `Fog`、`Frontier`、`PASS / RETRY / BLOCK`，可以在正文中直接使用。

## Processing notes

- 影响页面：`guides/five-prompt-style-baselines.md`、`index.md`
- 证据边界：这些是 Prompt Atlas 当前的训练归纳，不代表五位作者或团队的完整方法论，也不应表述为其原话
- 待补：后续可分别注册官方文档、Skill、文章或演讲作为外部 source
- log entry：`[2026-07-11] ingest | Five Prompt style baselines`
