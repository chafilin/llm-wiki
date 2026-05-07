---
title: "web.dev — Performance — Optimize LCP"
type: source
raw: raw/articles/web.dev — Performance — Optimize LCP.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A comprehensive web.dev guide to optimizing LCP by breaking the metric into four sequential subparts — TTFB, resource load delay, resource load duration, and element render delay — and providing concrete fixes for each. The article establishes that the vast majority of LCP time should be spent on the HTML document and the LCP resource itself; any other time is waste.

## Key takeaways
- LCP breaks into four subparts: TTFB (~40%), resource load delay (<10%), resource load duration (~40%), element render delay (<10%).
- Eliminate resource load delay: make the LCP image discoverable in initial HTML, use `fetchpriority="high"`, never use `loading="lazy"` on the LCP element, preload CSS background images and web fonts.
- Eliminate render delay: avoid render-blocking stylesheets and sync scripts in `<head>`, use SSR so image URLs appear in HTML source, break up long main-thread tasks.
- Reduce resource load duration: serve correct image sizes, use modern formats (WebP, AVIF), use CDNs, compress aggressively.
- Reduce TTFB: eliminate redirects, ensure CDN edge caching works, avoid unique URL parameters that bust cache.
- "Nothing can happen on the frontend until the backend delivers that first byte of content."

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
> "The vast majority of the LCP time should be spent loading the HTML document and LCP source. Any time before LCP where one of these two resources is not loading is an opportunity to improve."

> "Nothing can happen on the frontend until the backend delivers that first byte of content, so anything you can do to speed up your TTFB will improve every other load metric as well."
