# First Contentful Paint (FCP)

Source: https://web.dev/articles/fcp

## Overview

First Contentful Paint measures the time elapsed from when a user initially navigates to a page until any content becomes visible on screen. "FCP marks the first point in the page load timeline where the user can see anything on the screen."

## What Counts as Content

The metric applies to:
- Text elements
- Images (including background images)
- SVG elements
- Non-white canvas elements

## Key Measurement Considerations

FCP includes unload time from previous pages, connection setup time, redirect duration, and Time To First Byte (TTFB). These components can significantly affect field measurements compared to laboratory testing.

## Performance Targets

Sites should target **1.8 seconds or less** at the 75th percentile across mobile and desktop devices. Scores exceeding 3.0 seconds are considered poor performance.

## Measuring FCP

### Available Tools

**Field measurement:** PageSpeed Insights, Chrome User Experience Report, Search Console, web-vitals JavaScript library

**Lab measurement:** Lighthouse, Chrome DevTools, PageSpeed Insights

### JavaScript Implementation

Use the Paint Timing API with PerformanceObserver, or the `web-vitals` library which handles edge cases including background tabs, back/forward cache restoration, and prerendered pages.

## Optimization Strategies

- Eliminate render-blocking resources
- Minify and remove unused CSS
- Remove unused JavaScript
- Preconnect to required origins
- Reduce Time To First Byte
- Avoid redirects and excessive payloads
- Efficient cache policies and minimized DOM sizes
