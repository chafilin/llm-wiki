---
title: "web.dev — Performance — Optimize CLS"
type: source
raw: raw/articles/web.dev — Performance — Optimize CLS.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A web.dev guide covering the four most common causes of CLS — images without dimensions, ads/embeds without reserved space, dynamically injected content, and web fonts — with concrete solutions for each. Highlights the difference between lab measurement (load-only) and field measurement (full page lifecycle).

## Key takeaways
- Always set `width` and `height` attributes on `<img>` tags; modern browsers use these to reserve space via automatic aspect-ratio CSS.
- Reserve space for ads and dynamic content using `min-height` or `aspect-ratio` CSS; place late-loading content below the fold.
- Use `transform: translateY()` not `top`/`left` for animations to avoid layout shifts even on promoted layers.
- Use `font-display: optional` to prevent font-swap layout shifts; use `ascent-override`/`descent-override` CSS to match fallback font metrics.
- Preload critical fonts with `<link rel="preload">` to reduce the window for font-swap shifts.
- Pages eligible for bfcache restore instantly without reload-induced layout shifts — enabling bfcache is a CLS improvement strategy.

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
> "CLS is measured throughout the full life of the page and not just during the initial page load."
