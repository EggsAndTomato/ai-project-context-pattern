# log.md — ai-project-context-pattern 变更日志

> 结构 / 意图层面的"变了什么 + 为什么"。最新在上。琐碎代码修订走 git。

- 2026-06-20 — 方法论文档加"产物语言跟随用户"规则（顶部 blockquote + 版本 v1.2→v1.3）：所有产物用用户使用的语言生成，文档是中文但产物语言跟随用户、不跟随文档。据此简化 README.en.md 提示词（去掉硬编码的"generate in English"），现在两份 README 提示词完全对称、最简，语言由文档统一规定。待实测验证。
- 2026-06-20 — 改回单一文档策略：删除 `ai-project-context-pattern.en.md`，仅保留中文版为唯一事实源；新增 `README.en.md`（英文 README）。依据：子代理实测"英文提示词 + 中文文档 + 明确要求英文输出"能可靠产出零中文泄漏的英文知识库，故无需维护两份方法论文档，改为"一份中文文档 + 两份 README（EN 提示词显式声明输出语言）"。README.md / README.en.md 互加语言切换链接。
- 2026-06-20 — 新增 `ai-project-context-pattern.en.md`：方法论文档英文版（v1.2 EN），中文权威版的翻译；中文为单一事实源，两版漂移时以中文为准。
- 2026-06-20 — 方法论文档第八节 step 1 补空项目分支：原"读代码库"默认有代码，空项目无码可读会卡壳；改为"若已有代码先读，空项目跳过读码，用占位值先搭骨架"。由子代理实测 bootstrap 提示词时发现。版本 v1.1→v1.2。
- 2026-06-20 — 精简 README「怎么用」：删掉重复文档第八节的 5 步说明，改为最小引导（指向文档 + "不清楚先问我"）。理由：提示词里重述 bootstrap 步骤等于第二份规格说明，违背单一事实源、易与文档漂移；空项目本就是文档 bootstrap 覆盖的场景。
- 2026-06-20 — 改写 README 顶部 tagline 与「是什么」：按 vibe coding 场景先行 + 口语化重述（与 GitHub description 定位一致），保留两层渐进式披露与反 RAG 复利要点。
- 2026-06-20 — 升级 README「怎么用」：新增可复制即用的初始提示词（含文档 GitHub raw 链接），新项目用户无需自己组织 bootstrap 指令；raw 链接绕开 Gitea 自签证书导致 AI 工具无法抓取的问题。
- 2026-06-20 — 新增 `wiki/decisions/008-interlink-with-markdown-links.md`：定 markdown 链接为互链格式、由 LLM 维护（ADR-008）。
- 2026-06-20 — 落地文档间互链：方法论文档加"互链约定"段 + 4 模板补 `## 相关` + §五 Lint 加悬空/单向链接检查 + 新增 CRITICAL 互链工具动作规则（AGENTS.md 与方法论文档模板两处）。
- 2026-06-20 — 新增 `wiki/decisions/007-log-trigger-split.md`：为本轮 log 触发规则拆分补 ADR，记录决策理由（ADR-007）。
- 2026-06-20 — 修订 CRITICAL 维护规则：拆分 index 触发与 log 触发——index 仅在 wiki 新增页面时追加；log 扩为"任何结构/意图层面变更（新建/删改/改名文件、根级文档修订、核心术语或决策调整）后"追加。修正原规则只覆盖新建文件、遗漏根级文件与修订的盲区（原规则与 log.md 自述 scope 冲突，且违背 ADR-003 精确性前提）。同步改 `AGENTS.md` 与方法论文档。
- 2026-06-19 — 新增 `README.md`（项目入口说明，根级、不入 wiki index）。
- 2026-06-19 — 按本方法论为项目自身建立知识库：新增 `AGENTS.md`（基础层）+ `wiki/`（architecture×1、decisions×6、sessions×1、bugs 空骨架）+ loose `wiki/ab-test-findings.md`。设计会话总结见 `wiki/sessions/001-methodology-design.md`。
- 2026-06-19 — 方法论定稿并改名 `ai-project-context-pattern.md`（前身 `ai-wiki-context-pattern.md`；更早源自一份 PD 分层文档与 `llm-wiki.md` 想法）。移除与他文档的对照附录（v1.1）；删除冗余的 PD 文档与 `llm-wiki.md`（精神已吸收）。
