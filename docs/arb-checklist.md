# ARB Checklist: Marketing Automation with AI & Agents

Use before any use case goes to production. Each item needs an owner and evidence (link, doc or screenshot).

| # | Area | Check | Evidence |
|---|---|---|---|
| 1 | Business | Problem, baseline and target metric written; A/B test plan exists | |
| 2 | Business | Non-goals and scope for this phase agreed with the sponsor | |
| 3 | Data & compliance | All customer data stored and processed in-country (at rest and in transit) | |
| 4 | Data & compliance | PII fields identified; masked or removed before any model/LLM call | |
| 5 | Data & compliance | Retention policy applied (customer data kept ≥ 5 years, then deleted) | |
| 6 | Data | Meaning and source of every model input checked (provenance/semantics) | |
| 7 | AI safety | Guardrails on every customer-facing AI output (toxicity, PII leak, prompt injection) | |
| 8 | AI safety | Human approval step for agent actions that reach customers | |
| 9 | AI quality | Offline eval + online metric defined; LLM-as-judge / evals in LangFuse | |
| 10 | Security | Internal systems behind VPN; external calls over HTTPS with auth (JWT/TLS 1.2+) | |
| 11 | Security | Secrets/API keys in a vault, not in code; security survey signed off | |
| 12 | Operations | SLOs set and load-tested in pre-prod (availability, P50/P95 latency, RPS) | |
| 13 | Operations | Logs, metrics, traces and alerts in place (Grafana, Loki, Prometheus) | |
| 14 | Operations | DR site in-country and failover tested | |
| 15 | Cost | Freshness (real-time / near-real-time / batch) justified per use case; monthly cost estimated | |
| 16 | Decisions | Every major decision has an ADR, linked from the design doc | |

**Verdict:** Approved / Approved with conditions / Rejected · **Reviewer:** · **Date:**
