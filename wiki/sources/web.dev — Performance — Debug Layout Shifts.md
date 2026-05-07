---
title: "web.dev — Performance — Debug Layout Shifts"
type: source
raw: raw/articles/web.dev — Performance — Debug Layout Shifts.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A web.dev debugging guide by Katie Hempenius and Barry Pollard covering the Layout Instability API and Chrome DevTools tooling for identifying and diagnosing layout shift causes. Walks through how to interpret shift attribution data, common triggers by category, and techniques for reproducing shifts reliably.

## Key takeaways
- The Layout Instability API underlies all CLS tooling; use `PerformanceObserver` with `type: 'layout-shift'` and `buffered: true`.
- `LayoutShift` entries expose `sources` (up to 5 elements), `value`, `hadRecentInput`, and `startTime`; `LayoutShiftAttribution` gives previous and current rects.
- Elements listed as shift sources may not be the root cause — they may be indirectly displaced by changes elsewhere.
- DevTools Performance panel: Layout Shifts track shows purple bars; diamond markers indicate individual shifts with size proportional to impact; click to see animated shift and highlighted elements.
- Enable "Layout Shift Regions" in DevTools Rendering settings to visually highlight shifting areas in real time.
- Direction heuristics: large downward shifts → DOM insertion; 1–2 pixel shifts → CSS conflicts or font swapping.
- Add `debugger` inside the PerformanceObserver callback to pause execution precisely when a shift fires.

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
