# ai-project-context-pattern

> 用"知识库"方式组织 AI 项目上下文的方法论。

## 是什么
一套让 AI **增量沉淀、持续维护**项目知识库的模式——采用两层**渐进式披露**（基础层 `AGENTS.md` 自动加载 + 揭示层 `wiki/` 按需读），不是每次对话重新发现（RAG），而是让 LLM 边读边把知识累积进持久 wiki，越用越富。

## 结构
```
项目根/
├── AGENTS.md            ← 自动加载：维护规则 + 定位 + index（导航中枢）
├── log.md               ← 项目变更日志
└── wiki/                ← AI 自主维护的知识
    ├── architecture/       技术架构
    ├── decisions/          决策（ADR：为什么这么定）
    ├── bugs/               bug 复盘
    ├── sessions/           会话归档（按需、总结后）
    └── *.md                其余知识（概念 / how-to）
```

## 怎么用
把 [`ai-project-context-pattern.md`](ai-project-context-pattern.md) 给你的 AI（opencode / Claude Code 等），让它按文中的 Bootstrap 流程，给你的项目搭一套同样的知识库。

## 这个仓库本身就是实例
本 repo 用自己的方法论维护自身的知识库（`AGENTS.md` + `wiki/`）——即 dogfooding，可直接参考它长什么样。

## 灵感来源
灵感来自 Andrej Karpathy 的 [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)——让 LLM 增量构建并维护一个持久 wiki，而非每次从原始文档重新检索（RAG）。本仓库把这套理念应用到了**项目**上下文的组织上。

---
方法论全文：[`ai-project-context-pattern.md`](ai-project-context-pattern.md)
