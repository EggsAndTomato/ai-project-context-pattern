# ADR-002：index 永驻 AGENTS.md（不外置、不进 instructions）

> 日期：2026-06-19  状态：已采纳

## 背景
index（wiki 全量目录）是每次会话都需要的导航中枢。三种承载方式：
- A. 直接写进 AGENTS.md；
- B. 独立 `index.md` + 注册进 `opencode.json` 的 `instructions`；
- C. 独立 `index.md` + AGENTS.md 写"必须先读 index.md"。

## 选择
选 A：index 永驻 AGENTS.md，**不外置、不进 instructions**。

## 理由
1. AGENTS.md 是项目根自动加载、最权威的文件——读 index 成为"零成本默认动作"，不依赖 LLM 遵守"去读"的指令（C 的风险）。
2. 实测 `opencode.json` `instructions` 的**遵循度不高**（"在场" ≠ "被用"），B 不可靠。
3. 外置 index = 把导航中枢变懒加载，自毁"编译一次、每次可用"的前提。
4. 单一事实源：index 只在 AGENTS.md，不与 instructions 里的副本漂移。

## 后果
- AGENTS.md 会随 wiki 增长而变长 → 约 300 行触发一次"目录瘦身 Lint"（合并碎条 / 归档过时项），**不切懒加载**。
- 作者权属分离：LLM 只能改 index 区，规则 / 定位区人定（见 CRITICAL 规则）。
