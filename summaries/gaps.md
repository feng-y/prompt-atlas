# 待补内容与采集优先级

## P0：补齐证据链

- 回填 Fable repo L3 对齐的完整 Current Prompt 与最终采用版本。
- 回填 FeatureTable loop 的完整最终 Prompt、实际执行结果和 replay verdict。
- 找回 Wayfinder warmup prompt 的最终短版，区分“建议稿”与“实际发送稿”。
- 为依据多轮讨论重建的案例补 conversation link 或原文摘录。

## P1：补齐能力方向

| 方向 | 需要的真实案例 | 合格标准 |
| --- | --- | --- |
| Background | 从“堆资料”改成“说明为什么现在做”的 Prompt | 能指出背景中真正改变决策的 1–2 项 |
| Success | 从模糊完成改成 evidence contract | 有明确证据、verdict 与失败路由 |
| Architecture | 从模块罗列改成边界/依赖判断 | 有 repo anchor 和最终架构判断 |
| Refactor | 从机械替换改成语义迁移 | 有 ownership、residual 与 no-diff 约束 |
| Review | SPEC compliance 与 code quality 分离 | 有真实 review 输出和返修结果 |

## P2：增加非软件工程样本

当前 Atlas 过度集中在 Agent/Harness/大型 repo。后续至少需要：

- 一组设备购买或方案比较 Prompt Pair
- 一组家庭教育行动计划 Prompt Pair
- 一组信息检索与事实核验 Prompt Pair

目标不是扩大主题，而是检验 Decision Context 原则能否跨域迁移。

## 尚未建立的资产

- `patterns/`：至少 3 个案例重复验证后再晋升
- `loops/`：收录已运行且有 stop/evidence 的 loop，而非概念说明
- `harness/`：记录 Prompt 与 repo-owned context/guardrail/verification 的边界
- `case-studies/`：保留一次任务从 Current Prompt 到真实结果的完整链路
- `summaries/progress.md`：周期性回顾表达能力的变化，不按案例数量计进步
