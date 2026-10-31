# ADR-0004: Serve "Frequently bought together" from a precomputed top-K list

- **Status:** Accepted
- **Date:** 2026-10-31
- **Related principles:** P5 (freshness matched to need), P3 (measurable outcomes)

## Context
At checkout we show 4 items often bought with the items in the cart.
The page must meet P95 500 ms at 1000 RPS, and checkout must never be slowed by heavy reads on the operational DB.

## Options considered
1. **Precomputed top-K per item:** nightly Airflow job on CDP data writes `fbt_top10` per item to the online feature store; the recommender only reads and merges.
2. **Real-time vector DB query:** embed the cart, ANN search in the vector DB, rank with online features on every request.
3. **Co-purchase SQL on the operational DB** at request time.

## Decision
Option 1.

## Rationale
- Latency: a key lookup (~10 ms) vs. ~100 ms for embed + ANN + rank.
- Cost: one nightly job and a small Redis footprint vs. a vector DB sized for checkout traffic.
- Ops DB load: none (reads go to the CDP). Option 3 would put heavy joins on the same DB that serves checkout.
- Quality: co-purchase gives complements (phone → case). Vector similarity gives substitutes (phone → other phone), which is the wrong answer for this widget.
- Co-purchase patterns change slowly, so daily freshness is enough.

## Consequences
- New products have no list until they collect orders: fall back to category best-sellers; later (v2) borrow lists from similar items via the vector DB in batch.
- Promotions that start today show up in lists tomorrow (acceptable).
- We must add event tracking for widget impressions and clicks to measure uplift with an A/B test.
