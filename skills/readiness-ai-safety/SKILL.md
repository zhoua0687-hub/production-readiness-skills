---
name: readiness-ai-safety
description: Review AI and agent safety, including prompt injection, sensitive data leaving the network, model spend limits, evals, provider outage and deprecation plans, prompt/output logging, irreversible-action approval, and agent privileges. Use when models, prompts, embeddings, AI providers, or agents are present, or when the router selects R-05.
---

# AI Safety Review

Review the actual model and agent data flow rather than treating prompts as trusted code. Do not require AI controls when affirmative scope and technical evidence establish that no AI capability exists.

## Applicability

Use for hosted or local models, prompt templates, model APIs, agents, tool use, embeddings/RAG, AI-generated actions, or model-related billing. Missing SDK names alone are insufficient for exclusion because HTTP integrations may hide model calls.

## Evidence to inspect

Trace user and retrieved content into prompts, model requests/responses, tool calls, memory, logs, eval datasets, provider/model configuration, budgets, quotas, retries, fallbacks, and approval boundaries. Provider policies, BAAs, regional routing, production quotas, and eval results require external evidence when unavailable.

## Checks

### Untrusted content and sensitive data

- Treat every user-controlled, retrieved, emailed, uploaded, or tool-produced field that reaches a model as potentially hostile. Check instruction/data separation and whether model output can authorize actions.
- Prompt-injection defenses must be tested against the actual tools and data boundary. Do not claim a system prompt alone prevents injection.
- Customer, patient, secret, and other restricted data must not leave the approved network/provider path. Inspect context construction, logs, tracing, caching, fine-tuning, and third-party plugins, not just the visible prompt.
- Redaction and retention must match the data agreement and regulatory scope; coordinate BAA, residency, and deletion obligations with R-10.

### Cost, quality, and provider change

- Per-customer and global model budgets, token/request quotas, maximum agent steps, timeouts, and runaway-loop controls must match the pricing model and abuse risk.
- Cost alerts and spend visibility are coordinated with R-07. Verify actual enforcement rather than only dashboard estimates.
- Evals must represent important tasks, failure modes, and safety boundaries, with a baseline for detecting quality regressions after model, prompt, or retrieval changes.
- Provider outage behavior must be explicit: bounded retry, degraded functionality, fallback, or actionable failure. Do not claim resilience from an unused fallback configuration.
- Model deprecation and migration require version inventory, configuration ownership, compatibility evaluation, and a tested transition path.

### Actions and records

- Irreversible or high-impact actions require effective human approval at the transaction boundary. A dialog that an agent can bypass is not an approval control.
- Agent credentials and tools must be least-privilege and scoped to the current user/tenant; coordinate concrete privilege enforcement with R-02.
- Prompt/output/tool logs must support debugging while excluding prohibited data, limiting access and retention, and preserving enough context to investigate harmful actions.

## Verification boundaries

Do not send real customer data, secrets, or unauthorized prompts to external models. Do not incur model costs or execute agent tools without explicit approval. If evals, fallback tests, budgets, or provider settings were not exercised, report them as unverified.

## Output

Return findings with `finding_id`, `R-05`, severity, status, confidence, claim, concrete abuse/data-loss/cost/action scenario, evidence IDs/locations, validation, recommendation, and missing evidence. Separate confirmed controls and unknown provider behavior. Mirror Chinese and English content and IDs. For document output, save `readiness-ai-safety-report.en.md` and `readiness-ai-safety-report.zh-CN.md` as a pair without overwriting existing reports; do not change prompts, models, budgets, or agent state.
