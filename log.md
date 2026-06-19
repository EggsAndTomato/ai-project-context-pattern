# log.md — ai-project-context-pattern 变更日志

> 结构 / 意图层面的"变了什么 + 为什么"。最新在上。琐碎代码修订走 git。

- 2026-06-20 — 新增 `wiki/decisions/007-log-trigger-split.md`：为本轮 log 触发规则拆分补 ADR，记录决策理由（ADR-007）。
- 2026-06-20 — 修订 CRITICAL 维护规则：拆分 index 触发与 log 触发——index 仅在 wiki 新增页面时追加；log 扩为"任何结构/意图层面变更（新建/删改/改名文件、根级文档修订、核心术语或决策调整）后"追加。修正原规则只覆盖新建文件、遗漏根级文件与修订的盲区（原规则与 log.md 自述 scope 冲突，且违背 ADR-003 精确性前提）。同步改 `AGENTS.md` 与方法论文档。
- 2026-06-19 — 新增 `README.md`（项目入口说明，根级、不入 wiki index）。
- 2026-06-19 — 按本方法论为项目自身建立知识库：新增 `AGENTS.md`（基础层）+ `wiki/`（architecture×1、decisions×6、sessions×1、bugs 空骨架）+ loose `wiki/ab-test-findings.md`。设计会话总结见 `wiki/sessions/001-methodology-design.md`。
- 2026-06-19 — 方法论定稿并改名 `ai-project-context-pattern.md`（前身 `ai-wiki-context-pattern.md`；更早源自一份 PD 分层文档与 `llm-wiki.md` 想法）。移除与他文档的对照附录（v1.1）；删除冗余的 PD 文档与 `llm-wiki.md`（精神已吸收）。
