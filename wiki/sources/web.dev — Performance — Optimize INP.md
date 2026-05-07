---
title: "web.dev — Performance — Optimize INP"
type: source
raw: raw/articles/web.dev — Performance — Optimize INP.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A web.dev guide for diagnosing and improving INP by addressing each of its three components — input delay, processing duration, and presentation delay. Covers the diagnostic workflow (field RUM first, then lab reproduction) and concrete code patterns for yielding to the browser between tasks.

## Key takeaways
- Optimization workflow: field RUM data first → reproduce with DevTools → fix iteratively (fixing one slow interaction often reveals the next).
- Input delay stems from main thread blocking: script parsing/compilation, fetch handling, timers, and overlapping interactions.
- Break up event callback work with `requestAnimationFrame` + `setTimeout(fn, 0)` to let rendering occur between critical UI updates and deferred background work.
- Avoid layout thrashing: never update styles then immediately read layout values in the same task.
- Reduce presentation delay by flattening DOM size, adding elements lazily during interactions, and using `content-visibility` CSS for off-screen content.
- Client-rendered HTML during interactions blocks the browser until parsing completes — minimize volume.
- Each iframe has its own main thread; resource-constrained devices experience cross-thread impacts.

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
> "When rendering HTML through JavaScript, the browser won't yield until parsing completes."
