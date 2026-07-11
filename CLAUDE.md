# Claude Code Entry

Prompt Atlas 的运行规则由 [AGENTS.md](AGENTS.md) 统一定义。

开始任何任务前，依次阅读：

1. [README.md](README.md)
2. [AGENTS.md](AGENTS.md)
3. [index.md](index.md)
4. 目标目录的 README、模板与相关案例

## Prompt Pair delivery rule

当创建或更新 `prompt-pairs/` 中的案例时，使用 [Prompt Pair 模板](templates/prompt-pair.md)。

页面前半部分用于学习：Current Prompt、Problem Analysis、Minimal Rewrite、Why It Is Better、Transferable Principle 与 Outcome。页面最后必须是 `## Final Prompt`：

- 它是唯一完整、可直接发送给目标模型的版本；
- 必须综合分析中的有效信息；
- 不包含分析过程、解释、多个候选版本或“见上文”式引用；
- 不得停在 Minimal Rewrite 或中间分析。

本仓库训练 Prompt 表达并沉淀经过验证的知识；不要把会话过程全部永久记忆化。
