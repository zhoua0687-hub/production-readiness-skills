---
name: readiness-identity-access
description: Review authentication, account recovery, MFA, sessions, authorization, tenant isolation, enterprise SSO/SAML/SCIM, login abuse defenses, and support impersonation. Use when a product has users, accounts, organizations, protected records, or enterprise identity requirements, or when the production-readiness router selects R-01.
---

# Identity and Access Review

Review only the identity and access surface that applies to this product. Do not require enterprise identity features for a local single-user tool without evidence of that requirement.

## Applicability

Use this skill for accounts, login, protected resources, roles, organizations, multiple customers, support access, or identity-related contract requirements. Exclusion requires affirmative product-scope evidence and appropriate source/configuration inspection; a missing login page alone is insufficient.

## Evidence to inspect

Trace actual login, recovery, logout, session, callback, provisioning, authorization, tenant, and support-access paths. Inspect relevant models, middleware, policies, queries, tests, identity-provider configuration, and available operational procedures. Private provider settings and offboarding records may require external evidence.

## Checks

### Authentication and recovery

- Valid email addresses, including plus-addressing and apostrophes, must survive normalization and lookup without silent mutation.
- Password storage and verification must use appropriate established mechanisms; secrets must never appear in logs.
- Reset links must be unguessable, expire, work once, and resist replay and account enumeration. Check invalidation after use and relevant credential changes.
- MFA must include a usable recovery path for a lost device, with protections against social engineering and unsafe bypasses.
- Sessions must have appropriate idle/absolute expiration, revocation, and a way to terminate all sessions for one user.

### Authorization and tenants

- Enforce permissions on the server or trusted execution boundary, not only by hiding controls.
- Roles must match real duties when the product needs more than administrator/member; do not invent complex RBAC without a requirement.
- Test object-level authorization against cross-user access by changed IDs, predictable identifiers, alternate routes, exports, and background jobs.
- Apply tenant constraints consistently to reads, writes, searches, caches, files, jobs, and administrative paths. A tenant filter in only the controller is not enough.
- Support “log in as user” functionality, if present or required, must be explicitly authorized, time-bounded, visibly marked, and audited on every use.

### Enterprise identity and abuse defenses

- SSO, SAML, and SCIM are requirement-driven. When applicable, inspect validation, signature handling, tenant mapping, replay defenses, deprovisioning, and failure behavior.
- SCIM or equivalent offboarding must promptly revoke access, including active sessions where the risk requires it.
- Login, reset, MFA, and recovery endpoints need appropriate rate limits and abuse monitoring.
- Lockouts must resist brute force without enabling trivial denial of service against executives or other targeted users. Check recovery and support procedures.

## Verification boundaries

Use only authorized local/test environments for dynamic tests. Do not guess passwords or attack external identity providers. Mark provider configuration, offboarding timing, session fleet revocation, and support procedures `UNCONFIRMED` without evidence.

## Output

Return findings using `finding_id`, `R-01`, severity, status, confidence, claim, risk scenario, evidence IDs/locations, validation performed, recommendation, and missing evidence. Separately list confirmed controls, unconfirmed items, and not-reviewed paths. Provide equivalent Chinese and English content; keep IDs, evidence, and conclusions identical. For document output, save `readiness-identity-access-report.en.md` and `readiness-identity-access-report.zh-CN.md` as a pair without overwriting existing reports. Do not modify product files.
