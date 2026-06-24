# 仓库架构总览

> 边界：本文写"本仓库是什么、怎么组织、怎么加载"。
>   - 各项决策的"为什么" → `../decisions/`
>   - 方法论的完整规则 → 根目录 `ai-project-context-pattern.md`

## 仓库的双重身份
本仓库既是**方法论的定义**（`ai-project-context-pattern.md`，权威），又是该方法论的**自身实例**（`AGENTS.md` + `wiki/` + `log.md`，dogfooding）。

## 结构
```
项目根/
├── ai-project-context-pattern.md   ← 方法论权威定义（不在 wiki 内重复）
├── AGENTS.md                        ← 基础层：CRITICAL 规则 + 定位 + index（自动加载）
├── log.md                           ← 项目变更日志
└── wiki/                            ← 揭示层：项目自身的知识
    ├── architecture/
    ├── decisions/
    ├── bugs/
    ├── sessions/
    └── *.md (loose)
```

## 加载机制
- `AGENTS.md` 在项目根 → opencode / Claude Code **每会话自动加载**（只加载根目录的 AGENTS.md，子目录不加载；详见方法论第三节）。
- index 永驻 AGENTS.md → 导航是零成本默认动作，不依赖行为指令（ADR-002）。
- `wiki/` 各页由 AI 按需 Read（懒加载）。

## 关键约束
- 方法论的权威定义只在 `ai-project-context-pattern.md`；wiki 不重复规则，只记"本项目的决策 / 架构 / 会话"。
- 单一事实源：每条决策理由只在对应 ADR，别处只链接。

## 相关
- 哲学选型：[ADR-001：增量沉淀+持续维护](../decisions/001-compile-once-anti-rag.md)
- 加载与 index 归属：[ADR-002：index 永驻 AGENTS.md](../decisions/002-index-in-agents-md.md)
- index 摘要规范：[ADR-010：无状态描述符](../decisions/010-stable-descriptor-index.md)
- 互链约定：[ADR-008：markdown 链接互链](../decisions/008-interlink-with-markdown-links.md)
