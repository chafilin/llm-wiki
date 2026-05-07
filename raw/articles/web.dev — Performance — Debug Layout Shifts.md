# Debug Layout Shifts

Source: https://web.dev/articles/debug-layout-shifts

Authors: Katie Hempenius, Barry Pollard

## Overview

This guide covers tools and techniques for identifying and fixing layout shifts.

## Tooling

### Layout Instability API

The Layout Instability API is the browser mechanism underlying all layout shift debugging tools. Currently supported only by Chromium browsers.

#### Basic Usage

```javascript
let cls = 0;
new PerformanceObserver((entryList) => {
  for (const entry of entryList.getEntries()) {
    if (!entry.hadRecentInput) {
      cls += entry.value;
      console.log('Current CLS value:', cls, entry);
    }
  }
}).observe({type: 'layout-shift', buffered: true});
```

**Key behaviors:**
- `buffered: true` reports shifts both before and after observer initialization
- Reports are delayed until the main thread is idle
- Shifts within 500ms of user input are excluded from CLS calculations

#### LayoutShift Interface

| Property | Description |
|----------|-------------|
| `sources` | Array of DOM elements that moved (up to five largest impacts reported) |
| `value` | The layout shift score for this event |
| `hadRecentInput` | Whether shift occurred within 500ms of user interaction |
| `startTime` | When the shift occurred (milliseconds from page load start) |
| `duration` | Always 0 |

#### LayoutShiftAttribution Interface

Describes individual element shifts:

```javascript
{
  "node": "div#banner",
  "previousRect": { "x": 311, "y": 76, "width": 4, "height": 18 },
  "currentRect": { "x": 311, "y": 246, "width": 4, "height": 18 }
}
```

**Important caveat:** Elements listed as sources may not be the root cause — they might be indirectly affected by changes elsewhere.

### DevTools

#### Performance Panel

1. Open the Performance panel
2. Interact with the page to trigger layout shifts
3. View CLS score updates in the live metrics display

For detailed analysis, create a performance trace:
- The "Layout Shifts" track shows purple bars representing shift clusters
- Diamond markers indicate individual shifts; size correlates with impact
- Click diamonds to see shift animations and element highlighting

#### Highlight Layout Shift Regions

1. Go to **Settings > More Tools > Rendering > Layout Shift Regions**
2. Refresh the page
3. Layout shift areas briefly highlight in purple

## Identifying Layout Shift Causes

### Common Triggers

- **Position changes** of DOM elements
- **Dimension changes** of DOM elements
- **Insertion/removal** of DOM elements
- **Animations** that trigger layout

**Investigation strategy:** The DOM element immediately preceding the shifted element is most likely involved.

### Direction and Distance Clues

- **Large downward shifts** often indicate DOM element insertion
- **1-2 pixel shifts** suggest conflicting CSS styles or font-swapping effects

### Specific Causes and Solutions

#### Position Changes
Often caused by late-loading or overriding stylesheets, animation and transition effects.

#### Dimension Changes
Often caused by images/iframes without explicit `width` and `height` attributes, text blocks that swap fonts after rendering.

#### DOM Insertion/Removal
Often caused by ad and third-party embed insertion, banners, alerts, and modal insertion, infinite scroll loading content above existing content.

#### Layout-Triggering Animations
Avoid incrementing position properties (`top`, `left`); use CSS `transform` instead.

### Reproducing Layout Shifts

1. Interact with your site for 5-10 minutes deliberately triggering shifts
2. Keep the console open using the Layout Instability API
3. Test with different devices and connection speeds
4. Slower connections often make shifts more visible

**Advanced debugging — add a `debugger` statement:**

```javascript
new PerformanceObserver((entryList) => {
  for (const entry of entryList.getEntries()) {
    if (!entry.hadRecentInput) {
      cls += entry.value;
      debugger;
      console.log('Current CLS value:', cls, entry);
    }
  }
}).observe({type: 'layout-shift', buffered: true});
```
