# ADR-004：扁平 + 4 固定子目录，禁止三级目录与自建顶级目录

> 日期：2026-06-19  状态：已采纳

## 背景
wiki 内部如何组织？候选：
- 三级目录树（如 `bugs/前端/渲染/xxx.md`）；
- 固定几个顶级类目 + 类目内扁平；
- 完全自由、LLM 任意建目录。

## 选择
`wiki/` 下**只允许 4 个固定子目录**：`architecture / decisions / bugs / sessions`，加根级 loose 文件。**禁止三级目录、禁止自建其他顶级目录**。

## 理由
1. AI 靠 **index + 标题**导航，不靠文件夹深度；三级目录路径长、难引用，无收益。
2. "bug → 排查 → 方案"是**页面内章节**，不是目录层级（用 `bugs/` 模板的小节承载）。
3. 固定封闭的类目集避免混乱（不出现"有的固定、有的可选"的半吊子）；零散知识放根级 loose，不另设 `notes/` 桶。
4. 自由建目录会破坏一致性，难以 Lint。

## 后果
- 4 类目覆盖架构 / 决策 / bug / 会话；其余概念 / how-to 放 loose（如本项目的 `../ab-test-findings.md`）。
- 若真出现第 5 类高频产物，再讨论是否加入固定集（目前不预期）。

## 相关
- 结构总览：[overview](../architecture/overview.md)
- loose 页示例：[ab-test-findings](../ab-test-findings.md)
- 互链依赖扁平结构：[ADR-008](008-interlink-with-markdown-links.md)
