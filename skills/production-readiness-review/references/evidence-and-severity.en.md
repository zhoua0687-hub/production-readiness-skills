# Evidence, Status, and Severity

## Evidence rules

1. Anchor claims to reviewable evidence: `path:line`, a configuration key, a schema or migration, a test name and result, a command result, or an identified external record.
2. Assign evidence IDs (`E-001`, `E-002`, …) and reuse them in both languages. Redact secrets and sensitive values.
3. Separate direct observation from inference. Explain any inference and do not present it as a verified fact.
4. A repository can support code-level conclusions but usually cannot prove backup restores, penetration tests, on-call response, access reviews, certifications, contracts, or account ownership.
5. Missing documentation is not proof that an operational practice does not exist. A policy document alone is not proof that the practice operates effectively.
6. Record what was searched and what was unavailable. Do not claim dynamic verification that was not run.

## Check statuses

| Status | Meaning |
|---|---|
| `CONFIRMED_ISSUE` | Evidence supports a concrete defect or missing required control. |
| `CONFIRMED_CONTROL` | Evidence supports that a relevant control exists; this is not a guarantee against all bypasses. |
| `NOT_APPLICABLE` | The item is outside the established product or contract scope, with a reason. |
| `UNCONFIRMED` | Evidence is insufficient to decide; identify the exact missing evidence. |
| `NOT_REVIEWED` | The item or module was not examined; explain the execution limitation. |

Do not count `UNCONFIRMED` or `NOT_REVIEWED` as passes. Do not automatically count them as vulnerabilities either.

## Severity model

Severity reflects impact in the actual product context, not checklist importance.

| Severity | Use when |
|---|---|
| Critical | A credible immediate path to broad data compromise, major financial loss, unrecoverable data loss, or prolonged core-service outage requires urgent action. |
| High | A realistic scenario can cause material data exposure, unauthorized action, financial error, significant outage, or failed recovery. |
| Medium | A meaningful reliability, security, compliance, or financial weakness requires preconditions or has bounded impact. |
| Low | Limited operational, UX, or maintainability impact with no credible severe scenario identified. |
| Info | A contextual note or improvement that is not a defect. Keep it outside the priority-finding count. |

Use `High`, `Medium`, or `Low` confidence separately from severity. Unknowns remain unknowns; confidence labels must not turn them into confirmed findings.

## Finding record

Every confirmed issue uses these fields:

```text
finding_id
module / route_id
severity
status
confidence
claim
risk_scenario
evidence_ids and locations
validation_performed
recommendation
missing_evidence
```

The risk scenario must connect an actor or event to a concrete product impact. The recommendation should address the demonstrated cause without inventing unrelated features.

## Priority order

Sort confirmed findings by severity first, then realistic likelihood, blast radius, reversibility, and evidence confidence. Show at most ten priority findings. Do not fill unused slots with generic advice.

Confirmed controls, lower-priority observations, unknowns, skipped modules, and execution limitations have separate report sections.

## Bilingual parity

Both reports must contain the same route IDs, finding IDs, evidence IDs, counts, severity, confidence, ordering, locations, and limitations. Translate explanatory prose only. If one version changes, update the other before delivery.
