---
title: "web.dev — Performance — Custom Metrics"
type: source
raw: raw/articles/web.dev — Performance — Custom Metrics.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A web.dev guide to measuring site-specific performance needs that standard metrics cannot capture, covering the browser APIs available for custom instrumentation. Emphasizes using event-driven PerformanceObserver rather than polling APIs, and avoiding measurement code that itself causes performance issues.

## Key takeaways
- Custom metrics cover SPA page transitions, hydration completion, cache hit rates, event latency for interactive apps, and other site-specific signals.
- PerformanceObserver is the correct foundation — callbacks fire during idle periods, minimizing overhead; use `buffered: true` to catch entries before observer initialization.
- User Timing API (`performance.mark` / `performance.measure`) handles arbitrary time intervals.
- Long Tasks API (Chrome 58+) identifies main thread blocking tasks >50ms; superseded by Long Animation Frames API (Chrome 123+) which provides better attribution.
- Element Timing API lets you mark specific elements with `elementtiming` attribute to measure their render time.
- Event Timing API tracks interaction latency for click and keyboard events.
- "The first rule of effective performance measurement is to make sure your performance measurement techniques aren't causing performance issues themselves."

## Connections
[[Web Performance]], [[Core Web Vitals]]

## Quotes
> "The first rule of effective performance measurement is to make sure your performance measurement techniques aren't causing performance issues themselves."
