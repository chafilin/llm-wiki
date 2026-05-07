# Cumulative Layout Shift (CLS)

Source: https://web.dev/articles/cls

## Overview

CLS is a Core Web Vital metric measuring visual stability by quantifying unexpected layout shifts on web pages. CLS measures "the largest burst of layout shift scores for every unexpected layout shift that occurs during the entire lifecycle of a page."

A **session window** contains one or more rapid layout shifts occurring within less than 1 second of each other, with a maximum 5-second window duration. CLS identifies the session with the highest cumulative score.

## Good CLS Score Targets

Sites should aim for CLS of **0.1 or less** at the **75th percentile** of page loads, segmented by device type:

- **Good:** 0.1 or less
- **Needs improvement:** 0.1–0.25
- **Poor:** Greater than 0.25

## Layout Shifts Explained

Layout shifts occur when visible elements change their start position between frames. New DOM elements or size changes don't count unless they cause existing elements to move.

### Layout Shift Score Formula

```
layout shift score = impact fraction × distance fraction
```

**Impact fraction** measures how much viewport area unstable elements affect across two frames (as a proportion of total viewport).

**Distance fraction** represents the greatest horizontal or vertical distance any unstable element moved, divided by the viewport's largest dimension.

### Example Calculation

An element occupying half the viewport that shifts down by 25% of viewport height yields:
- Impact fraction: 0.75
- Distance fraction: 0.25
- Layout shift score: 0.1875

## Expected vs. Unexpected Shifts

### User-Initiated Shifts

Layout shifts occurring within 500 milliseconds of user interaction (clicks, taps, keypresses) receive the `hadRecentInput` flag for exclusion from CLS.

### Animations & Transitions

Use CSS `transform` properties instead of modifying positional values:
- Use `transform: scale()` instead of changing `height`/`width`
- Use `transform: translate()` instead of modifying `top`, `right`, `bottom`, or `left`

Respect browser `prefers-reduced-motion` settings.

## Measuring CLS

### Field Tools

- Chrome User Experience Report
- PageSpeed Insights
- Search Console (Core Web Vitals report)
- `web-vitals` JavaScript library

### Lab Tools

- Chrome DevTools
- Lighthouse
- PageSpeed Insights
- WebPageTest

**Note:** Lab environments may underreport CLS since they measure only page-load shifts.

### JavaScript Measurement

```javascript
new PerformanceObserver((entryList) => {
  for (const entry of entryList.getEntries()) {
    console.log('Layout shift:', entry);
  }
}).observe({type: 'layout-shift', buffered: true});
```

### web-vitals Library

```javascript
import {onCLS} from 'web-vitals';

onCLS(console.log);
```

## Key Differences: Metric vs. API

- Background pages shouldn't report CLS values
- Back/forward cache restoration should reset CLS to zero
- The API doesn't report iframe layout shifts, though the metric includes them
- Long-lived tabs require reporting CLS when pages are backgrounded
