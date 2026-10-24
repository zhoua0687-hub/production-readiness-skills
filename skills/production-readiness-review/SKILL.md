---
name: production-readiness-review
description: Coordinate an evidence-based production readiness review of a whole project. Use for launch readiness, production audits, enterprise readiness, or broad risk checklists. Build a project profile, select only applicable specialist skills, expose skipped and unknown scope, and produce matching Chinese and English reports. Not intended for a single-diff code review.
---

# Production Readiness Review

Act as the coordinator, not as a substitute for every specialist. Select and aggregate specialist reviews without inventing evidence or mechanically running every checklist.

## Non-negotiable rules

- Keep the reviewed product read-only. Do not edit code, configuration, infrastructure, dependencies, or external services.
- Do not run destructive tests, credential attacks, production load tests, or external scans without explicit authorization.
- Ask only questions whose answers materially change scope. Otherwise inspect available evidence and record the limitation.
- Never convert "not found" into "not implemented", "not applicable", or "safe".
- Never fabricate a finding, control, test result, file, line number, certification, or operational practice.
- Do not copy secrets, personal data, card data, tokens, or other sensitive values into reports.
- Keep Chinese and English outputs equivalent in scope, IDs, findings, severity, evidence, ordering, and limitations.

## Required references

Read these files before routing:

1. `references/project-profile.en.md` or `references/project-profile.zh-CN.md` for the profile and route matrix.
2. `references/evidence-and-severity.en.md` or `references/evidence-and-severity.zh-CN.md` for statuses, evidence, and ranking.
3. `references/report-template.en.md` and `references/report-template.zh-CN.md` when producing the final reports.

Use one language for working instructions if context is limited, but always preserve both output versions.

## Specialist catalog

Every module must appear in the route matrix, including skipped modules.

| Route ID | Skill name | Primary scope |
|---|---|---|
| R-01 | `readiness-identity-access` | Authentication, recovery, sessions, authorization, tenants, enterprise identity |
| R-02 | `readiness-application-security` | Secrets, dependencies, input, OWASP, uploads, browser/security boundaries, encryption, privileges, safe logs |
| R-03 | `readiness-data-reliability` | Data model, migrations, queries, backups, recovery, time/Unicode, generic idempotency, import/export, retention |
| R-04 | `readiness-payments-billing` | Money, charging, subscriptions, invoices, refunds, tax, metering, reconciliation |
| R-05 | `readiness-ai-safety` | Models, prompts, agents, sensitive prompt data, evals, model spend, fallback, human approval |
| R-06 | `readiness-integrations` | External APIs, OAuth, webhooks, API versioning, customer keys, sandboxes, transactional email |
| R-07 | `readiness-operations` | Environments, delivery, rollout, queues, capacity, DR, telemetry, incidents, cost and storage operations |
| R-08 | `readiness-quality-maintainability` | Tests, review, dependencies, code health, documentation, support tooling, ownership, maintainability |
| R-09 | `readiness-user-experience` | Weak networks, UI states, actionable errors, accessibility, localization, notifications, undo, navigation |
| R-10 | `readiness-compliance` | Assurance, SOC 2, HIPAA/BAA, PCI, GDPR, residency, access reviews, legal-policy alignment |

Cross-cutting concerns have one primary owner. Generic idempotency belongs to R-03 even when R-04 is skipped; payment-specific idempotency belongs to R-04. View and change audit requirements belong to R-10, while concrete authorization enforcement belongs to R-01. Merge duplicates during aggregation.

## Workflow

### 1. Establish the project profile

Inspect actual source, dependency manifests, configuration, tests, deployment files, and documentation needed for scope. Identify product type, execution entry points, users, tenants, data classes, money flow, AI use, external integrations, delivery model, and known operational boundaries.

Do not inspect unrelated files merely to make the review look exhaustive. Record inspected roots and unavailable components such as private backends, cloud accounts, CI systems, contracts, or production telemetry.

### 2. Route every module

Assign each module exactly one routing decision:

- `RUN`: positive evidence shows the capability or risk exists, or the user explicitly requested the module.
- `NOT_APPLICABLE`: affirmative product-scope evidence plus an appropriate technical inspection supports exclusion. Record both.
- `UNCONFIRMED`: evidence is insufficient to decide. Run a bounded evidence-gap review when possible; otherwise state what is missing.

A missing SDK, keyword, UI screen, or repository file alone is not affirmative proof of absence. A module may be `RUN` while individual checklist items are `NOT_APPLICABLE` or `UNCONFIRMED`.

### 3. Run selected specialists

Use the Skill tool to invoke selected specialists by their exact catalog names. Pass the project profile, inspected scope, user constraints, route ID, and known evidence gaps. For an `UNCONFIRMED` route, request evidence-gap analysis rather than assuming a full implementation exists.

If a required specialist is unavailable or cannot complete, mark its execution `NOT_REVIEWED` and explain why. Do not simulate its result.

A specialist may discover evidence that challenges the initial route. Re-evaluate the route explicitly and retain the reason for the final decision.

### 4. Aggregate and prioritize

Normalize specialist results using the shared evidence guide. Merge duplicate findings without losing evidence. Prioritize confirmed data disclosure, financial loss, unrecoverable data loss, and service interruption, then consider exploitability, blast radius, likelihood, and evidence confidence.

Report at most ten priority findings. Fewer verified findings means a shorter list. Keep lower-priority results and evidence gaps in their proper sections rather than inflating severity.

### 5. Produce both versions

Use stable route IDs (`R-01`…`R-10`), finding IDs (for example `F-APPSEC-001`), and evidence IDs (`E-001`…) in both versions. Translate prose only; keep paths, code, configuration keys, commands, and identifiers unchanged.

If the user requested document output, create both `readiness-report.zh-CN.md` and `readiness-report.en.md` in a user-selected or new report directory. Inspect the destination and never overwrite an existing report. Report files are the only permitted writes; product files remain untouched.

If the user requested chat output only, provide Chinese and English versions with equivalent content. Do not claim files were saved.

## Final quality gate

Before delivering, verify:

- Every route has a decision, reason, evidence, and gaps.
- Every confirmed finding and confirmed control has reviewable evidence.
- `UNCONFIRMED` and `NOT_REVIEWED` are visible and not counted as passes or vulnerabilities.
- Both versions have identical IDs, counts, severity, ordering, and limitations.
- The report states what was not dynamically tested.
- No product code or configuration was changed.
