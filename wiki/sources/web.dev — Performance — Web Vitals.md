---
title: "web.dev — Performance — Web Vitals"
type: source
raw: raw/articles/web.dev — Performance — Web Vitals.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The top-level web.dev overview of Google's Web Vitals initiative, defining the three stable Core Web Vitals (LCP, INP, CLS), their thresholds, and the metric lifecycle (experimental → pending → stable). Serves as the authoritative entry point into the Web Vitals ecosystem.

## Key takeaways
- Three Core Web Vitals: LCP (≤2.5s), INP (≤200ms), CLS (≤0.1) — all currently stable.
- Success threshold: 75th percentile of page loads across mobile and desktop must meet "good".
- Metrics progress through experimental → pending (≥6 months) → stable phases; changes are documented in a public changelog with predictable annual updates.
- Supporting metrics (not Core): TTFB, FCP, TBT.
- Lighthouse uses TBT as a lab proxy for INP since real interactions cannot be replicated in lab.
- The `web-vitals` JavaScript library provides a unified API for all three Core metrics with analytics integration.

## Connections
[[Core Web Vitals]], [[Web Performance]]

## Quotes
