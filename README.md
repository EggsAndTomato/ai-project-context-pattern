# ai-project-context-pattern

> 用 AI 搞 vibe coding 时，把项目变成会自己长大的知识库的方法论。

## 是什么
如果你用 AI 搞 vibe coding，这里有一套把项目变成**会自己长大的知识库**的方法——AI 在每次对话里顺手沉淀、持续维护，越用越富，而不是每次都从头重新找一遍（RAG）。

靠两层**渐进式披露**做到：基础层 `AGENTS.md`（项目根、自动加载）放维护规则 + 全量导航 index；揭示层 `wiki/` 按需读，装项目自己的知识。知识**会复利**——交叉引用、矛盾标注、综合分析都在 wiki 里预先做好，直接拿来用。

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

最省事的方式：复制下面这段提示词丢给你的 AI（工具无关，opencode / Claude Code / Cursor / Aider 皆可），它会抓取文档并执行 bootstrap：

```
请用《AI 项目上下文模式》给当前项目搭一个 AI 自维护的知识库。

文档地址（先抓取并完整阅读）：
https://raw.githubusercontent.com/EggsAndTomato/ai-project-context-pattern/refs/heads/master/ai-project-context-pattern.md

然后按文档「第八节 Bootstrap 流程」执行：
1. 重点看：第三节 AGENTS.md 结构、第八节 Bootstrap、第九节检查清单。
2. 先摸底当前代码库；定位 / 技术栈 / 已有架构与决策里不清楚的点，列清单问我——确认后再动手，别急着建文件。
3. 在项目根建：AGENTS.md（CRITICAL 维护规则 + 1 行定位 + index 骨架）、log.md（空骨架）、wiki/ 下 4 个固定空子目录（architecture/decisions/bugs/sessions）。
4. 至少写 wiki/architecture/overview.md，并登记进 index。
5. 用第九节检查清单自检。

先回我：你读到的要点 + 要问我的定位问题。确认后再落盘。
```

## 这个仓库本身就是实例
本 repo 用自己的方法论维护自身的知识库（`AGENTS.md` + `wiki/`）——即 dogfooding，可直接参考它长什么样。

## 灵感来源
灵感来自 Andrej Karpathy 的 [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)——让 LLM 增量构建并维护一个持久 wiki，而非每次从原始文档重新检索（RAG）。本仓库把这套理念应用到了**项目**上下文的组织上。

---
方法论全文：[`ai-project-context-pattern.md`](ai-project-context-pattern.md)
