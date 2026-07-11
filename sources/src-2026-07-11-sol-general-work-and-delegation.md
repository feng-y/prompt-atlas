---
type: source
id: src-2026-07-11-sol-general-work-and-delegation
status: active
evidence_status: user-provided-excerpt
origin: X article pasted by user
captured: 2026-07-11
immutable: true
used_by:
  - ../summaries/delegation-readiness-roadmap.md
---

# 5.6 Sol is underhyped for general work

> 用户提供的 Jason（@jxnlco）文章摘录。它被纳入 Prompt Atlas，不是作为模型排行榜证据，而是作为“Prompt 之后如何进入真实工作委托”的方向性来源。

## Provenance

- 原始位置 / URL：用户未提供可核验 URL；原文显示发布于 X，标题为 `5.6 Sol is underhyped for general work`
- 作者或会话：Jason / @jxnlco；由用户在 2026-07-11 会话中完整粘贴
- 获取方式：用户提供原文
- 许可或隐私边界：仅用于本仓库内部学习与综合；外部指标、产品可用性和模型命名仍需单独核验

## Content or excerpt

> Real work is not just a repo of markdown files and a git repo.
>
> High level, high leverage work, whether you're a developer or not, spans email, Slack, multiple documents, multiple browser tabs, and native software.
>
> It's no longer just about finding the context, but actually working on things for long periods of time autonomously, delegating, learning to delegate work, and work across your entire computer.

文章以内部研究任务为例，描述 Sol 检查研究分支、创建 Luna 配置、启动训练任务并持续观察运行；作者同时强调，这不是模型从零发明训练方案，已有配置和研究路径已经存在，人类主要提供正确权限。

文章随后把模型家族和计算模式区分为：

- Sol：旗舰模型，面向更复杂和长时任务；
- Terra：日常工作；
- Luna：快速、低成本、高吞吐；
- Ultra：通过更多 sub-agents 和计算换取更快、更强的结果。

文章认为，真实工作能力依赖两类执行表面：

- Plugins：连接 Slack、Google Drive、Microsoft 365 等结构化工作上下文；
- Computer Use：处理没有干净 API 的浏览器、本地应用和原生软件步骤。

文章给出的核心判断是：

> A good answer is not enough. The job has to get done.

其推荐的试用方式是：连接已有工作插件，让模型先说明它理解了哪些项目、当前重点、仍缺什么上下文以及下一步建议，再交给它一个真实任务推进。

## Processing notes

- 影响了哪些 wiki 页面：`summaries/delegation-readiness-roadmap.md`、`index.md`、`maps/prompt-atlas.md`
- 仍待核验的部分：文章中的模型指标、产品权限、Ultra 可用范围、SEC-Bench Pro / DeepSWE / Artificial Analysis 数据及“Sol 训练 Luna”的公开出处
- log entry：`## [2026-07-11] ingest | Sol general work and Delegation Readiness`
