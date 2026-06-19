# ai-project-context-pattern

> 定位：指导 AI 用"知识库"方式组织项目上下文的方法论（权威定义见 `ai-project-context-pattern.md`）；本仓库同时用该方法论维护自身的知识库（dogfooding）。

<!-- ============ 维护规则（CRITICAL）·人定，LLM 禁改 ============ -->
## 维护规则（CRITICAL）

- 回答任何实质问题前：你的**下一个动作**是完整阅读下方 index，再决定读哪些 wiki 页。
- 在 wiki/ 下**新增页面后**：你的**下一个动作**是在下方 index 追加一行（index 仅此情况追加）。
- 发生**结构/意图层面的变更后**（新建 / 删改 / 改名文件、根级文档修订、核心术语或决策调整）：你的**下一个动作**是在 `log.md` 追加一条（最新在上，记"变了什么 + 为什么"）。
- wiki/ 下**只允许** 4 个子目录（architecture/decisions/bugs/sessions）或根级 loose 文件；**禁止新建其他子目录**。
- 你**只能修改本文件的 index 区**；本文件其余区域（规则、定位）禁止修改。
- **禁止归档原始会话**；session 归档前必须先总结。

<!-- ============ 项目定位·人定 ============ -->
## 项目定位
本仓库是"AI 项目上下文组织方法论"的家：方法论全文见 `ai-project-context-pattern.md`（权威定义，不在 wiki 内重复）；`wiki/` 是该方法论在本项目自身的实例化（决策理由、架构、设计会话等）。

<!-- ============ index·LLM 维护 ============ -->
## index（wiki 全量目录）
### architecture
| 文件 | 摘要 |
|---|---|
| `wiki/architecture/overview.md` | 仓库双重身份与结构：方法论文档 + 自身知识库（基础层/揭示层 + 加载机制） |

### decisions
| 文件 | 摘要 |
|---|---|
| `wiki/decisions/001-compile-once-anti-rag.md` | 核心哲学：增量沉淀+持续维护（反 RAG），而非全量加载/每次重算 |
| `wiki/decisions/002-index-in-agents-md.md` | index 永驻 AGENTS.md，不外置、不进 opencode.json instructions |
| `wiki/decisions/003-critical-tool-action-lint.md` | 维护规则用 CRITICAL+工具动作级，Lint 必需（应对遵循度问题） |
| `wiki/decisions/004-flat-four-dirs-no-tree.md` | 扁平 + 4 固定子目录，禁止三级目录与自建顶级目录 |
| `wiki/decisions/005-no-raw-layer.md` | 不设 raw 层 |
| `wiki/decisions/006-on-demand-session-archiving.md` | 会话按需、总结后归档，非每次必存 |
| `wiki/decisions/007-log-trigger-split.md` | 拆分 index/log 触发：log 覆盖所有结构/意图变更（非仅新建文件） |

### bugs
| 文件 | 摘要 |
|---|---|

### sessions
| 文件 | 摘要 |
|---|---|
| `wiki/sessions/001-methodology-design.md` | 方法论设计会话：从 PD 模式演进到知识库式上下文模式 |

### 其他（根级 loose）
| 文件 | 摘要 |
|---|---|
| `wiki/ab-test-findings.md` | A/B 测试发现：知识库式 vs 精简懒加载式的强弱项 |
