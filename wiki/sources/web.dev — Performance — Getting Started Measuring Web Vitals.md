---
title: "web.dev — Performance — Getting Started Measuring Web Vitals"
type: source
raw: raw/articles/web.dev — Performance — Getting Started Measuring Web Vitals.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A practical guide by Katie Hempenius on establishing a Web Vitals measurement strategy, covering both RUM (field) and lab data sources, their respective tools, and the key limitations of lab measurement for each Core Web Vital. Intended as a starting point for teams setting up Web Vitals monitoring.

## Key takeaways
- Field data is what Google uses to evaluate Core Web Vitals compliance; lab data is for development and CI/CD.
- Entry-level field tools: Chrome DevTools (integrates CrUX), PageSpeed Insights (28-day aggregate), Search Console (per-page historical), CrUX Vis (dashboard).
- The `web-vitals` library (~2KB) enables DIY RUM without manual browser API implementation.
- CrUX-based tools report with monthly granularity; PSI and Search Console show past 28 days.
- Lab limitations: LCP differs due to loading conditions; CLS is underreported (load-only); INP cannot be measured in lab at all — TBT is the recommended proxy.
- Lab tools: Chrome DevTools Performance panel, Lighthouse (LCP, CLS, TBT), WebPageTest.

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
