# 可迁移原则 v0.3

这些原则来自现有 Prompt Pair 的共同模式。它们不是必须套用的模板，而是写完 Prompt 后用于自检的观察角度。

## 1. 先构建 Decision Context，再描述 Task

至少让模型知道：为什么现在做、当前判断是什么、真正的困惑是什么、这一轮只需要完成什么。

## 2. 用“当前困惑”暴露决策点

背景不是资料堆积。最有价值的背景通常是：我已经确认了什么，我卡在哪个判断，哪个答案会改变方案。

## 3. 边界要同时给出替代路径

“不要 fork Wayfinder”之外，还要说明扩展应由 repo context/guardrail 承担；否则禁止项只会压缩模型空间，不会提高决策质量。

## 4. 允许挑战，但要求最终判断

“允许质疑我的三层划分”保留模型价值；“最终给出最高杠杆改进”防止答案停留在开放讨论。

## 5. 一轮只设一个 Immediate Task

研究、判断、实现、验证可以属于同一目标，但不要在同一轮隐式要求全部完成。明确本轮停在 code-read、SPEC、slice A 或 verdict。

## 6. 把完成条件写成可观察证据

优先使用 build、replay diff、field mapping、repo anchor、verdict 等可检查证据。避免“优化好”“完整支持”“一致性对齐完成”这类自证式完成条件。

## 7. Unknown 要被路由，不必被一次消灭

保留 slice-local fog；只有会改变 locked decision、scope 或 verification strategy 的 unknown 才升级给人。

## 8. Loop 不是“继续做”，而是状态机

一个可用 loop 至少说明：当前 slice、每轮动作、PASS/RETRY/BLOCK 条件、升级规则。没有 stop condition 的循环只是重复。

## 9. Verification 应反向决定切片

如果失败后无法通过证据归因，就说明 slice 太大或边界错误。按可观察语义拆分，通常比按文件或模块数量拆分更稳定。

## 10. 优先 Minimal Rewrite

训练目标不是让每个 Prompt 变长，而是找到最值得补的一处。成熟版本用来展示上限，Minimal Rewrite 才是日常表达能力的主要训练材料。

## 11. 组织思考，但隐藏模板

`Goal / Decision Context / Control Boundary / Immediate Task / Observable Evidence` 用于检查 Prompt 是否遗漏关键决策信息，不是固定的五段式写作模板。Final Prompt 应把这些信息自然嵌入上下文，让读者可以直接复制，而不是看到一组教学栏目。

## 12. 先达到人类可写的改写高度，再讨论 repo 编译

Prompt Alignment 当前首先训练人能够自然表达清楚的目标、状态、边界、关注点和期望结果。AI 的改写应当仍然是人可以理解、模仿并逐步自行写出的 Prompt，而不是直接生成一份只有 Agent 才会写的完整控制合同。

不要在尚未进入真实 repo 时，凭外部理解补写具体文件入口、架构事实、证据路线或执行机制。脱离 repo 现实的“编译”即使结构完整，也可能稳定地把任务引向错误问题空间。

Repo-aware 编译只有在执行 Agent 实际读取当前 repo、确认已有 Harness 与验证能力之后才有价值。它属于后续执行环境中的 grounding，而不是当前 Prompt 表达训练的默认产物。
