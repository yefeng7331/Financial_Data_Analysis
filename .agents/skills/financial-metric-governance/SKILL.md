---
name: financial-metric-governance
description: Define or review governed financial metrics, semantic metadata, dimensions, synonyms, and calculation contracts for the Financial_Data_Analysis banking question-answering project. Use for metric catalogs, business definitions, semantic-layer design, and metric ambiguity analysis; do not use for investment valuation or trading signals.
---

# Financial Metric Governance

Build metric definitions that produce one reproducible answer for one stated business question.

## Source of truth

1. Read `需求分析/1.资料/金融/金融需求说明.md` before defining project metrics.
2. Inspect the actual schema, seed data, migrations, and existing metric code when present. Do not invent tables or fields.
3. If requirements and implementation disagree, report the conflict and treat the implemented contract as unverified until the user chooses the authority.

## Required metric contract

For every metric, define its business meaning, formula, grain, time field and timezone, filters, status rules, distinct key, currency treatment, supported dimensions, null handling, data owner, and validation example. Use [references/metric-contract.md](references/metric-contract.md) when creating or reviewing a metric catalog.

Resolve ambiguous words such as “客户数”, “交易金额”, “贷款余额”, “逾期余额”, and “回收率” before implementation. Ask only when the choice materially changes the result and cannot be recovered from project evidence.

## Boundaries

- Keep metric logic independent from presentation wording.
- Version breaking definition changes; do not silently rewrite historical meaning.
- Preserve traceability from answer to metric, fields, filters, and data timestamp.
- Do not change databases, migrations, `.env`, credentials, or production data without explicit approval.
- Treat investment recommendations, market forecasts, and trading signals as out of scope.
