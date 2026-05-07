# Interaction to Next Paint (INP)

Source: https://web.dev/articles/inp

## Overview

Interaction to Next Paint (INP) is a stable Core Web Vital metric that measures how quickly a page responds to user interactions. "90% of a user's time on a page is spent _after_ it loads," making responsiveness throughout the entire page lifecycle crucial.

## What is INP?

INP assesses overall page responsiveness by observing the latency of all click, tap, and keyboard interactions throughout a user's visit. The metric reports the longest interaction observed, while ignoring statistical outliers (one highest interaction per 50 interactions).

**Key Definition:** An interaction's latency consists of the time "from when user interaction occurs...to the next time the rendering...is updated."

## Good INP Thresholds

Measured at the 75th percentile:

- **≤ 200 milliseconds**: Good responsiveness
- **200–500 milliseconds**: Needs improvement
- **> 500 milliseconds**: Poor responsiveness

## Interaction Components

An interaction includes three phases:

1. **Input Delay**: Time before event handlers begin executing (often caused by long tasks)
2. **Processing Duration**: Time for all event handler callbacks to execute
3. **Presentation Delay**: Time until the next frame is painted

## Observed Interaction Types

INP measures only:
- Mouse clicks
- Touchscreen taps
- Keyboard key presses

**Excluded interactions** include scrolling, hovering, and zooming.

## INP vs. First Input Delay (FID)

INP improves on its predecessor by measuring responsiveness for "all interactions on a page," rather than just the first one. FID only assessed initial responsiveness, while INP captures the complete user experience.

## Measurement Approaches

### Field Data
Real User Monitoring (RUM) provides contextual data about actual interactions, including whether they occurred during or after page load.

### Lab Testing
Lab environments can reproduce slow interactions by:
- Interacting with pages during load when the main thread is busiest
- Following common user flows
- Testing on lower-end devices

## JavaScript Measurement

```javascript
import {onINP} from 'web-vitals';

onINP(console.log);
```

## API Differences

- Event entries below 104ms don't report by default
- Interactions within iframes aren't reported by the API but count for the metric
- Pages restored from the back/forward cache reset their INP value to zero

## When INP May Not Be Reported

- No user interactions (clicks, taps, or key presses) occurred
- User only scrolled or hovered
- Page accessed by non-interactive bots
