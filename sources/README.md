# Sources

这里保存 Prompt Atlas 的证据来源：原始 Prompt、聊天摘录、文章、真实执行结果、外部链接或其不可变快照。

Sources 不是 wiki 页面。Agent 可以读取、引用和为它们建立链接，但不得改写原始内容或把总结覆盖到来源中。需要补充说明时，创建新的 source record 或在 wiki 页面中解释。

## Source record

每个来源使用 [source-record 模板](../templates/source-record.md)：

- 记录来源、获取日期、证据状态与可追溯定位；
- 内容不便提交时，保留 URL、摘要范围和必要摘录；
- 一个原始来源可更新多个 Prompt Pair / principle / case study；
- 处理来源后，将实际变更写入根目录 [log.md](../log.md)。

## 与 Inbox 的区别

`inbox/` 是待处理输入队列，可以被整理、移动或丢弃；`sources/` 是已纳入判断依据的证据记录，应保持可追溯。