# Contributing

Prompt Atlas 的单位不是“一个好 Prompt”，而是一条可学习的变化链。

新增案例时：

1. 使用真实工作 Prompt，保留 Current Prompt 原貌。
2. 先指出已经做得好的地方，再找最高杠杆问题。
3. 必须提供 Minimal Rewrite，并在页面末尾提供唯一的 Final Prompt；分析稿不能替代可直接发送版本。
4. `Goal / Decision Context / Control Boundary / Immediate Task / Observable Evidence` 只用于检查内容完整性，不应默认成为 Final Prompt 的显式标题。
5. Final Prompt 应将必要信息自然嵌入 Markdown 段落；只有任务本身需要逐项执行、正式交接或逐项返回时才使用标题和列表。
6. 不伪造历史原文。无法确认时标记为摘录或重建。
7. 尽量补 Outcome，让原则接受真实任务结果检验。
8. 一个案例只选择一个主归档方向，其他能力写入标签。
9. 没有跨案例证据前，不急于抽象成 pattern 或 skill。

Review 时重点检查：

- 改写是否真的改善 Decision Context，而不只是变长
- 边界是否给模型留下必要判断空间
- Immediate Task 是否唯一
- Success 是否可由外部证据判断
- Final Prompt 是否位于最后，且没有混入分析或多个候选版本
- Final Prompt 是否自然、完整、可直接复制，而不是 Foundation 字段的机械拼接
- 原则是否能迁移，而不是复述当前案例
