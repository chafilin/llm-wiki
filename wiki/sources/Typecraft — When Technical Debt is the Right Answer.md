---
title: When Technical Debt is the Right Answer
type: source
raw: raw/articles/Typecraft — When Technical Debt is the Right Answer.md
date_ingested: 2026-05-07
tags: []
---

## Summary

Argues that technical debt isn't inherently bad — it's a tool that becomes harmful only when used without intention or a repayment plan. Uses Martin Fowler's Technical Debt Quadrant (Reckless/Prudent × Deliberate/Inadvertent) to distinguish strategic shortcuts from careless ones. The central question before incurring debt is "will this feature persist?"

## Key takeaways

- **Fowler's quadrant**: Reckless-Deliberate ("ship it, fix later") vs. Prudent-Deliberate ("we know the trade-off") vs. Reckless-Inadvertent ("we didn't know better") vs. Prudent-Inadvertent ("now we see the problem")
- **Omega messes** (Sandi Metz): ugly but contained code that's acceptable as a strategic trade-off — valid for disposable features, one-off campaigns, isolated internal tools
- **Three tiers of consequence**: The Good (upgradeable later — skip WebSockets, add later), The Bad (hidden friction that compounds — no retry logic, no pagination), The Ugly (entrenching — business logic in jobs, god methods)
- **Five questions before incurring debt**: deadline flexibility, feature criticality, evolution likelihood, refactoring cost, repayment timeline
- Debt should be documented with rationale and a scheduled repayment — not silently accumulated

## Connections

[[Technical Debt]] [[Software Development]] [[Complexity]]

## Quotes

> "Intentional debt serves as a speed tool rather than a liability when used strategically."
