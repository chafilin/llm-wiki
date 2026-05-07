---
title: Core Web Vitals
type: concept
updated: 2026-05-07
---

## Definition

Core Web Vitals are Google's three stable, field-measurable metrics that represent the most important aspects of user experience: loading (LCP), visual stability (CLS), and responsiveness (INP). A site "passes" when 75% of real page loads meet the "good" threshold for all three. They affect Google Search ranking.

## Why it matters

These are the metrics Google uses to rank pages and the ones PageSpeed Insights surfaces first. As a frontend dev, these are the KPIs I'm accountable for on any production site. They're also the only performance metrics with a standardized, research-backed methodology for threshold selection.

## The three metrics

| Metric | Measures | Good | Poor | Type |
|--------|---------|------|------|------|
| **LCP** (Largest Contentful Paint) | Loading | ≤2.5s | >4.0s | Field + Lab |
| **CLS** (Cumulative Layout Shift) | Visual stability | ≤0.1 | >0.25 | Field + Lab |
| **INP** (Interaction to Next Paint) | Responsiveness | ≤200ms | >500ms | Field only* |

*INP requires real interactions — use TBT (<200ms) as the lab proxy.

All thresholds measured at the **75th percentile** across mobile and desktop.

## Metric lifecycle

Metrics go through three phases: Experimental → Pending (min 6 months) → Stable. INP replaced FID in March 2024. LCP, CLS, INP are all currently stable.

## Measurement tools

**Field (real users):**
- Chrome User Experience Report (CrUX) — 28-day aggregate
- PageSpeed Insights — CrUX data + Lighthouse lab
- Search Console Core Web Vitals report — per-page, historical
- `web-vitals` npm library — DIY RUM (~2KB)

**Lab (synthetic):**
- Lighthouse — LCP, CLS, TBT (not INP)
- Chrome DevTools Performance panel — all three in live metrics view
- WebPageTest — field conditions simulation

## Key implementation patterns

```javascript
import {onCLS, onINP, onLCP} from 'web-vitals';

function sendToAnalytics(metric) {
  const body = JSON.stringify(metric);
  (navigator.sendBeacon && navigator.sendBeacon('/analytics', body)) ||
    fetch('/analytics', {body, method: 'POST', keepalive: true});
}

onCLS(sendToAnalytics);
onINP(sendToAnalytics);
onLCP(sendToAnalytics);
```

## LCP optimization quick wins

1. `fetchpriority="high"` on hero image — single highest-ROI change
2. Remove `loading="lazy"` from above-fold images
3. Preload: `<link rel="preload" fetchpriority="high" as="image" href="...">`
4. Use WebP/AVIF format
5. Reduce TTFB (CDN, caching)

## CLS optimization quick wins

1. Set explicit `width` + `height` on all `<img>` elements
2. Reserve space for ads/embeds with `min-height` or `aspect-ratio`
3. Replace `top`/`left` animations with `transform: translateY()`
4. Use `font-display: optional` or override fallback font metrics

## INP optimization quick wins

1. Break up long event callbacks with `setTimeout` after visual update
2. Use `requestAnimationFrame` to defer non-visual work
3. Avoid layout thrashing (read layout → write styles → read layout)
4. Reduce DOM size; consider `content-visibility: auto` for off-screen content

## Examples

- A page where the hero image has no `fetchpriority` — browser treats it same as any image, LCP suffers
- An ad unit without `min-height: 250px` — shifts content down when it loads, tanks CLS
- A search box that runs a synchronous filter on every keypress — blocks main thread, INP suffers

## Connections

[[Web Performance]] [[Software Development]]
