---
title: Web Performance
type: entity
updated: 2026-05-07
sources: 17
---

## Overview

Web performance is measured through user-centric metrics that answer four questions: Is it happening? Is it useful? Is it usable? Is it delightful? Google's Web Vitals initiative distills this to three Core Web Vitals (LCP, CLS, INP) evaluated at the 75th percentile — the threshold that 75% of real page loads must meet. Lab tools (Lighthouse, DevTools) and field tools (CrUX, PageSpeed Insights) serve different purposes and must be used together. No single metric is sufficient.

## Key claims

- **Core Web Vitals** are LCP (loading), CLS (visual stability), and INP (responsiveness). All three are stable metrics evaluated at the 75th percentile. [[web.dev — Performance — Web Vitals]]
- **LCP target is 2.5s**: measures when the largest visible image/text block renders. Four subparts: TTFB (~40%), resource load delay (<10%), resource load duration (~40%), element render delay (<10%). Optimize TTFB and resource load duration first. [[web.dev — Performance — LCP]] [[web.dev — Performance — Optimize LCP]]
- **CLS target is 0.1**: score = impact fraction × distance fraction. Session window model (max 5s, gaps <1s). Most fixes: set explicit `width`/`height` on images, reserve space for ads/embeds, use `transform` for animations not `top`/`left`. [[web.dev — Performance — CLS]] [[web.dev — Performance — Optimize CLS]]
- **INP target is 200ms**: replaces FID; measures ALL interactions (click, tap, keypress) not just the first. Three components: input delay + processing duration + presentation delay. Yield to main thread with `setTimeout`/`requestAnimationFrame` for non-critical work. [[web.dev — Performance — INP]] [[web.dev — Performance — Optimize INP]]
- **TBT is the lab proxy for INP**: sum of blocking time beyond 50ms for all Long Tasks after FCP. Target <200ms on average mobile hardware. Not a field metric. [[web.dev — Performance — TBT]]
- **TTFB target is 0.8s**: not a Core Web Vital, but high TTFB makes 2.5s LCP near-impossible. Includes redirect + DNS + TLS + connection + first byte time. [[web.dev — Performance — TTFB]]
- **`fetchpriority="high"`** on LCP images is one of the highest-ROI single-line optimizations — prevents the browser from treating the hero image as low priority. Never use `loading="lazy"` on LCP elements. [[web.dev — Performance — Optimize LCP]]
- **Compositor-only animations**: only `transform` and `opacity` avoid layout and paint. `will-change: transform` promotes elements to their own GPU layer. Do not over-promote — each layer costs GPU memory. [[web.dev — Performance — Stick to Compositor-Only Properties]]
- **Lab vs field gap**: CLS is particularly underreported in lab — Lighthouse only measures load-time shifts. CrUX captures the full page lifecycle. Always cross-check. [[web.dev — Performance — Getting Started Measuring Web Vitals]]
- **Threshold methodology**: "good" thresholds require ≥10% of origins to pass (achievability). "Poor" thresholds typically affect 10-30% of origins. 75th percentile chosen to ensure majority of visits are captured without being distorted by extreme outliers. [[web.dev — Performance — Defining Core Web Vitals Thresholds]]
- **Custom metrics** via Performance Observer API: User Timing for arbitrary intervals, Long Animation Frames API (Chrome 123+) supersedes Long Tasks API, Element Timing for specific elements, Event Timing for interaction latency. [[web.dev — Performance — Custom Metrics]]
- **Back/forward cache** (bfcache) dramatically improves CLS for navigation-heavy sites. Ensure bfcache eligibility by removing incompatible patterns. [[web.dev — Performance — Optimize CLS]]
- **Debug layout shifts**: Layout Instability API with `PerformanceObserver`, DevTools Performance panel purple bars, `Layout Shift Regions` rendering flag for visual overlay. Sources array identifies shifted elements but may not be the root cause. [[web.dev — Performance — Debug Layout Shifts]]

## Media optimization

- **Replace GIFs with `<video>`**: AV1 is 20–40× smaller than GIF; `<video autoplay loop muted playsinline>` replicates GIF behavior with no JS. [[Evil Martians — Better Web Video with AV1 Codec]]
- **Two-source strategy**: AV1 + Opus (modern browsers) as first `<source>`, H.264 + AAC as fallback. Browsers pick the first supported format. [[Evil Martians — Better Web Video with AV1 Codec]]
- **AV1 vs H.264**: 30–50% smaller at equivalent quality. Hardware decode requires iPhone 15+, M3 Mac; older devices fall back gracefully.
- **ffmpeg encoder**: use `libsvtav1` (SVT-AV1) — faster than `libaom-av1`. Key flags: `-qp 30`, `-movflags +faststart`, `-pix_fmt yuv420p`.
- Media is often the LCP element — AV1 video replacing a large hero image or GIF directly improves LCP load duration.

## Open questions

- What's the practical impact of INP on Manychat's chat widget (it runs in an iframe with its own main thread)?
- How do you measure CWV for SPAs where navigation doesn't reload the page?
- What's the web-vitals library overhead at scale (millions of page loads)?

## Connections

[[Core Web Vitals]] [[JavaScript Memory Management]] [[Software Development]]
