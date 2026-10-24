---
name: readiness-user-experience
description: Review weak-network behavior, loading/empty/error states, actionable errors, form preservation, email rendering, notification controls, undo, keyboard and screen-reader accessibility, localization, and predictable navigation. Use for products with user interfaces or customer communications and when the router selects R-09.
---

# User Experience and Accessibility Review

Test the flows and constraints that real users encounter. Do not require translations, email-client matrices, or formal accessibility certification unless the audience, contracts, and product surface justify them.

## Applicability

Use for graphical interfaces, CLI interaction where relevant, notifications, customer email, and user-facing navigation. A product with no user interface may exclude visual checks but still require actionable errors and accessible automation interfaces where applicable.

## Evidence to inspect

Inspect critical screens and flows, asynchronous states, error handling, forms, focus/navigation, semantic markup/native accessibility properties, localization and formatting, notification preferences, destructive actions, email templates, and performance-sensitive assets. Runtime behavior and assistive-technology support require actual execution evidence.

## Checks

### States, recovery, and performance

- Pages and critical interactions should remain usable under realistic latency, packet loss, offline transitions, and constrained devices. Use measured budgets based on the product rather than an arbitrary page-size rule.
- Every applicable screen needs deliberate loading, empty, error, and partial-data states. Avoid indefinite spinners and blank remote-content areas.
- Errors must explain what happened, whether data/action is safe, and what the user can do next. Do not expose secrets or internal stack traces.
- Validation failures must preserve other entered fields and make the failing field identifiable. Repeated submission should not lose work.
- Destructive or costly actions should support undo where the domain allows it; otherwise provide an appropriate confirmation and recovery path. Do not promise undo for irreversible external actions.

### Accessibility and localization

- Keyboard navigation must cover actions, menus, dialogs, lists, and focus restoration without traps. Screen readers need meaningful names, roles, states, ordering, and announcements.
- Check contrast, zoom/reflow, reduced motion, touch/pointer alternatives, and platform accessibility behavior according to the supported surfaces.
- Contractual accessibility requirements need an agreed standard and evidence from appropriate manual and automated testing; an ARIA attribute alone does not prove compliance.
- Translations, dates, times, numbers, currency display, pluralization, collation, and right-to-left layout should match supported locales. Do not translate technical identifiers or corrupt source data.

### Communication and navigation

- Notifications should have appropriate opt-out/preferences, while mandatory transactional or legal messages follow their own rules.
- Customer email should be tested in the clients actually used by customers, with readable fallbacks and links that remain usable.
- Back, Escape, close, cancel, and browser history must preserve user expectations and avoid accidental data loss or unexpected exits.

## Verification boundaries

Use available preview, browser, device, or accessibility tools when authorized and relevant. Do not claim screen-reader, email-client, old-device, or weak-network coverage from static inspection alone. Record viewport, platform, tooling, and untested clients.

## Output

Return findings with `finding_id`, `R-09`, severity, status, confidence, claim, concrete blocked/confused/data-loss user scenario, evidence IDs/locations, validation, recommendation, and missing evidence. Separate static observations from runtime verification and mirror both languages with identical IDs. For document output, save `readiness-user-experience-report.en.md` and `readiness-user-experience-report.zh-CN.md` as a pair without overwriting existing reports. Do not modify product files.
