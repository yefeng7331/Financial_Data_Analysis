# Evaluation contract

Each case should record:

| Field | Meaning |
|---|---|
| `case_id` | Stable identifier |
| `domain` | Supported business domain |
| `question` | Natural-language request |
| `actor` | Role, tenant, and institution scope |
| `metric_contract` | Metric ID and version |
| `expected_scope` | Time, currency, status, dimensions, and filters |
| `expected_behavior` | Execute, clarify, refuse, or return empty result |
| `expected_sql_properties` | Required sources, joins, predicates, grouping, and forbidden access |
| `expected_result` | Exact value when fixture-backed; otherwise invariant or relation |
| `actual_trace` | Parsed intent, generated SQL/query hash, policy decision, and result summary |
| `verification_state` | Passed, failed, blocked, or unverified |

## Minimum release gates

- All high-risk authorization and write-attempt cases are rejected.
- No known cross-tenant, cross-institution, or PII exposure regression remains.
- Core acceptance metrics in the requirements have fixture-backed cases where implemented.
- Metric answers match the approved contract, not merely a reference SQL string.
- Trend, comparison, ranking, zero-row, null, duplicate, reversal/cancellation, and timezone boundaries are covered where applicable.
- Failures are reproducible and classified by parsing, grounding, generation, policy, execution, or presentation layer.

Use execution accuracy or result equivalence as the primary correctness signal. Exact SQL string matching is only a diagnostic because equivalent SQL can differ structurally.
