---
title: "web.dev — Performance — TTFB"
type: source
raw: raw/articles/web.dev — Performance — TTFB.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The web.dev reference for Time to First Byte, covering what TTFB measures (redirect time, DNS, TLS, service worker startup, plus request time to first response byte), its recommended thresholds, and measurement approaches in lab and field. TTFB is a diagnostic metric rather than a Core Web Vital.

## Key takeaways
- Good TTFB is 0.8 seconds or less; poor is above 1.8 seconds.
- TTFB is not a Core Web Vital — missing its threshold is acceptable if it doesn't impair FCP or LCP.
- Encompasses redirect time, service worker startup, DNS lookup, connection + TLS negotiation, and time to first response byte.
- SPAs need minimal TTFB for client-side rendering; server-rendered sites may have higher TTFB but better FCP/LCP.
- The 103 Early Hints status complicates measurement; Chrome 133 reverted `responseStart` to measure the final document response.
- Cross-origin resource TTFB requires `Timing-Allow-Origin` headers; cached primary-origin resources may return `responseStart` of 0.

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
> "TTFB is a metric that measures the time between starting navigating to a page and when the first byte of a response begins to arrive."

> "Most sites should strive to have a TTFB of 0.8 seconds or less"
