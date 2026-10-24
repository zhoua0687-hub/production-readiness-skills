# Production Readiness Skills — English Guide

This suite adapts production-readiness review scope to the actual project. It does not force every product through one enormous checklist. It builds a project profile, selects applicable specialists, and aggregates evidence-based risks.

## Suite contents

- **One coordinator:** `production-readiness-review`
- **Ten specialists:** identity/access, application security, data reliability, payments/billing, AI safety, integrations, operations/resilience, quality/maintainability, user experience, and compliance/assurance
- **Three bilingual reference sets:** project profile/routing, evidence/severity, and review report templates

The coordinator and specialist directories are:

```text
production-readiness-skills/
├── README.en.md
├── README.zh-CN.md
└── skills/
    ├── production-readiness-review/
    │   ├── SKILL.md
    │   ├── SKILL.zh-CN.md
    │   └── references/
    ├── readiness-identity-access/
    ├── readiness-application-security/
    ├── readiness-data-reliability/
    ├── readiness-payments-billing/
    ├── readiness-ai-safety/
    ├── readiness-integrations/
    ├── readiness-operations/
    ├── readiness-quality-maintainability/
    ├── readiness-user-experience/
    └── readiness-compliance/
```

Every specialist directory contains an English `SKILL.md` and a Chinese `SKILL.zh-CN.md`.

## Core behavior

### Review only what applies

The coordinator records one route for every module:

- `RUN`: positive evidence shows the capability or risk exists, or the user explicitly requested the review.
- `NOT_APPLICABLE`: affirmative scope evidence and technical inspection jointly support exclusion.
- `UNCONFIRMED`: evidence is insufficient; perform bounded evidence-gap review where possible.

For example, payments can be skipped when affirmative scope establishes no charging or monetary data and technical inspection corroborates it. Merely finding no payment keywords remains `UNCONFIRMED`. Every module appears in the route matrix; none disappears silently.

### Evidence first

- Every issue needs a concrete risk scenario, severity, confidence, and reviewable location.
- Confirmed controls also need evidence; “looks secure” is not a conclusion.
- Missing repository documents about restore drills, on-call, or compliance do not prove those practices are absent.
- `UNCONFIRMED` and `NOT_REVIEWED` are neither passes nor automatic vulnerabilities.
- Report at most ten priority findings; never fill unused slots with generic advice.

### Read-only by default

The skills do not change product code, configuration, dependencies, infrastructure, or external services. They do not independently run destructive tests, real payments, external scans, or model calls. Only a user request for document output permits writing the two report files in a selected or new report directory.

## Installation

This directory is a **source suite** and is not installed automatically.

For project-level installation:

1. Open `skills/`.
2. Copy all 11 skill directories into the target project's `.claude/skills/` directory.
3. Preserve every directory name and internal path, especially the coordinator's `references/`.
4. Reload skills as required by the Claude Code version in use and confirm that the coordinator and specialists appear in the available skill list.

For personal installation, copy the same 11 directories into the personal skills directory. Installing only the coordinator leaves unavailable specialists `NOT_REVIEWED`, so install the complete suite.

## Usage

Run a complete production-readiness review:

```text
/production-readiness-review
```

Invoke a specialist directly when the scope is already clear:

```text
/readiness-payments-billing
```

Use the coordinator when applicability decisions, cross-module deduplication, and unified prioritization are needed.

## Bilingual output

- English skill entry: `SKILL.md`
- Chinese skill entry: `SKILL.zh-CN.md`
- Other English documents: `*.en.md`
- Other Chinese documents: `*.zh-CN.md`
- Coordinator file reports: `readiness-report.en.md` and `readiness-report.zh-CN.md`
- Direct specialist file reports: a module-specific pair of `.en.md` and `.zh-CN.md` files

Chinese and English reports must have identical route IDs, finding IDs, evidence IDs, counts, severity, confidence, ordering, and limitations. Translate prose only; keep paths, code, configuration keys, commands, and identifiers unchanged. Neither version may be a summary of the other.

Whenever a rule, template, or report changes, update its counterpart.

## Boundaries

This suite supports broad production-readiness review. It does not replace:

- A code review of a single change
- An authorized penetration test
- Legal, tax, regulatory, or certification conclusions
- Production migration, restore, failover, load, or alert drills
- Direct verification of private cloud settings, provider dashboards, and company procedures

Anything not actually performed must be marked unverified or unconfirmed.

## Maintenance checks

After changing the suite:

1. Confirm every skill has both language entry files and frontmatter names matching its directory.
2. Confirm coordinator module names and route IDs match specialist directories.
3. Confirm references resolve and English/Chinese sections and rules remain equivalent.
4. Confirm exclusion reasons, unknowns, and verification limits remain visible.
5. Confirm product edits, dependency installation, and external-service operations are not default behavior.
