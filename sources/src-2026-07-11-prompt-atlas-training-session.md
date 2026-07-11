---
type: source
id: src-2026-07-11-prompt-atlas-training-session
status: active
evidence_status: original
origin: ChatGPT project conversation
captured: 2026-07-11
immutable: true
used_by:
  - guides/prompt-studio-training.md
---

# Prompt Atlas training-session source

> 本来源记录 2026-07-11 会话中关于 Prompt Atlas、Prompt Studio、训练方法、个人短板与参考风格的原始依据。

## Provenance

- 原始位置 / URL：ChatGPT 项目会话，未公开链接
- 作者或会话：用户与 ChatGPT
- 获取方式：用户明确要求同步本会话中与 Prompt Atlas 相关的内容
- 许可或隐私边界：仅保留可用于个人训练体系的摘要与用户明确表达；不保存无关私密内容

## Content or excerpt

### 当前目标

- 提高 Prompt 的质量与信息密度，引导模型更稳定地完成真实工作。
- 不以复杂 Prompt Engineering 技巧、固定模板或新增 Skill 为主要训练对象。
- 通过大量真实 Prompt Pair 进行仿写：原始表达、问题分析、最小改写、专家风格、可迁移原则。

### 当前短板

- Prompt 多为离散的需求型描述，信息不少但组织松散。
- 擅长说明“要做什么”，较少提前建立 Why、Decision Context、Boundary、Immediate Task 与可观察的 Success Criteria。
- 容易在同一轮持续追加需求，使研究、设计、实现、验证边界混合。
- 目标不是把 Prompt 写长，而是提高单位文字承载的决策信息。

### 推荐训练方式

- 优先使用真实工作 Prompt，不脱离实际场景练习。
- 初期以 Prompt Pair 仿写为主，先刷新旧表达习惯，再逐步进入盲写与独立 review。
- 每次只指出最值得改进的 1–3 个问题，避免教学负担过大。
- 如果 Prompt 已足够好，不为了润色而修改。

### 五类参考基线

- Anthropic / Alex Albert：Why、Boundary、Immediate Task；用决策背景替代离散任务列表。
- Matt Pocock：用少量强概念控制多轮行为，例如 Destination、Fog、Frontier、Spec、Review against Spec。
- Simon Willison：事实、证据、推断、假设与最小实验分离。
- Lilian Weng：从单次 Prompt 提升到 Harness、反馈回路和系统改进。
- Boris Cherny：在任务与验证已经清晰后，用 Goal、Loop、Subagent 与停止条件推进执行。

### 长期 Project 定位

Prompt Studio 的唯一目标是训练 Prompt 表达能力。用户提交真实 Prompt 后，默认先 review Prompt 本身，而不是直接完成任务；长期观察表达习惯是否从 Task List 转向 Decision Context。

## Processing notes

- 影响了哪些 wiki 页面：`guides/prompt-studio-training.md`、`index.md`、`maps/prompt-atlas.md`
- 仍待核验的部分：五类风格需要后续持续补充官方或原始出处；当前页面是训练导航，不是人物思想的完整归档
- log entry：`[2026-07-11] ingest | Prompt Studio training baseline`
