# ADR-003：维护规则用 CRITICAL + 工具动作级；Lint 必需

> 日期：2026-06-19  状态：已采纳

## 背景
实测发现**"载入上下文" ≠ "被遵循"**：平淡的行为指令（尤其需判读意图的，如 answer-only 的"询问时别改代码"）经常被违反——模型"乐于助人"默认会压过不显眼的规则。若维护 wiki 靠这类指令，必然经常漏更新 index / log。

## 选择
1. 维护规则写成**工作流里的具体"下一个动作"**（工具动作级），用 CRITICAL 标注、放 AGENTS.md 顶部。
2. **Lint 列为必需**，作为对"不完美遵循"的自愈网。

## 理由
1. 约束**工具动作**的规则（如"创建文件后下一个动作是追加 index"）远比约束**意图判读**的规则耐破——前者无歧义。
2. 把"正确动作"做成"零成本默认动作"（index 本就在眼前），降低对合规的依赖。
3. 行为指令必被偶尔违反 → Lint 定期扫漂移（孤儿页 / index 缺条目 / 矛盾 / 过时主张）并修复，兜底。

## 后果
- AGENTS.md 顶部要保留醒目的 CRITICAL 区。
- Lint 是周期性开销，但换来自愈；不做 Lint = 反模式（方法论反模式 #7）。
- A/B 测试中观察到：Wiki 代理在改动后**主动**跑了一次 Lint（无人提示），验证此设计有效（见 [A/B 测试发现](../ab-test-findings.md)）。

## 相关
- 证据：[A/B 测试发现](../ab-test-findings.md)
- 规则精确性前提：[ADR-007](007-log-trigger-split.md)、[ADR-008](008-interlink-with-markdown-links.md)
- 架构总览：[overview](../architecture/overview.md)
- Lint 语义项强化（摘要无状态）：[ADR-010](010-stable-descriptor-index.md)
