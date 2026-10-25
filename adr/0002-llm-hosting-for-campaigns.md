# ADR-0002: Route campaign LLM calls by data classification

- **Status:** Accepted
- **Date:** 2026-10-25
- **Related principles:** P1 (data stays in-country), P2 (guardrails on AI output)

## Context
An LLM writes the text for marketing campaigns. The company operates in Saudi Arabia,
so personal data (PII) must not leave the country (PDPL). External LLM APIs are stronger
and easier to use, but may process data outside the country.

## Options considered
1. **Self-hosted open-source model in-country only:** fully compliant, but needs GPUs and an ops team; quality may be lower.
2. **External LLM API only:** best quality and least effort, but PII could leave the country.
3. **Hybrid, routed by data classification:** external API when no restricted data is involved; self-hosted model otherwise.

## Decision
Option 3, the hybrid:
- A **PII / classification filter runs automatically before every LLM call**.
- If the request has **no personal data**, and compliance allows that data class to leave the country, it may use the **external API**.
- If it **contains personal data**, or the data may not leave the country, it goes to the **self-hosted open-source model**.
- **Fail-safe:** when the filter is unsure, route to the self-hosted model.
- **Templates:** the external model writes messages with placeholders (e.g. `{name}`, `{product}`);
  real customer values are filled in **inside the country** after the response returns.

## Rationale
Most campaign text is segment-level and needs no personal data, so it can use the stronger API.
Anything personal stays in-country, which keeps us PDPL-compliant.

## Consequences
- We run and maintain two LLM paths plus a classification filter.
- Which data classes may leave the country is decided and documented by compliance/legal, not by the engineering team.
- The filter's misses must be monitored (sample review in LangFuse).
