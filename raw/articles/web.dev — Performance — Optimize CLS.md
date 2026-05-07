# Optimize Cumulative Layout Shift

Source: https://web.dev/articles/optimize-cls

## Overview

CLS is a Core Web Vitals metric measuring content instability. "Sites should strive to have a CLS of 0.1 or less for at least 75% of page visits."

## Common CLS Causes

- Images without dimensions
- Ads, embeds, and iframes lacking dimensions
- Dynamically injected content without reserved space
- Web fonts

## Understanding CLS Measurement

Lab environments (Chrome DevTools, Lighthouse) measure CLS during initial page load only. The Chrome UX Report (CrUX) captures full-page-lifecycle shifts. "CLS is measured throughout the full life of the page and not just during the initial page load."

## Optimization Solutions

### Images Without Dimensions

Include `width` and `height` attributes on `<img>` tags:

```html
<img src="puppy.jpg" width="640" height="360" alt="Puppy with balloons">
```

Modern browsers automatically calculate aspect ratio from these attributes. Combine with responsive CSS:

```css
img {
  height: auto;
  width: 100%;
}
```

For responsive images using `srcset`, maintain consistent aspect ratios across all variants:

```html
<img
  width="1000"
  height="1000"
  src="puppy-1000.jpg"
  srcset="puppy-1000.jpg 1000w, puppy-2000.jpg 2000w"
  alt="Puppy with balloons"
/>
```

### Ads, Embeds, and Dynamic Content

Reserve space using CSS properties:

```css
/* Fixed height */
.ad-container {
  min-height: 250px;
}

/* Responsive using aspect-ratio */
.ad-container {
  aspect-ratio: 16 / 9;
}
```

- Place late-loading content lower in viewport
- Avoid inserting content without user interaction
- Use placeholders or skeleton UI
- Implement "Load More" buttons so shifts occur within 500ms of interaction (excluded from CLS)

### Animation Properties

Avoid layout-shifting animations. "Changing the `top` and `left` properties cause layout shifts, even when the element is on its own layer."

Use `transform` instead:

```css
/* Avoid */
animation: moveDown 1s;
@keyframes moveDown { from { top: 0; } to { top: 100px; } }

/* Prefer */
animation: slideDown 1s;
@keyframes slideDown { from { transform: translateY(0); } to { transform: translateY(100px); } }
```

### Web Fonts

Font loading causes layout shifts when fallback fonts have different metrics.

Use `font-display: optional` to avoid re-layout:

```css
@font-face {
  font-family: "Google Sans";
  src: url("google-sans.woff2") format("woff2");
  font-display: optional;
}
```

Override fallback metrics using CSS properties:

```css
@font-face {
  font-family: "Google Sans";
  src: url("google-sans.woff2");
  ascent-override: 90%;
  descent-override: 22%;
  line-gap-override: 0%;
}
```

Preload critical fonts:

```html
<link rel="preload" 
      href="google-sans.woff2" 
      as="font" 
      type="font/woff2" 
      crossorigin>
```

## Back/Forward Cache Strategy

Pages eligible for the bfcache restore instantly without reload-induced layout shifts. "When this was rolled out to Chrome, noticeable improvements in CLS were observed."
