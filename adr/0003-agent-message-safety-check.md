# ADR-0003: Run the safety check on agent messages inline

- **Status:** Accepted
- **Date:** 2026-10-25
- **Related principles:** P2 (guardrails on AI output), P4 (human approval for agent actions)

## Context
The campaign agent generates messages that are sent to customers (WhatsApp/SMS).
We must decide where the safety check (toxicity, wrong offers, PII leaks, prompt injection) runs.

## Options considered
1. **Inline:** the message cannot be sent until it passes the check.
   - Pros: bad messages never reach customers.
   - Cons: adds a few seconds of latency.
2. **Out-of-band:** the message is sent immediately and checked afterwards.
   - Pros: no added latency.
   - Cons: a bad message may already have reached customers before we catch it.

## Decision
Option 1: inline.

## Rationale
- A few seconds of delay makes no real difference when building a campaign.
- A wrong or offensive message sent to customers can cost us a lot and cannot be taken back.

## Consequences
- Every campaign message waits for the check; the check must stay fast and highly available.
- Messages that fail are blocked and routed to a human for review.
- Out-of-band monitoring (sampling in LangFuse) can still be added on top for quality trends.
