---
title: "web.dev — Performance — User-Centric Metrics"
type: source
raw: raw/articles/web.dev — Performance — User-Centric Metrics.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A framework article from web.dev establishing why performance measurement must be user-centric rather than purely technical. It organizes metrics around four questions (Is it happening? Is it useful? Is it usable? Is it delightful?) and introduces five metric categories covering perceived load speed, load responsiveness, runtime responsiveness, visual stability, and smoothness.

## Key takeaways
- "Performance is relative" — real user conditions (device, network) matter; lab testing alone is insufficient.
- Five metric categories map to distinct phases of the user experience, from first byte to smooth animations.
- Six core metrics to monitor: FCP, LCP, INP, TBT, CLS, TTFB — each measurable in lab and/or field.
- Custom metrics via lower-level APIs (User Timing, Long Tasks, Long Animation Frames, Element Timing, Navigation Timing, Resource Timing, Server Timing) cover site-specific needs.
- "No single metric is sufficient" — comprehensive evaluation requires multiple metrics across categories.

## Connections
[[Web Performance]], [[Core Web Vitals]]

## Quotes
> "performance is relative"

> "no single metric is sufficient"
