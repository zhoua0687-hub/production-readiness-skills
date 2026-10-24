---
name: readiness-data-reliability
description: Review data modeling, migrations, query scalability, pooling, backup and recovery, deletion, timezones and Unicode, generic idempotency, pagination, imports/exports, and retention. Use when data is stored or exchanged and when the production-readiness router selects R-03.
---

# Data Reliability Review

Match the depth of review to the actual datastore and product promises. A local in-memory tool does not need database migrations or nightly hosted backups, but its persistence and recovery expectations must be established before exclusion.

## Applicability

Use for databases, files, local persistence, shared state, imports/exports, background writes, contractual retention, or recovery requirements. Money-specific representation belongs to R-04; generic non-payment idempotency remains here even when payments are not applicable.

## Evidence to inspect

Inspect schemas, models, migrations, query paths, indexes, datastore configuration, connection lifecycle, transaction boundaries, jobs, serialization, import/export code, deletion paths, and available backup/restore/retention records. Cloud backup, PITR, restore drills, and production query plans require external or runtime evidence.

## Checks

### Model, migration, and scale

- Assess whether the schema expresses real entities, ownership, invariants, uniqueness, lifecycle, and extension points coherently. Do not label a schema “AI improvised” from style alone.
- Migrations must have explicit forward behavior and honest rollback behavior. If a change is irreversible, identify why and how data is preserved; never invent a down migration that loses data.
- Check lock duration, table rewrites, backfills, concurrent/index strategies, and deploy compatibility for realistic table sizes. Do not run unapproved migrations on live data.
- Compare indexes and query plans with actual filters, joins, sort order, and cardinality. Deep pagination must remain stable under inserts/deletes and avoid pathological offsets where scale requires it.
- Connection acquisition, pooling, timeouts, transaction scope, and concurrency must not exhaust the datastore during plausible bursts.

### Recovery and deletion

- Nightly or otherwise appropriate backups must match recovery objectives. Confirm configuration separately from actual restore-test evidence.
- PITR is required only when the recovery objective calls for it; verify coverage, retention, and restoration rather than assuming a vendor feature is enabled.
- Soft delete or undo should support accidental-deletion recovery where the product promises it, while respecting retention and erasure obligations. Do not mandate soft deletes for every record.

### Correctness and interchange

- Store instants unambiguously, normally UTC, and preserve the intended timezone for future/local reminders. Test DST changes and date-only values separately.
- Exercise apostrophes, accents, emoji, non-Latin scripts, and right-to-left text through storage, retrieval, search, export, and display without corrupting meaning.
- Generic retries and repeated submissions need idempotency or deduplication at the trusted write boundary, with uniqueness scope and concurrent-request behavior checked.
- Imports and exports are requirement-driven. When applicable, test real encodings, delimiters, quoting, legacy CSV behavior, partial failure, large files, and repeatable exports.
- Retention code must implement contractual deletion across primary stores, derived data, caches, files, and jobs. Backup/log erasure obligations are coordinated with R-10 and require external evidence where applicable.

## Verification boundaries

Never run destructive migration, restore, deletion, or load tests against production without explicit authorization. Record dataset sizes and runtime availability. Missing cloud or drill records means `UNCONFIRMED`, not proof that backups or restores do not exist.

## Output

Return findings with `finding_id`, `R-03`, severity, status, confidence, claim, concrete data-loss/corruption/availability scenario, evidence IDs/locations, validation, recommendation, and missing evidence. Keep controls and unknowns separate and mirror both languages with identical IDs. For document output, save `readiness-data-reliability-report.en.md` and `readiness-data-reliability-report.zh-CN.md` as a pair without overwriting existing reports. Do not modify product files or data.
