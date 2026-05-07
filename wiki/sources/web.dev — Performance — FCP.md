---
title: "web.dev — Performance — FCP"
type: source
raw: raw/articles/web.dev — Performance — FCP.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The web.dev reference for First Contentful Paint, which marks the point in the load timeline when any content first becomes visible to the user. Covers qualifying content types, performance targets, measurement tools, and optimization strategies.

## Key takeaways
- Good FCP is 1.8 seconds or less; poor is above 3.0 seconds; measured at 75th percentile across mobile and desktop.
- Qualifying content: text, images (including backgrounds), SVG, and non-white canvas elements.
- FCP includes unload time from previous pages, connection setup, redirects, and TTFB — field data will differ from lab data because of this.
- Optimization levers: eliminate render-blocking resources, minify/remove unused CSS and JS, preconnect to required origins, reduce TTFB, avoid redirects, minimize DOM size, and use efficient cache policies.
- Use the Paint Timing API with `PerformanceObserver` or the `web-vitals` library (which handles background tabs, bfcache, and prerendered pages).

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
> "FCP marks the first point in the page load timeline where the user can see anything on the screen."
