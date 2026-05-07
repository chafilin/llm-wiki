# Largest Contentful Paint (LCP)

Source: https://web.dev/articles/lcp

## Overview

Largest Contentful Paint measures perceived load speed by identifying when the page's main content becomes visible. "LCP reports the render time of the largest image, text block, or video visible in the viewport, relative to when the user first navigated to the page."

This metric addresses limitations of older approaches like `load` and `DOMContentLoaded` events, which don't necessarily correspond to what users actually see on screen.

## Performance Targets

**Good LCP Score:** 2.5 seconds or less

The benchmark measurement should use the 75th percentile of page loads, evaluated separately for mobile and desktop devices. Values exceeding 4.0 seconds are considered poor performance.

## Elements Considered for LCP

The following element types qualify as LCP candidates:

- `<img>` elements (using first frame presentation time for animated content)
- `<image>` elements within `<svg>` elements
- `<video>` elements (poster image or first frame, whichever is earlier)
- Elements with background images loaded via `url()` function
- Block-level elements containing text nodes or inline-level text children

**Important exclusions:** The metric applies heuristics to exclude certain elements users likely perceive as non-contentful:

- Elements with opacity of 0
- Elements covering the full viewport
- Placeholder images or low-entropy images

## Size Determination

For LCP calculations, only the visible portion within the viewport counts. "For image elements that have been resized from their intrinsic size, the size that gets reported is either the visible size or the intrinsic size, whichever is smaller."

CSS margins, padding, and borders don't factor into size calculations.

## Timing and Reporting

The browser dispatches a `PerformanceEntry` of type `largest-contentful-paint` after rendering the first frame, then updates it whenever a larger element renders.

**Key timing considerations:**

- Elements must be rendered and visible to qualify
- Images that haven't loaded don't count yet
- Text nodes using web fonts during the font block period don't count until fully loaded
- New DOM elements larger than previous candidates trigger updates
- User interaction (tap, scroll, keypress) stops new entries from being reported

"The browser will stop reporting new entries as soon as the user interacts with the page (via a tap, scroll, or keypress), as user interaction often changes what's visible to the user."

## Load Time vs. Render Time

For security reasons, cross-origin images without the `Timing-Allow-Origin` header historically only exposed load time rather than render time. As of Chrome 133+, coarsened render time is provided even without this header, though setting the header remains recommended for accuracy.

## Layout and Size Changes

Changes to an element's position or size don't generate new LCP candidates — "only the element's initial size and position in the viewport is considered."

## Measuring LCP

### Available Tools

**Field measurement:**
- Chrome User Experience Report
- PageSpeed Insights
- Search Console (Core Web Vitals report)
- web-vitals JavaScript library

**Lab measurement:**
- Chrome DevTools
- Lighthouse
- PageSpeed Insights
- WebPageTest

### JavaScript Implementation

```javascript
new PerformanceObserver((entryList) => {
  for (const entry of entryList.getEntries()) {
    console.log('LCP candidate:', entry.startTime, entry);
  }
}).observe({type: 'largest-contentful-paint', buffered: true});
```

### Metric vs. API Differences

- Background tab entries should be ignored
- Entries after backgrounding should be excluded
- Back/forward cache restoration requires measurement
- Iframes are counted in the metric but not the API
- Prerendered pages measure from `activationStart` rather than navigation start

The `web-vitals` JavaScript library handles many of these differences automatically.
