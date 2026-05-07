# Time to First Byte (TTFB)

Source: https://web.dev/articles/ttfb

## Overview

"TTFB is a metric that measures the time between starting navigating to a page and when the first byte of a response begins to arrive." It serves as a foundational measure for connection setup and server responsiveness in both lab and field environments.

## What TTFB Measures

TTFB encompasses these request phases:

- Redirect time
- Service worker startup time (if applicable)
- DNS lookup
- Connection and TLS negotiation
- Request duration until the first response byte arrives

The metric is calculated as the elapsed time between `startTime` and `responseStart`.

## TTFB and Early Hints

The introduction of 103 Early Hints creates measurement nuance. "The 103 Early Hints counts as the 'first bytes'." Chrome 115 initially updated `responseStart` to measure the final document response, but this was reverted in Chrome 133.

## Good TTFB Scores

"Most sites should strive to have a TTFB of **0.8 seconds or less**" to support user-centric metrics like First Contentful Paint (FCP) at the 75th percentile. Scores greater than 1.8 seconds are considered poor.

**Important caveat:** TTFB is not a Core Web Vitals metric, so meeting this threshold isn't mandatory if it doesn't impair performance on metrics that matter.

### Context Matters

- **Single Page Applications (SPAs)**: Require minimal TTFB for client-side rendering
- **Server-rendered sites**: May have higher TTFB but better FCP/LCP values

## Measuring TTFB

### Field Tools
- Chrome User Experience Report
- `web-vitals` JavaScript library

### Lab Tools
- Chrome DevTools network panel
- WebPageTest

### JavaScript Measurement (Navigation Requests)

```javascript
new PerformanceObserver((entryList) => {
  const [pageNav] = entryList.getEntriesByType('navigation');
  console.log(`TTFB: ${pageNav.responseStart}`);
}).observe({
  type: 'navigation',
  buffered: true
});
```

### web-vitals Library

```javascript
import {onTTFB} from 'web-vitals';
onTTFB(console.log);
```

### Measuring Resource Requests

```javascript
new PerformanceObserver((entryList) => {
  const entries = entryList.getEntries();
  for (const entry of entries) {
    if (entry.responseStart > 0) {
      console.log(`TTFB: ${entry.responseStart}`, entry.name);
    }
  }
}).observe({
  type: 'resource',
  buffered: true
});
```

**Note:** Resources from the primary origin may return `responseStart` of 0 if already cached. Cross-origin TTFB measurement requires `Timing-Allow-Origin` headers.
