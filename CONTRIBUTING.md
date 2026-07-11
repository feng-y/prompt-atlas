# Contributing

Prompt Atlas 的单位不是“一个好 Prompt”，而是一条可学习的变化链。

新增案例时：

1. 使用真实工作 Prompt，保留 Current Prompt 原貌。
2. 先指出已经做得好的地方，再找最高杠杆问题。
3. 必须提供 Minimal Rewrite；Expert Lens 用于展示表达上限；Final Prompt 才是可直接发送的最终产物。
4. `Goal / Decision Context / Control Boundary / Immediate Task / Observable Evidence` 只用于分析完整性，不应默认成为 Final Prompt 的显式标题。
5. Final Prompt 应将必要信息自然嵌入 Markdown 段落；只有真正需要逐项执行或返回时才使用列表。
6. Final Prompt 放在案例尾部，读者不需要重新拼装 Minimal Rewrite 与 Expert Lens。
7. 不伪造历史原文。无法确认时标记为摘录或重建。
8. 尽量补 Outcome，让原则接受真实任务结果检验。
9. 一个案例只选择一个主归档方向，其他能力写入标签。
10. 没有跨案例证据前，不急于抽象成 pattern 或 skill。

Review 时重点检查：

- 改写是否真的改善 Decision Context，而不只是变长
- 边界是否给模型留下必要判断空间
- Immediate Task 是否唯一
- Success 是否可由外部证据判断
- Final Prompt 是否自然、完整、可直接复制，而不是教学标签的拼接
- 原则是否能迁移，而不是复述当前案例
