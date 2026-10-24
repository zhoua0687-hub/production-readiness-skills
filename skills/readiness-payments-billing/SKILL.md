---
name: readiness-payments-billing
description: Review money representation, charging, payment idempotency, subscriptions, proration, dunning, invoices, refunds, tax, usage metering, custom contracts, reconciliation, and payment-data scope. Use only when money, billing, pricing, or charging is in scope, or when the router selects R-04.
---

# Payments and Billing Review

Apply this skill when the product charges money or stores monetary amounts, even if a payment provider is not visible. Do not infer payment absence merely from missing provider keywords.

## Applicability

`NOT_APPLICABLE` requires affirmative no-payment/no-money product scope plus appropriate source, dependency, configuration, and entry-point inspection. Unknown billing integrations or incomplete product scope remain `UNCONFIRMED`. User-requested billing review always takes precedence.

## Evidence to inspect

Trace checkout, payment intent/state transitions, provider callbacks, subscription changes, invoice generation, credit/refund paths, usage collection, pricing/plan models, tax configuration, ledger/revenue reports, and reconciliation. Use sandbox or test evidence only; production provider settings and finance procedures need external records.

## Checks

### Money and transaction correctness

- Store money in integer minor units with an explicit currency, or an exact decimal representation appropriate to the domain. Account for zero-decimal and non-two-decimal currencies.
- Define rounding, tax, discounts, credits, and allocation rules for the markets actually served; do not invent global tax support without a sales footprint.
- Payment retries must use correctly scoped, persisted idempotency keys and safe response replay. Double-click prevention in the UI is not a substitute for server/provider idempotency.
- Model success, pending, failure, cancellation, timeout, and out-of-order/duplicate provider events without assuming one callback equals one completed charge.
- Verify that payment webhook signature and retry handling are coordinated with R-06, with one primary finding owner.

### Subscription and billing lifecycle

- Upgrades, downgrades, cancellations, renewal, proration, and plan changes must produce explainable amounts and consistent effective dates.
- Failed-payment retries and dunning must respect provider rules, customer communication preferences where applicable, and avoid accidental duplicate recovery attempts.
- Invoices must include required legal/tax fields and customer PO numbers when procurement contracts require them.
- Refunds, credits, and partial refunds must preserve auditability and reconcile with the original transaction.
- Usage metering must match billable quantities to the agreed precision, handle late/duplicate events, and provide a traceable path to the invoice.
- Annual or custom contracts must have an explicit representation or a controlled manual process; do not force unsupported terms through ordinary plan logic.
- Revenue reports must be reconcilable to invoices, payments, refunds, credits, taxes, and provider/finance records.

### Payment data scope

- Keep full card numbers and sensitive authentication data out of application databases and logs. Confirm hosted fields/tokenization and vendor data flows with evidence.
- PCI applicability, controls, and attestations are coordinated with R-10; a payment provider integration alone does not prove the product is out of PCI scope.

## Verification boundaries

Never create real charges, refunds, subscriptions, or customer credits for review. Use provider test modes only when explicitly authorized. Distinguish code paths from actual settlement, finance reconciliation, and tax determinations; professional tax/legal conclusions are outside what code alone can prove.

## Output

Return findings with `finding_id`, `R-04`, severity, status, confidence, claim, concrete financial scenario and amount/unit where known, evidence IDs/locations, validation, recommendation, and missing evidence. Keep confirmed controls and unknown finance/provider practices separate. Mirror Chinese and English content and IDs. For document output, save `readiness-payments-billing-report.en.md` and `readiness-payments-billing-report.zh-CN.md` as a pair without overwriting existing reports; never include cardholder data or modify payment state.
