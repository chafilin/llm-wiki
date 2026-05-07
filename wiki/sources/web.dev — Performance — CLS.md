---
title: "web.dev — Performance — CLS"
type: source
raw: raw/articles/web.dev — Performance — CLS.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The canonical web.dev reference for Cumulative Layout Shift, explaining how the metric quantifies visual instability using session windows, a layout shift score formula (impact fraction × distance fraction), and how to distinguish expected from unexpected shifts. Covers measurement tooling in both lab and field contexts.

## Key takeaways
- Good CLS is 0.1 or less; poor is above 0.25; evaluated at the 75th percentile.
- CLS uses the worst session window: a burst of shifts occurring within 1 second of each other, capped at 5 seconds total.
- Layout shift score = impact fraction × distance fraction; new elements or resizes only count if they cause existing elements to move.
- Shifts within 500ms of user interaction are flagged `hadRecentInput` and excluded from CLS.
- Use `transform: translate()` and `transform: scale()` instead of animating `top`/`left`/`height`/`width` to avoid layout shifts.
- Lab tools underreport CLS because they only capture page-load shifts; full lifecycle shifts require field measurement.

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
> "CLS measures the largest burst of layout shift scores for every unexpected layout shift that occurs during the entire lifecycle of a page."
