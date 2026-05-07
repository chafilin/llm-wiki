# Web Vitals

Source: https://web.dev/articles/vitals

## Overview

Google's Web Vitals initiative provides unified guidance on essential quality signals for delivering excellent user experiences online. Web Vitals simplifies the landscape by focusing on what matters most: the Core Web Vitals.

## Core Web Vitals

Core Web Vitals apply universally to all web pages and represent distinct facets of user experience. They're measurable in real-world conditions and reflect critical user-centric outcomes.

### The Three Metrics

**Largest Contentful Paint (LCP)** — Measures loading performance. Target: within 2.5 seconds of page load initiation.

**Interaction to Next Paint (INP)** — Measures responsiveness. Target: 200 milliseconds or less.

**Cumulative Layout Shift (CLS)** — Measures visual stability. Target: 0.1 or less.

Success is measured at the **75th percentile** across mobile and desktop devices.

## Metric Lifecycle

Core Web Vitals metrics progress through three phases:

- **Experimental**: Prospective metrics undergoing testing and refinement
- **Pending**: Metrics that have passed validation with defined timelines (minimum six-month phase)
- **Stable**: Current essential metrics actively supported by Chrome

Current status: LCP, CLS, and INP are all stable.

## Measurement Tools

### Field Measurement
- Chrome User Experience Report
- Chrome DevTools
- PageSpeed Insights
- Search Console Core Web Vitals report

### JavaScript Implementation

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

### Lab Measurement
- Chrome DevTools (LCP, INP, CLS)
- Lighthouse (LCP, CLS; uses Total Blocking Time as INP proxy)

## Supporting Metrics

Other Web Vitals supplement Core metrics:
- Time to First Byte (TTFB)
- First Contentful Paint (FCP)
- Total Blocking Time (TBT)

All changes to Web Vitals are documented in a public changelog with predictable annual updates for Core Web Vitals.
