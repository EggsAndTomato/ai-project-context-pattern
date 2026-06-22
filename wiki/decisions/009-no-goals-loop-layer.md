# ADR-009：不采纳 goals/ 工作循环层（维持 KB 模式 v1.3 现状）

> 日期：2026-06-22  状态：已采纳

## 背景
评估是否为 KB 模式新增 `goals/` 类目 + 配套《工作循环模式》文档，让 agent 能基于持久化 goal 自主推进 sizable 工作块。评估素材为根级两份方案：`ai-project-context-pattern-更改方案.md`、`work-loop-pattern-起草方案.md`。

讨论中考虑过多种形态：goals 入 wiki 第 5 目录、goals 独立根级操作层、配套 loop 文档、KB 零改的薄集成指南等。逐步收敛的关键发现：

1. **执行机制大面积重复 superpowers**：goal 文件+可验证清单 ≈ `writing-plans` 的 plan 文档；每项派全新子代理 ≈ `subagent-driven-development`；实跑验证才勾选 ≈ TDD + 期望输出 + **两阶段 review（spec 合规 → 代码质量）**——superpowers 的 review 比设计的勾选还强。
2. **loop 真正独有的只有三点**：跨 session 续跑指针、wiki 沉淀桥、接入 triage。其中"沉淀"本就是 KB 方法论 Ingest 操作的职责；"续跑指针"是 superpowers 自身缺口，不归方法论。
3. **KB 方法论文档已工具无关**：Ingest（"定了个决策→沉淀"）+ log 触发（"结构变更→log"）按**知识事件**触发，不依赖具体执行工具；若绑定 superpowers 反而伤害可移植性。

## 选择
**不采纳 goals/loop 层。维持 KB 模式 v1.3 原样：不改 `ai-project-context-pattern.md`、不新增固定目录、不改 AGENTS.md 模板、不加任何 superpowers 相关规则。** superpowers（或任何 plan→执行工作流）与现有 wiki 范式免费组合，无需桥接。

## 理由
1. **避免重造**：执行归成熟工具（superpowers）；重造一个更弱的平行实现没道理。
2. **保持工具无关**：方法论文档耦合特定工具（superpowers）会伤害可移植性，对一个面向"各式各样场景"的 OSS 方法论是倒退。现有 Ingest 已工具无关。
3. **无硬冲突**：superpowers 产物放 `docs/superpowers/`（wiki 之外），不碰 AGENTS.md，不违反固定 4 目录——两套范式正交，无需协调。
4. **角色分工清晰**：superpowers = 怎么造出 X（per-feature、偏过程性、相对临时）；wiki = 项目是什么 & 为什么（持久、复利）。实现工作产出持久知识时，按现有 Ingest 手动沉淀即可。

## 后果
- KB 模式 v1.3 维持不变。
- 沉淀仍由现有 Ingest 操作覆盖：feature 工作产出持久知识（新决策 / 架构变更 / 值得记的坑）时，需手动 Ingest 进 wiki + 更新 index + log（同今天）。
- 已知的非阻塞缺口（接受）：
  - superpowers 不自动沉淀 → 靠手动 Ingest，可接受；
  - 跨 session 续跑指针缺失 → superpowers 自身职责，不归方法论；
  - 现有 Ingest 例子偏"吸收/决策"事件，"完成实现工作"未显式点名 → 被"结构变更→log"隐式覆盖，暂不补。
- 未来若证据表明"实现工作常滑过 Ingest 触发"，再考虑在 KB 文档 Ingest 描述里加一个**工具无关**的触发例子（届时另起 ADR，且仅作措辞性修订）。

## 相关
- 固定目录集与"第 5 类产物"边界（评估曾考虑加 goals/ 为第 5 目录）：[ADR-004：扁平 + 4 固定子目录](004-flat-four-dirs-no-tree.md)
- index / AGENTS.md 区域权属（评估曾考虑加「当前 goal」指针区）：[ADR-002：index 永驻 AGENTS.md](002-index-in-agents-md.md)
- 评估素材（根级、非 wiki 产物）：`../../ai-project-context-pattern-更改方案.md`、`../../work-loop-pattern-起草方案.md`
