# AI Architecture Portfolio

Portfolio for the **AI Architecture Design** course (MLOps MENA, Eng. Sameh Amin, Oct–Dec 2026).
Each session adds a layer to one running design: an AI and agent platform for marketing automation at an e-commerce company.

## Scenario

<!-- TODO: rewrite this section in your own words. -->
An e-commerce company wants to use AI and agents to automate and personalise its marketing.
Use cases in scope:

1. Homepage personalisation
2. Next-best action / abandoned-cart recovery
3. Churn prediction
4. Cold start for new customers and products
5. Agentic campaign automation

## Assumptions

<!-- TODO: review, edit and add your own. -->
- The company operates in Saudi Arabia, so customer data must stay in-country (PDPL / data residency).
- Business goals: <!-- TODO: e.g. CSAT from X% to Y%, conversion from A% to B% -->
- Existing systems: <!-- TODO: from your as-is diagram -->

## How to read this repo

| Folder | What's inside |
|---|---|
| `docs/` | One design doc per session (`01-framing.md`, `02-building-blocks.md`, …) |
| `diagrams/` | Exported PNG/SVG plus the draw.io source files |
| `adr/` | Architecture Decision Records, one decision per file (`0001-….md`) |
| `capstone/` | Final architecture PDF and slides |

Start with `docs/01-framing.md`, then read the ADRs it links to.

## Progress

- [x] Session 1: Architecture views, steps and process ([Mini Project 1: Governance Pack](docs/mini-project-1-governance.md))
- [ ] Session 2: AI system building blocks
- [ ] Session 3: LLM & RAG architecture
- [ ] Session 4: Agentic AI architecture
- [ ] Session 5: Security, governance, evals
- [ ] Session 6: Enterprise case studies
- [ ] Capstone
