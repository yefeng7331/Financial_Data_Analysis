---
name: financial-query-evaluator
description: Build or run evaluation suites for the Financial_Data_Analysis natural-language financial question-answering system. Use for golden questions, Text-to-SQL regression tests, metric correctness, security negative tests, robustness, and release acceptance; do not use as a substitute for defining missing business metrics.
---

# Financial Query Evaluator

Evaluate the full chain from user wording to governed, authorized, reproducible results.

## Evidence first

Read the financial requirements and inspect the actual schema, metric contracts, query pipeline, and available fixtures. Do not fabricate production data or expected values. If no executable fixture exists, produce a proposed test case marked `unverified` rather than claiming it passed.

Use [references/evaluation-contract.md](references/evaluation-contract.md) to structure cases and release results.

## Coverage

Include representative and boundary cases across customer, account, transaction, wealth management, credit, repayment, overdue, risk, AML, manual review, collection, and operations where the current implementation supports them. Cover time comparison, trend, ranking, institution/channel breakdown, synonyms, follow-up questions, empty results, invalid requests, and materially ambiguous definitions.

Security tests must include unauthorized tables and columns, cross-tenant or cross-institution access, prompt injection, attempts to request raw PII, stacked statements, DDL/DML, expensive unbounded queries, and malicious enum or identifier text.

## Scoring and reporting

Separate these dimensions: intent/metric selection, SQL validity, execution success, result equivalence, authorization, explanation/lineage, robustness, and latency. A syntactically valid SQL statement is not a correct answer.

Report verified passes, verified failures, blocked cases, and unverified proposals separately. Preserve failing questions, generated SQL, expected contract, actual result summary, and reproducible environment details without leaking sensitive data.

Do not modify databases, fixtures, expected results, or acceptance thresholds merely to make a run pass without explicit approval.
