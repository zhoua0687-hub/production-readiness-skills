---
name: readiness-compliance
description: Review evidence for penetration testing, enterprise security questionnaires, SOC 2, HIPAA and BAAs, view/change audit trails, PCI scope, GDPR deletion, data residency, access reviews, and terms/privacy alignment. Use according to data, customers, contracts, regions, and regulatory scope, or when the router selects R-10.
---

# Compliance and Assurance Review

Determine obligations from actual data, customers, contracts, regions, and vendors. Do not require every framework for every product, and never declare legal compliance or certification from source code alone.

## Applicability

Use when regulatory, contractual, enterprise procurement, sensitive-data, audit, residency, or legal-policy questions apply. A local product may still have privacy or distribution obligations. External records are necessary for many checks; missing repository documents alone justify `UNCONFIRMED`, not a finding of noncompliance.

## Evidence to inspect

Inspect data-flow maps, inventory/classification, contracts and DPAs, vendor/subprocessor lists, policies, audit reports, penetration-test reports, questionnaire responses, risk registers, retention/deletion workflows, audit schemas, access-review records, terms/privacy text, and relevant implementation paths. Handle all evidence as potentially confidential.

## Checks

### Assurance and enterprise evidence

- Penetration testing should match product exposure and customer requirements. Verify scope, date, tester independence where required, remediation, and retesting; do not run or claim a penetration test from a checklist review.
- Security questionnaire answers need current, traceable evidence and owners. Do not turn aspirations or planned controls into affirmative answers.
- SOC 2 requires defined controls, operating evidence, and an independent auditor when applicable. A policy folder or checkbox is not an attestation.
- Vulnerability disclosure and device-loss processes are technically reviewed with R-02; here check contractual evidence and ownership only where needed.

### Sensitive data and audit

- HIPAA applies when protected health information and covered-entity/business-associate relationships require it. Do not wait for a UI feature to identify PHI; trace actual data.
- BAAs must cover every applicable vendor touching PHI, including model, logging, support, analytics, and hosting providers where relevant.
- Audit trails should capture required record views as well as changes, with actor, tenant, timestamp, purpose/context where required, integrity, retention, and restricted audit-log access.
- PCI scope must follow real card data flows. Keep prohibited card data out of databases/logs and obtain current scope evidence; coordinate implementation findings with R-04.

### Privacy, residency, and governance

- GDPR or contractual deletion workflows must identify every applicable primary, derived, file, cache, log, backup, vendor, and model-data location. Address backup expiry and restored-data deletion honestly rather than claiming impossible immediate erasure.
- Data residency must include primary and disaster-recovery storage, logs, telemetry, support exports, subprocessors, and AI/provider routing when contracts restrict geography.
- Access reviews need a defined cadence when required, appropriate reviewers, evidence of decisions, revocation follow-through, and sign-off. Quarterly reviews are not universal unless policy or contract requires them.
- Terms and privacy policies must match actual collection, use, sharing, retention, deletion, AI/provider processing, and customer rights. Identify mismatches without presenting a code review as legal advice.

## Verification boundaries

Do not access confidential audit material beyond the authorized scope or copy personal/patient/card data into the report. Legal, regulatory, certification, and auditor conclusions require qualified owners and external evidence. Clearly separate implemented technical controls from organizational effectiveness evidence.

## Output

Return findings with `finding_id`, `R-10`, severity, status, confidence, claim, concrete exposure/contract/audit scenario, evidence IDs/locations, validation, recommendation, and missing evidence. List required external evidence and avoid unsupported compliance verdicts. Mirror Chinese and English content and IDs. For document output, save `readiness-compliance-report.en.md` and `readiness-compliance-report.zh-CN.md` as a pair without overwriting existing reports; do not modify product or compliance records.
