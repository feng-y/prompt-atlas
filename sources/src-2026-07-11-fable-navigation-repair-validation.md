---
type: source
id: src-2026-07-11-fable-navigation-repair-validation
status: active
evidence_status: original
origin: ChatGPT project conversation
captured: 2026-07-11
immutable: true
used_by:
  - prompt-pairs/11-loop/002-single-target-navigation-repair.md
  - prompt-pairs/11-loop/003-business-target-navigation-queue.md
  - prompt-pairs/12-verification/002-harness-change-value-validation.md
---

# Fable repo navigation, repair and value validation

> 本来源记录一组围绕 DaVinci repo 感知能力的连续 Prompt：先以真实业务目标探测导航行为，再修复高价值 Harness 缺口，最后用独立目标验证正向价值与负向影响。

## Provenance

- 原始位置 / URL：ChatGPT 项目会话，未公开链接
- 作者或会话：用户与 ChatGPT
- 获取方式：用户明确要求将本轮形成的高价值 Prompt 同步到 Prompt Atlas
- 许可或隐私边界：只保存 Prompt 设计与抽象工作流；不复制业务导航文件中的完整内部代码与配置细节

## Content or excerpt

用户最初给出的观察目标：

> 让 Fable 从 `CLAUDE.md` 进入 FeatureTable 需求。
>
> 观察它：
> - 第一个 anchor 找到什么；
> - 是否进入正确架构边界；
> - unknown 路由到哪里；
> - 是否找到 replay gate；
> - 在哪里仍需要人工纠正。

随后补充了三个关键要求：

> 还少了一个修复高价值的执行逻辑。

> 先读取业务目标导航的文件，然后逐个分析；FeatureTable 已经处理，先处理其他目标；Prompt 不要过长。

> 修改完成后，需要运行一些测试，验证修改的价值，以及是否有负向价值。

由此形成三层使用方式：

1. 单目标 probe：观察导航、边界、unknown routing、verification 与人工纠正点。
2. 多目标 queue：读取业务目标导航文件，逐个选择未处理目标推进。
3. Holdout validation：用未参与修改过程的目标验证正向收益、负向回归与跨目标价值。

## Processing notes

- 影响页面：两个 Loop Prompt Pair、一个 Verification Prompt Pair、`index.md`、`log.md`
- 未提升：尚未形成稳定 Harness principle；需等待真实运行结果和跨目标重复验证
- log entry：`[2026-07-11] ingest | Fable navigation repair and value validation`
