# [案例标题]

**标签**：Goal / Context / Evidence / Boundary / Immediate Task / Success / Stop / Review / Architecture / Refactor / Research / Wayfinder / Loop / Verification  
**目标模型**：ChatGPT / Codex / Claude Code / Fable  
**证据状态**：原文 / 摘录 / 重建 / 已验证

## Current Prompt

> 粘贴实际准备发送或已经发送的 Prompt。保留原貌，不先润色。

## Problem Analysis

- 已经做得好的地方
- 最影响结果的一处问题
- 哪些内容是必要合同，哪些只是重复过程控制
- 如果只改一处，改哪里最值

## Minimal Rewrite

> 尽量保持原表达。先删除无效脚手架，再只补最关键的 Task Contract 信息。

## Contract Changes

说明本轮改变了哪些合同：Goal / Outcome、Decision Context、Available Evidence、Constraints / Approval Boundary、Immediate Task、Success Criteria、Stop Rules。没有变化的维度不要为了完整而填写。

同时指出哪些执行决策重新交还给模型或 Harness，例如读取顺序、工具选择、推理步骤、循环次数或 review 路径。

## Why It Is Better

说明改写减少了模型的哪一部分猜测、冲突或决策成本，而不是只说“更清晰、更专业”。区分：

- 增加了必要信息；
- 删除了重复或矛盾信息；
- 把 execution script 改成 decision rule；
- 澄清了自治、审批、验证或停止边界。

## Transferable Principle

一句可迁移原则。未经多个真实任务验证时，标记为 candidate，不直接提升为仓库 principle。

## Outcome（执行后补）

- 实际发送版本：
- 模型结果：
- 返修轮次：
- 证据 / verdict：
- token / tool loops / latency（适用时）：
- 下次只保留什么：

## Final Prompt

Final Prompt 必须是页面最后一节，也是唯一可直接发送给目标模型的版本。

写作前使用 `Goal / Outcome → Decision Context → Available Evidence → Constraints / Approval Boundary → Immediate Task → Success Criteria → Stop Rules` 检查是否遗漏关键内容，但不要把这些名称机械写成最终 Prompt 的段落标题。

在这里写一份自然、连续、可直接复制的 Markdown。描述目的地与完成标准，不替模型编写不必要的执行脚本。只有真正 invariant 才使用绝对规则；搜索、工具、重试和继续调查优先写成由证据缺口驱动的 decision rule。

不得混入分析、比较说明、多个备选版本或“见上文”式引用。
