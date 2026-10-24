---
name: readiness-operations
description: Review environment parity, infrastructure as code, deployment gates and rollback, zero-downtime delivery, queues, scheduling, caching, capacity, DNS/TLS, storage and cost controls, disaster recovery, observability, alerting, on-call, runbooks, postmortems, and status communication. Use for operated services or release operations and when the router selects R-07.
---

# Operations and Resilience Review

Adapt this review to the actual operating model. A distributed hosted service and a local desktop application have different deployment, recovery, and monitoring needs; do not require autoscaling, a second region, or an on-call rotation without a service-level requirement.

## Applicability

Use for deployed services, release pipelines, background work, production infrastructure, customer uptime commitments, or operational cost. Code-level evidence may support some checks while cloud configuration, alerts, drills, contracts, and staffing remain external evidence gaps.

## Evidence to inspect

Inspect environment/configuration boundaries, IaC, CI/CD, deployment and migration ordering, feature flags, worker/queue/cron code, cache usage, capacity configuration, DNS/TLS automation, lifecycle rules, budgets/alerts, logging/tracing setup, incident documents, runbooks, and status tooling. Do not assume a checked-in file reflects production state.

## Checks

### Environments and delivery

- Development, staging, and production should be reproducible and meaningfully comparable, with intentional configuration differences rather than unexplained drift.
- Infrastructure should be represented as reviewable code where infrastructure exists, including restoration of critical configuration.
- The delivery path must run relevant tests before release. Test ownership belongs to R-08; this skill checks enforcement and deployment behavior.
- Rollbacks must be practical under pressure and compatible with database/schema changes. Zero-downtime deployment requires backward-compatible transitions, health checks, and safe failure paths.
- Feature flags should separate code release from feature exposure where release risk justifies them, with lifecycle and stale-flag cleanup.

### Runtime work and capacity

- Slow work should move to appropriate background queues without losing execution guarantees. Retries need backoff/jitter, idempotency awareness, and a dead-letter or equivalent intervention path.
- Scheduled work must remain safe with multiple instances through locking, leader election, uniqueness, or idempotent execution.
- Caches need explicit invalidation/versioning and correctness behavior when source data changes.
- Autoscaling and capacity limits should match real load and downstream bottlenecks. CDN and geographic delivery are requirement-driven, not universal.
- DNS, certificates, and renewals need monitored ownership and expiry protection; verify actual external configuration before claiming coverage.
- Lifecycle rules should remove obsolete temporary/storage data according to retention requirements. Budget and cost alerts must detect runaway services or agent loops promptly enough to act.

### Recovery, telemetry, and incident response

- Disaster recovery needs written scope, owners, recovery objectives, and periodic tested recovery. A second region is required only when availability commitments or risk demand it.
- Logs must be structured, searchable, correlated, and useful during incidents without sensitive payloads; coordinate redaction with R-02.
- Error tracking should group related failures and preserve actionable context. External uptime checks must exercise the customer path beyond the internal network where service commitments apply.
- Dashboards should cover relevant latency, error rate, throughput, saturation, and queues. Tracing should connect slow requests across actual service boundaries.
- Alerts should reach a accountable human, have actionable thresholds, and be tuned using evidence. On-call ownership, escalation, runbooks, and response expectations require operational confirmation.
- Postmortems should produce tracked changes, not only narratives. A customer status page should reflect real incident ownership and communication needs.

## Verification boundaries

Do not deploy, roll back, failover, scale, purge storage, trigger pages, or alter DNS/TLS during review without explicit authorization. Distinguish configuration review from executed restore, failover, alert, and rollback tests. External operational items without evidence are `UNCONFIRMED`.

## Output

Return findings with `finding_id`, `R-07`, severity, status, confidence, claim, concrete outage/recovery/cost scenario, evidence IDs/locations, validation, recommendation, and missing evidence. Separate code-level controls from external operational practices and mirror both languages with identical IDs. For document output, save `readiness-operations-report.en.md` and `readiness-operations-report.zh-CN.md` as a pair without overwriting existing reports. Do not change infrastructure or runtime state.
