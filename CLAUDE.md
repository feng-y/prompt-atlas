# Claude Code Entry

Prompt Atlas 的运行规则由 [AGENTS.md](AGENTS.md) 统一定义。

开始任何任务前，依次阅读：

1. [README.md](README.md)
2. [AGENTS.md](AGENTS.md)
3. [index.md](index.md)
4. 目标目录的 README、模板与相关案例

## Prompt Pair delivery rule

当创建或更新 `prompt-pairs/` 中的案例时，使用 [Prompt Pair 模板](templates/prompt-pair.md) 与 [Prompt Foundation Structure](guides/prompt-foundation-structure.md)。

第一阶段的训练目标不是写得高级，而是让模型进入正确的问题空间。写作前使用以下维度检查内容是否完整：

- Goal / Why
- Decision Context
- Control Boundary
- Immediate Task
- Observable Evidence

这些是内部检查维度，不是 Final Prompt 的默认段落标题。Final Prompt 必须位于页面末尾，并将必要信息自然嵌入 Markdown 表达中。只有任务本身需要正式合同、多人交接或逐项返回时，才因为实际消费价值使用标题或列表。

Final Prompt 必须是唯一完整、可直接发送的版本：综合分析中有效信息，但不包含分析过程、解释、多个候选版本或“见上文”式引用。不得停在 Minimal Rewrite，也不得把 `Goal / Context / Boundary / Task / Done` 机械拼接成表单。

本仓库训练 Prompt 表达并沉淀经过验证的知识；不要把会话过程全部永久记忆化。
