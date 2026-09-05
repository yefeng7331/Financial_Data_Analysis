# SQL safety checklist

Apply these checks to the parsed statement or database AST, not only with string matching.

## Before execution

- Exactly one statement and an allowed read operation (`SELECT`, or a dialect-equivalent read-only query).
- No comments or encoding tricks that alter parser interpretation.
- Every referenced catalog, schema, table, column, function, and join path is allowlisted.
- Tenant, institution, role, and row-level predicates are injected or enforced by the database policy layer.
- Sensitive columns are removed, masked, or aggregated according to the verified role.
- A bounded time range is present for large event tables unless an approved snapshot query is used.
- Row limit, timeout, memory limit, and concurrency budget are enforced outside the generated SQL.
- Query plan or cost estimate is checked when the database supports it.

## Explicitly reject

Reject DDL/DML, `COPY`, `LOAD`, export commands, filesystem or network functions, extension installation, unsafe user-defined functions, stored procedures, session-setting changes, privilege changes, transaction control, temporary-object creation, and multiple statements.

## After execution

- Record actor, role, normalized question, approved metric version, query hash, policy decision, source timestamp, duration, row count, and outcome.
- Validate result shape, null rate, duplicate risk, currency, totals, and expected range.
- Avoid logging raw sensitive values or secrets.
- On failure, preserve the guardrails and return a bounded diagnostic. Never retry with broader access.
