---
title: "web.dev — Performance — LCP"
type: source
raw: raw/articles/web.dev — Performance — LCP.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The canonical web.dev reference for Largest Contentful Paint, covering how LCP is defined, which element types qualify, how size is computed, and how to measure the metric in both field and lab environments. LCP addresses limitations of older load events by focusing on when the largest visible content element actually renders.

## Key takeaways
- Good LCP is 2.5 seconds or less; poor is above 4.0 seconds; measured at the 75th percentile.
- Qualifying element types: `<img>`, `<image>` inside SVG, `<video>` (poster or first frame), CSS background images, and block-level text containers.
- Size counts only the visible in-viewport portion; CSS margins/padding/borders are excluded.
- Browser stops reporting LCP candidates once the user interacts (tap, scroll, keypress).
- Cross-origin images need `Timing-Allow-Origin` header for accurate render timing; Chrome 133+ provides coarsened render time regardless.
- The `web-vitals` library handles edge cases (background tabs, bfcache, iframes, prerendering) automatically.

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
> "LCP reports the render time of the largest image, text block, or video visible in the viewport, relative to when the user first navigated to the page."

> "The browser will stop reporting new entries as soon as the user interacts with the page (via a tap, scroll, or keypress), as user interaction often changes what's visible to the user."
