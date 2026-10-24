# Project Profile and Route Matrix

Complete this profile from evidence. Use `Unknown` where information is unavailable; do not fill gaps with guesses.

## Review context

| Field | Value | Evidence or limitation |
|---|---|---|
| Project and review question |  |  |
| Project root and available components |  |  |
| Review date and reviewer |  |  |
| User constraints and explicitly requested modules |  |  |
| Product type and supported platforms |  |  |
| Runtime and entry points |  |  |
| Users, roles, organizations, and tenants |  |  |
| Data stored or processed, including sensitive data |  |  |
| Charging, money values, subscriptions, or invoices |  |  |
| AI models, prompts, agents, or model providers |  |  |
| External APIs, webhooks, email, and OAuth |  |  |
| Deployment, hosting, CI/CD, and environments |  |  |
| Contracts, regions, regulatory obligations |  |  |
| Operational evidence outside the repository |  |  |
| Inspected paths and search scope |  |  |
| Unavailable components and access limitations |  |  |
| Dynamic verification performed or not performed |  |  |

## Routing rules

- `RUN`: a positive signal exists, or the user explicitly requested the module.
- `NOT_APPLICABLE`: affirmative scope evidence and technical inspection jointly support exclusion.
- `UNCONFIRMED`: available evidence is insufficient; record the gap and perform only bounded evidence-gap review when possible.
- Execution is tracked separately as `PENDING`, `COMPLETE`, or `NOT_REVIEWED`.

## Route matrix

Keep all rows and IDs. Add evidence IDs rather than pasting sensitive values.

| Route ID | Module | Decision | Positive signals and inspected evidence | Missing evidence | Reason | Execution |
|---|---|---|---|---|---|---|
| R-01 | `readiness-identity-access` |  |  |  |  | PENDING |
| R-02 | `readiness-application-security` |  |  |  |  | PENDING |
| R-03 | `readiness-data-reliability` |  |  |  |  | PENDING |
| R-04 | `readiness-payments-billing` |  |  |  |  | PENDING |
| R-05 | `readiness-ai-safety` |  |  |  |  | PENDING |
| R-06 | `readiness-integrations` |  |  |  |  | PENDING |
| R-07 | `readiness-operations` |  |  |  |  | PENDING |
| R-08 | `readiness-quality-maintainability` |  |  |  |  | PENDING |
| R-09 | `readiness-user-experience` |  |  |  |  | PENDING |
| R-10 | `readiness-compliance` |  |  |  |  | PENDING |

## Scope examples

- A complete local, single-user product with an explicit no-payment/no-AI scope and corroborating source, dependency, and configuration inspection may exclude R-04 and R-05 as `NOT_APPLICABLE`.
- Merely finding no payment keywords is `UNCONFIRMED`, not `NOT_APPLICABLE`.
- A repository without deployment evidence may still support code-level R-07 checks, but external backup, alert, and on-call practices remain `UNCONFIRMED`.
- A user-requested payment review is `RUN` even when no provider integration is visible; report the mismatch rather than silently refusing the requested scope.
