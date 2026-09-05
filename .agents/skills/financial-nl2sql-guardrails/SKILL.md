---
name: financial-nl2sql-guardrails
description: Design, implement, or review safe natural-language-to-SQL behavior for the Financial_Data_Analysis banking analytics project. Use when work involves SQL generation, query execution, database permissions, sensitive financial data, or answer traceability; do not use for ordinary hand-written SQL unrelated to the question-answering pipeline.
---

# Financial NL2SQL Guardrails

Make generated queries correct, bounded, read-only, permission-aware, and auditable.

## Workflow

1. Inspect the actual database dialect, schema, relationships, access layer, and user/role context.
2. Ground generation with approved metadata, metric definitions, enum values, join paths, and verified example queries.
3. Parse and validate SQL before execution. Apply [references/sql-safety-checklist.md](references/sql-safety-checklist.md) whenever generated SQL may run.
4. Execute through a least-privilege read-only connection with time, row, memory, and concurrency limits.
5. Return the interpreted question, metric and time scope, SQL or a privileged-safe trace, result timestamp, and warnings. Do not expose hidden prompts, credentials, or unauthorized schema details.

## Non-negotiable invariants

- Generated SQL must not contain DDL, DML, transaction control, privilege changes, external file/network access, stored-procedure calls, or stacked statements.
- Authorization is enforced outside the model. Prompt instructions and frontend route guards are not security boundaries.
- Apply table, column, row, tenant, institution, and role restrictions before execution; reject queries that cannot be proven in scope.
- Minimize customer, account, loan, risk, AML, and collection identifiers. Aggregate or mask sensitive values unless the verified role requires detail.
- Never “repair” a failed query by broadening permissions or removing security filters.
- Database, `.env`, credential, and migration changes require explicit user approval.

When a question is materially ambiguous, return the ambiguity and safe interpretations instead of choosing a financially significant definition silently.
