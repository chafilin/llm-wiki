# Optimize Largest Contentful Paint

Source: https://web.dev/articles/optimize-lcp

## Overview

LCP measures how quickly the main content of a web page is loaded. **Target:** 2.5 seconds or less for at least 75% of page visits.

## LCP Breakdown: Four Subparts

LCP consists of these sequential, non-overlapping components:

| LCP Subpart | % of LCP | Description |
|---|---|---|
| Time to First Byte | ~40% | Initial HTML response time |
| Resource load delay | <10% | Time between TTFB and LCP resource loading starts |
| Resource load duration | ~40% | Time to transfer the LCP resource |
| Element render delay | <10% | Time from resource completion to element rendering |

**Key principle:** "The vast majority of the LCP time should be spent loading the HTML document and LCP source. Any time before LCP where one of these two resources is not loading is an opportunity to improve."

## Optimization Strategy: Four Steps

### 1. Eliminate Resource Load Delay

**Goal:** Start loading the LCP resource as early as possible.

**Discovery optimization:**
- Ensure the LCP resource is discoverable in initial HTML markup by the browser's preload scanner
- Make LCP images use `src` or `srcset` attributes in HTML
- Preload CSS background images with `<link rel="preload">`
- Preload web fonts with `<link rel="preload">`

**Priority optimization:**
- Use `fetchpriority="high"` on likely LCP elements
- Never use `loading="lazy"` on LCP images
- Use `fetchpriority="low"` on non-visible images (carousels)

```html
<!-- Preload with high priority -->
<link rel="preload" fetchpriority="high" as="image" 
      href="/path/to/hero-image.webp" type="image/webp">

<!-- Set high priority on img elements -->
<img fetchpriority="high" src="/path/to/hero-image.webp">
```

### 2. Eliminate Element Render Delay

**Goal:** Enable LCP element rendering immediately after resource completion.

**Common blocking causes:**
- Render-blocking stylesheets still loading
- Synchronous scripts in `<head>`
- JavaScript code hasn't added element to DOM
- A/B testing libraries hiding content
- Long tasks blocking the main thread

**Solutions:**

```html
<!-- Avoid this -->
<head>
  <script src="/path/to/main.js"></script>
</head>
```

- Inline small stylesheets to avoid network requests
- Defer or inline render-blocking JavaScript
- Use server-side rendering (SSR) to make image resources discoverable from HTML source
- Break up long tasks

### 3. Reduce Resource Load Duration

**Goal:** Minimize network transfer time for the LCP resource.

- Reduce resource size: serve optimal image sizes, use modern formats (WebP, AVIF), compress aggressively
- Use Content Delivery Networks (CDNs) to reduce distance traveled
- Assign `fetchpriority="high"` to LCP resources to reduce network contention
- Use `font-display` values other than `auto`/`block` for web fonts

### 4. Reduce Time to First Byte (TTFB)

**Goal:** Deliver initial HTML as quickly as possible.

**Common TTFB issues:**
- Multiple redirects
- Cached content unavailable at CDN edge
- Unique URL parameters preventing caching

"Nothing can happen on the frontend until the backend delivers that first byte of content, so anything you can do to speed up your TTFB will improve every other load metric as well."

## Summary

Optimizing LCP requires addressing all four subparts in order of impact:

1. Ensure LCP resource loads as early as possible
2. Enable rendering immediately after resource completion
3. Reduce LCP resource load time without sacrificing quality
4. Deliver initial HTML document fastest possible
