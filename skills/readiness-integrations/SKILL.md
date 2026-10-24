---
name: readiness-integrations
description: Review third-party API resilience, webhooks, OAuth refresh, API versioning, customer API keys, integration rate limits, sandboxes, and transactional email authentication and suppression. Use for external API, callback, OAuth, public API, or email dependencies and when the router selects R-06.
---

# Integrations Review

Review actual external dependencies and customer-facing integration surfaces. Do not require a public API, sandbox, or developer platform when the product has no such requirement.

## Applicability

Use for outbound/inbound APIs, webhooks, OAuth, partner services, customer API keys, integration credentials, or transactional email. Payment-specific money consequences belong to R-04 and queue infrastructure to R-07; this skill owns integration authenticity, contracts, and delivery behavior.

## Evidence to inspect

Inspect HTTP clients, timeouts, serializers, schemas, callbacks, signature middleware, API routers, key storage, OAuth token stores, refresh jobs, retry logic, delivery logs, provider configuration, sandbox support, and email send/suppression paths. DNS, provider dashboards, suppression lists, and external delivery records require external evidence.

## Checks

### Third-party APIs and OAuth

- Requests need appropriate timeouts, bounded retries with backoff/jitter, cancellation, and idempotency awareness so one flaky call does not become a lost or duplicated operation.
- Response parsing must handle optional fields, errors, pagination, and schema evolution deliberately. Contract/integration tests and provider change monitoring should match the dependency's criticality.
- OAuth tokens need secure storage, expiry handling, refresh before failure, concurrency control, revoked-token handling, and reauthorization paths.
- A sandbox or test environment is required only when customers or partners need to test integrations; verify realistic behavior and separation from production.

### Webhooks and customer APIs

- Incoming webhooks must verify authentic signatures over the correct payload, with timestamp/replay defenses and secret rotation where supported.
- Callback processing must handle duplicates, ordering, timeouts, and retries safely. Outgoing webhooks need bounded retries and a durable record of failed deliveries/dead letters when offered.
- Public APIs need deliberate versioning and compatibility policy so changes do not silently break existing integrations.
- Customer API keys must be creatable, revocable, scoped, stored safely, shown only as appropriate, and covered by audit logs without exposing key material.
- API rate limits must protect shared resources while accounting for bursts, retries, and legitimate integration workloads; responses should help clients recover.

### Transactional email

- SPF, DKIM, and DMARC must be checked against the actual sending domains and providers. A code library or environment variable does not prove DNS is correct.
- Bounce and complaint events must update suppression/delivery behavior where required, especially for password resets and billing notices.
- Check sender/domain ownership, unsubscribe or preference obligations by message type, delivery monitoring, and actionable handling of persistent provider failures.

## Verification boundaries

Do not trigger real provider callbacks, emails, OAuth grants, or external load without authorization. Use recorded fixtures and authorized test/sandbox environments. Mark external DNS, provider configuration, and actual delivery behavior unconfirmed when not inspected.

## Output

Return findings with `finding_id`, `R-06`, severity, status, confidence, claim, concrete lost/duplicate/insecure integration scenario, evidence IDs/locations, validation, recommendation, and missing evidence. Keep provider-side unknowns separate and mirror both languages with identical IDs. For document output, save `readiness-integrations-report.en.md` and `readiness-integrations-report.zh-CN.md` as a pair without overwriting existing reports. Do not modify integration configuration or send real events.
