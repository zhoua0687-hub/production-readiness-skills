---
name: readiness-quality-maintainability
description: Review test quality and coverage, regression and load testing, test data, code review, dependency and framework maintenance, dead code, complexity, architecture records, onboarding and handover documentation, support tooling, changelogs, ownership, and bus factor. Use for every codebase at an appropriate depth and when the router selects R-08.
---

# Quality and Maintainability Review

Evaluate whether people can verify, change, release, and inherit this product safely. Do not equate test count with correctness, large files with defects, or missing process documents with proof that a team has no process.

## Applicability

Use for source code and tests in every project, narrowing checks to the languages, platforms, business flows, team, and delivery model that actually exist. CI enforcement belongs to R-07, third-party contract details to R-06, and dependency security/provenance to R-02.

## Evidence to inspect

Inspect test suites and their assertions, critical-flow coverage, fixtures, test-data generation, CI/test configuration, review/branch configuration when available, manifests, framework versions, dead-code signals, large/complex modules, architecture records, README, support/admin tooling, changelogs, and ownership/handover material.

## Checks

### Tests and verification

- Unit tests must express intended behavior and meaningful boundaries, not only mirror the implementation or inflate coverage.
- Integration tests should cover real third-party contracts and failure modes at appropriate depth. End-to-end tests should cover signup, checkout, and other critical/revenue flows only when those flows exist.
- Load testing should match launch and realistic usage risks; do not demand a fixed scale without product evidence. Never load-test production without authorization.
- Test data should resemble production shape and edge cases without copying production personal, customer, patient, secret, or payment data.
- Regression tests should preserve prior bug fixes, especially interacting behaviors. Trace claims such as “tested” to actual test code and results.
- Old hardware, supported browsers, and platform versions should be tested according to the actual customer base and support policy.

### Change and dependency health

- Code should be readable, appropriately structured, and consistent with local idioms. Identify concrete duplication, stale experiments, unreachable code, or excessive responsibilities rather than applying an arbitrary line-count rule.
- Code review and branching should prevent unreviewed changes and destructive conflicts where team/delivery risk requires them. Repository host settings are external evidence when unavailable.
- Dependencies and frameworks need a sustainable upgrade cadence and support-window awareness. Monthly review may be useful, but upgrade timing should reflect vulnerabilities, compatibility, and upstream support rather than a ritual alone.
- Remove dead code only after confirming references and behavior. Split oversized files only when cohesion and change risk justify it.

### Knowledge, support, and ownership

- Architecture decisions should record context, alternatives, and reasons for consequential choices. README setup instructions should be complete enough for a newcomer; do not claim “under an hour” without an observed onboarding test.
- Documentation should cover operation, recovery, support, and inherited knowledge appropriate to the product.
- Admin and support tooling should let operations/customer success perform required work safely without routine engineering intervention; least privilege and audit remain applicable.
- Customer changelogs should communicate relevant behavior and breaking changes when the product has external users or integrations.
- Accounts, domains, repositories, signing identities, and cloud resources should have appropriate company ownership and recovery paths; verify externally rather than inferring from names.
- Bus factor requires shared access, documentation, and practical knowledge. A second name on an account alone does not prove continuity.

## Verification boundaries

Run existing tests only when the environment is available and execution is authorized; do not install unrequested dependencies or run destructive/load tests. Report commands, environment, outcomes, and untested platforms honestly. External review policies, ownership, and staffing remain `UNCONFIRMED` without records.

## Output

Return findings with `finding_id`, `R-08`, severity, status, confidence, claim, concrete regression/delivery/maintenance scenario, evidence IDs/locations, validation, recommendation, and missing evidence. Separate verified test results, coverage gaps, and external process unknowns. Mirror both languages with identical IDs. For document output, save `readiness-quality-maintainability-report.en.md` and `readiness-quality-maintainability-report.zh-CN.md` as a pair without overwriting existing reports. Do not modify product files.
