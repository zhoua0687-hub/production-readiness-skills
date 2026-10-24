---
name: readiness-application-security
description: Review application and data security, including exposed secrets, dependency provenance, server validation, OWASP risks, URL/WebView boundaries, uploads, CORS, headers, encryption, least privilege, sensitive logging, vulnerability disclosure, and device-loss readiness. Use for most networked or input-handling products and when the router selects R-02.
---

# Application Security Review

Select controls that match actual inputs, execution boundaries, data, and deployment. Do not prescribe server headers or CORS for a product with no HTTP server, and do not turn generic best practices into confirmed vulnerabilities.

## Applicability

Use for user input, remote content, network requests, local privileged operations, stored data, dependencies, secrets, files, or browser/WebView behavior. If the product is entirely static and local, narrow the review to its real supply-chain, input, and privilege boundaries.

## Evidence to inspect

Inspect manifests and lockfiles, environment templates, secret handling, request handlers, validation, serializers, templates, SQL/query construction, browser/WebView setup, upload/storage paths, HTTP middleware, IAM/configuration, and logging. Repository history, CI scanning, cloud encryption/IAM, key rotation, disclosure, and device procedures require evidence when available.

## Checks

### Secrets and dependencies

- Search appropriate source and configuration scope for embedded credentials without exposing their values. Repository history and AI chat history are `UNCONFIRMED` unless actually provided and inspected.
- Check rotation procedures for keys that may have been pasted into configuration or chats; do not claim rotation occurred from code alone.
- Confirm package names, sources, lockfile integrity, and signs of typosquatting or accidental packages. Use existing dependency scanning where safely available; do not install unrequested tools.

### Input and execution boundaries

- Validate and authorize on the trusted boundary, not only in forms. Prefer structured validation and context-appropriate output encoding over blanket “sanitization”.
- Trace SQL/query parameters, HTML/DOM rendering, redirects, cookies, CSRF defenses, request forgery, path handling, deserialization, and command execution where those sinks exist.
- For user-supplied URLs, WebViews, iframes, or remote content, inspect scheme/host policy, local-network and local-file access, redirects, navigation, JavaScript bridges, sandbox flags, and credential sharing. A sandbox attribute alone is not proof of safety.
- Uploads, when applicable, need type/content checks, malware scanning where required, size limits, safe names/paths, authorization, and storage that cannot execute uploaded content.

### Platform and data protection

- CORS must reflect real origins and credentials behavior. Security headers must cover applicable HTTP responses, including errors, without breaking the product indiscriminately.
- Verify TLS and encryption-at-rest claims using actual client, server, and platform evidence. Cloud settings outside the repository remain unconfirmed without records.
- Apply least privilege to users, services, CI, support, and AI agents. Check production credential scope and separation rather than assuming sandbox labels prove isolation.
- Audit/security logs should capture meaningful actor and action context while excluding passwords, tokens, keys, card numbers, and unnecessary sensitive payloads.
- Vulnerability disclosure and stolen-device response require accessible procedures, credential revocation, and evidence of ownership; absence from the repository is not proof of absence.

## Verification boundaries

Do not run exploitative payloads against external systems or access real secrets to prove they work. Use non-destructive local tests only when authorized. Distinguish code inspection, scanner results, runtime response inspection, and external operational evidence.

## Output

Return findings with `finding_id`, `R-02`, severity, status, confidence, concrete risk scenario, evidence IDs/locations, validation, recommendation, and missing evidence. Keep confirmed controls, unknowns, and not-reviewed items separate. Mirror Chinese and English content and IDs. For document output, save `readiness-application-security-report.en.md` and `readiness-application-security-report.zh-CN.md` as a pair without overwriting existing reports. Never include secret values and never modify product files.
