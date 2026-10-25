# ADR-0001: Detect abandoned carts with a 15-minute batch job

- **Status:** Accepted
- **Date:** 2026-10-25
- **Related principles:** P5 (freshness matched to need), P3 (measurable outcomes)

## Context
We want to remind customers who add products to the cart but don't check out.
We need to decide how quickly we detect an "abandoned" cart.

## Options considered
1. **Real-time streaming (Kafka + Flink):** a timer per cart, fires seconds after the threshold.
   - Pros: fastest reaction.
   - Cons: higher cost, more moving parts to run and monitor.
2. **Scheduled batch job every 15 minutes:** scans carts with no checkout in the last N minutes.
   - Pros: cheap and simple to build and operate.
   - Cons: a reminder can arrive up to 15 minutes later than it could.

## Decision
Option 2: a batch job every 15 minutes.

## Rationale
- It is the cheapest option.
- A customer who just added a product may still be browsing and adding other items.
  Waiting ~15 minutes gives them that time; if they still haven't bought, we send the reminder.
  Reacting within seconds adds cost without adding value for this use case.

## Consequences
- Reminder latency is up to ~15 minutes (acceptable, by design).
- If A/B tests show that faster reminders convert better, we can move to streaming later;
  the domain events (cart, checkout) are already published, so the switch stays possible.
