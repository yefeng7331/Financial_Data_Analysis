# Metric contract

Use this checklist for each governed metric.

| Field | Required decision |
|---|---|
| `metric_id` | Stable English identifier |
| `business_name` | Primary Chinese name |
| `definition` | Plain-language meaning and exclusions |
| `formula` | Aggregation formula with numerator and denominator where applicable |
| `grain` | Customer, account, transaction, order, contract, case, day, or other verified grain |
| `time_semantics` | Event field, timezone, inclusive/exclusive boundary, snapshot versus flow |
| `filters` | Valid statuses, cancellation/reversal handling, institution and channel scope |
| `distinct_key` | Key used to prevent duplicate counting |
| `currency` | Currency scope, conversion rule, rate date, and rounding |
| `dimensions` | Supported groupings and hierarchy |
| `null_policy` | Exclude, map to unknown, or fail validation |
| `synonyms` | Approved business aliases |
| `lineage` | Source tables, fields, joins, and transformation version |
| `owner` | Business owner and technical owner |
| `freshness` | Data timestamp and acceptable delay |
| `example` | Minimal input and expected output |

Project domains include customer, account, transaction, wealth management, credit, repayment, overdue, risk, anti-money-laundering, manual review, collection, and operations. Domain membership does not prove a schema exists.

Known synonym candidates from the requirements include `客户数/用户数`, `放款额/放款金额`, `理财规模/AUM`, and `逾期余额/逾期金额`. Confirm whether each pair is truly equivalent in the current data contract.
