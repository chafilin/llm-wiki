---
title: "web.dev — Performance — Defining Core Web Vitals Thresholds"
type: source
raw: raw/articles/web.dev — Performance — Defining Core Web Vitals Thresholds.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A methodological paper by Bryan McQuade and Barry Pollard explaining how Google selected the specific threshold values for LCP, INP, and CLS. Thresholds were chosen by balancing quality of user experience (grounded in HCI research), achievability (at least 10% of origins must pass), and device considerations (same thresholds for mobile and desktop).

## Key takeaways
- Three criteria for threshold selection: high-quality user experience, achievability (≥10% of origins meet "good"), and parity across mobile and desktop.
- 75th percentile was chosen to balance majority coverage while dampening outlier impact.
- LCP threshold of 2.5s derived from HCI research on response time expectations (Card and Miller: "roughly 0.3–3 seconds").
- INP threshold of ≤200ms reflects research showing delays over 200ms break the perceived causal link between action and response.
- CLS threshold of ≤0.1 derived from empirical observation: shifts ≥0.15 were consistently perceived as disruptive; ≤0.1 was noticeable but not excessively so.
- Authors acknowledge thresholds are not perfect: "there is often no single 'correct' threshold."
- "Many sites would benefit from optimizing even beyond the 'good' thresholds."

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
> "the criteria were sometimes in conflict with one another"

> "Many sites would benefit from optimizing even beyond the 'good' thresholds and should seek to correlate with their individual business metrics."
