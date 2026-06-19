# ADR-008：文档间用 markdown 链接互链（由 LLM 维护）

> 日期：2026-06-20  状态：已采纳

## 背景
方法论文档多处提到"互链 / 双链 / 交叉引用 / 单一事实源（别处只链接）"，但**从未定义机制**——没链接格式、没维护动作。结果 LLM 被要求"补交叉引用"却不知用什么格式，产出不一致的 backtick 死文本（本 repo 实测：wiki 内 0 个可点击链接）。这使 §五 Lint 的"孤儿页 / 缺失交叉引用"两项**空转**——它们要求真实链接才能检查。

Karpathy 的 llm-wiki 把交叉引用维护明确交给 LLM（"LLM 负责所有 bookkeeping"）；当前文档嘴上继承了这个分工，实际没落地。

## 选择
1. **格式定为 markdown 链接** `[文本](相对路径.md)`，**不**用 `[[wikilink]]`。
2. **维护交给 LLM**，写成工具动作级规则（ADR-003 风格）：新建 / 更新 wiki 页后，下一个动作是在 `## 相关` 段补结构相关页的链接，并在被链接页补反向链接。
3. **每个结构化页（architecture/decisions/bugs/sessions）须有 `## 相关` 段**；loose 页鼓励。
4. **Lint 的孤儿页 / 缺失交叉引用因此变得可执行**，并新增"悬空链接"（指向不存在文件）、"单向链接"（A→B 但 B 未回链）两项检查。

## 理由
1. **对齐 llm-wiki 分工**：人 sourcing / 提问，LLM 做 bookkeeping（含链接）——这正是 Karpathy 的核心分工。
2. **选 markdown 链接而非 wikilink**：守住"零工具 / 纯 markdown / 任意 agent 可用"的奠基卖点（ADR-001 / ADR-004）；markdown 链接在 GitHub / 任意查看器可直接点击，且可被 Lint grep。代价是无自动 graph view——这是有意识的取舍。
3. **工具动作级规则 > 抽象口号**（ADR-003）："下一个动作是补 markdown 链接"比"你要维护交叉引用"耐破得多。
4. **为大项目打底**：小项目靠扁平 index 够用；大项目页数多时，关系导航只能靠顺链接跳转——现在落地链接约定，是为 scale 预埋。

## 后果
- Lint 多了两项可执行检查（悬空 / 单向链接），自愈网更实。
- 链接随 ingest 增长，link rot（改名 / 删页导致悬空）靠 Lint 兜底。
- **未解决**：index 的 ~300 行天花板与超大规模下的搜索工具（qmd）需求——属独立未来问题，本次不动；markdown 链接不与之冲突，可后续叠加。

## 相关
- 极简哲学：[ADR-001](001-compile-once-anti-rag.md)、[ADR-004](004-flat-four-dirs-no-tree.md)
- 规则工具动作级：[ADR-003](003-critical-tool-action-lint.md)
- 架构总览：[overview](../architecture/overview.md)
