---
title: "web.dev — Performance — TBT"
type: source
raw: raw/articles/web.dev — Performance — TBT.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The web.dev reference for Total Blocking Time, a lab-only metric that sums the blocking portions of all Long Tasks (tasks >50ms) occurring after FCP. TBT is used as a proxy for INP in lab environments where real user interactions cannot be measured.

## Key takeaways
- Good TBT is less than 200ms on average mobile hardware.
- Blocking time per task = task duration minus 50ms; TBT is the sum of all such values after FCP.
- TBT is lab-only — field measurement is unreliable due to user interaction variance.
- Correlates strongly with INP but cannot replace field INP data.
- Better than Time to Interactive (TTI) at capturing user-perceived responsiveness: three 51ms tasks give 3ms TBT but push TTI far out.
- Optimization: reduce long tasks, reduce third-party code impact, minimize JavaScript execution time and main thread work.

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
> "the total amount of time after First Contentful Paint where the main thread was blocked for long enough to prevent input responsiveness"
