---
title: "web.dev — Performance — INP"
type: source
raw: raw/articles/web.dev — Performance — INP.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The canonical web.dev reference for Interaction to Next Paint, the stable Core Web Vital that replaced FID. INP measures overall page responsiveness by observing latency for all click, tap, and keyboard interactions throughout the page lifetime, reporting the worst case while ignoring statistical outliers.

## Key takeaways
- Good INP is ≤200ms; needs improvement is 200–500ms; poor is >500ms; measured at 75th percentile.
- "90% of a user's time on a page is spent after it loads" — responsiveness throughout the lifecycle matters, not just at load.
- An interaction's latency = input delay + processing duration + presentation delay.
- INP measures clicks, taps, and keypresses only — scrolling, hovering, and zooming are excluded.
- INP improves on FID by covering all interactions, not just the first one.
- Events under 104ms don't report by default; iframe interactions count for the metric but not the API.

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
> "90% of a user's time on a page is spent _after_ it loads"

> An interaction's latency consists of the time "from when user interaction occurs...to the next time the rendering...is updated."
