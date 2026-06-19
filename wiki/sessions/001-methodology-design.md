# SESSION-001：方法论设计会话（从 PD 模式演进到知识库式上下文模式）

> 日期：2026-06-19  归档于：2026-06-19

## 主题
为"用 AI 做 vibe coding 的个人 / 小团队"设计一套项目上下文组织方法论，并定稿。

## 关键决策（均已有 ADR）
- 放弃"大而全设计文档"，先做 PD（渐进式披露）分层方案，后演进为"知识库式"（增量沉淀 + 持续维护）。
- 经 A/B 测试对比两种方案，最终**只保留知识库式**（`ai-project-context-pattern.md`），删除 PD 版。
- index 永驻 AGENTS.md（ADR-002）；CRITICAL + 工具动作级规则 + 必需 Lint（ADR-003）；扁平 4 固定子目录（ADR-004）；不设 raw（ADR-005）；会话按需归档（ADR-006）。

## 结论与产出
- 方法论定稿 `ai-project-context-pattern.md`（v1.1）。
- 删除冗余：原 PD 文档、`llm-wiki.md`（精神已吸收）。
- 按本方法论为项目自身建知识库（本次产出）。

## 下一步
- 拟用 opencode slash command（类 `/init`）做应用形态，便于新项目一键 bootstrap（待定）。
- 在真实项目试用，回收反馈迭代方法论与模板。
