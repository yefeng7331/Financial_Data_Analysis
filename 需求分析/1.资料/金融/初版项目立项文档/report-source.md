# 金融问数系统技术栈调研：研究底稿

- 日期：2026-09-05
- 范围：自然语言问数、Text-to-SQL、语义层、金融数据平台、BI、安全与评测
- 决策目标：形成第一版技术栈建议，提交用户审批；不修改现有项目流程提示词
- 样本：WrenAI、DB-GPT、Vanna、Dataherald、Chat2DB、OpenBB、FinRobot、Apache Superset、Snowflake Cortex Analyst、Databricks Genie

## 核心证据账本

| 结论 | 证据 | 可信度 | 限制 |
|---|---|---:|---|
| 语义层是可靠问数的核心，而不是附加项 | WrenAI 的 MDL/上下文层；Snowflake Semantic View/YAML；Databricks 指标、维度、同义词与样例 SQL | 高 | 商业产品内部实现不公开 |
| 已验证的“问题—SQL—结果”样例应进入持续评测 | Snowflake Verified Query Repository 与隔离评测；Databricks example queries | 高 | 需要项目自行建设金融测试集 |
| Python/FastAPI 是开源问数与金融 AI 项目的主流组合之一 | DB-GPT、Vanna、OpenBB 均公开采用 Python/FastAPI；FinRobot 使用 Python | 高 | 不是唯一合理选择 |
| 不宜直接以 Vanna 仓库为长期底座 | GitHub 显示该仓库于 2026-03-29 归档只读 | 高 | 可借鉴设计，不能按活跃上游依赖 |
| 直接采用完整 DB-GPT/WrenAI 会引入超出第一版的复杂度 | 两者均覆盖多数据源、Agent/RAG、报表等广泛能力；WrenAI 还有 Rust/DataFusion 语义核心 | 中高 | 若项目后续转为平台型产品可重新评估 |
| 查询安全必须依靠数据库权限与多层校验 | PostgreSQL RLS；Superset 明确自身不是数据库防火墙并要求最小权限 | 高 | AST 解析不能替代数据库权限 |
| SQLGlot 适合 AST 审查与方言处理，但不能单独承担执行验证 | SQLGlot 官方 README 明确其是解析/转译工具，不是完整验证器 | 高 | 仍需只读账号、超时、限行和执行前检查 |
| v1 使用 PostgreSQL + pgvector 可减少基础设施数量 | pgvector 在 PostgreSQL 内支持精确检索及 HNSW/IVFFlat | 中高 | 大规模多租户检索时需重新压测，可能升级 Qdrant |
| LangGraph 适合问数闭环的可恢复状态流程 | 官方文档支持持久化、人工介入、流式输出与故障恢复 | 高 | 仍需项目自行设计状态契约与幂等规则 |

## 主要来源

- [WrenAI GitHub](https://github.com/Canner/WrenAI)
- [DB-GPT GitHub](https://github.com/eosphoros-ai/DB-GPT)
- [Vanna GitHub](https://github.com/vanna-ai/vanna)
- [Dataherald GitHub](https://github.com/dataherald/dataherald)
- [Chat2DB GitHub](https://github.com/OtterMind/Chat2DB)
- [OpenBB GitHub](https://github.com/OpenBB-finance/OpenBB)
- [FinRobot GitHub](https://github.com/AI4Finance-Foundation/FinRobot)
- [Apache Superset GitHub](https://github.com/apache/superset)
- [Snowflake Cortex Analyst](https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-analyst)
- [Snowflake Verified Query Repository](https://docs.snowflake.com/en/user-guide/views-semantic/verified-query-repository)
- [Databricks Genie 配置](https://docs.databricks.com/aws/genie/set-up)
- [Databricks Genie 质量调优](https://docs.databricks.com/aws/en/genie-agents/tune-quality)
- [LangGraph Persistence](https://docs.langchain.com/oss/python/langgraph/persistence)
- [SQLGlot GitHub](https://github.com/tobymao/sqlglot)
- [pgvector GitHub](https://github.com/pgvector/pgvector)
- [PostgreSQL Row Security](https://www.postgresql.org/docs/17/ddl-rowsecurity.html)
- [Langfuse GitHub](https://github.com/langfuse/langfuse)
- [BAAI BGE-M3](https://huggingface.co/BAAI/bge-m3)

