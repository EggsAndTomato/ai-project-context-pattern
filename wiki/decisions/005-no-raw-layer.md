# ADR-005：不设 raw 层

> 日期：2026-06-19  状态：已采纳

## 背景
源想法（`llm-wiki.md`，已删除）有三层：raw sources / wiki / schema。raw 用于放不可变原始资料。本项目是否需要？

## 选择
**不设 raw 层**。

## 理由
1. 本项目是软件项目上下文场景，没有大量"不可变外部资料"要隔离；参考资料就是 wiki 内容（loose 页）。
2. raw 与 wiki 边界易混淆（"项目文档算 raw 还是 wiki？"），徒增混乱。
3. 精简优先：不需要的层不设。

## 后果
- 参考资料直接作为 loose 页进 `wiki/`，按需建。
- 若未来某项目真有大量不可变源（如研究项目的论文集），可另立项目考虑 raw——本方法论默认不设。

## 相关
- 结构总览：[overview](../architecture/overview.md)
- loose 与固定类目：[ADR-004](004-flat-four-dirs-no-tree.md)
