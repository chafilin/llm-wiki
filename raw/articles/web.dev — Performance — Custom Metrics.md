# Custom Metrics

Source: https://web.dev/articles/custom-metrics

## Overview

Universal metrics provide valuable baseline performance data, but many sites require measuring additional metrics specific to their unique functionality — such as single-page app transitions, database query times, server-side rendering hydration, cache hit rates, or event latency in interactive applications.

## Why Custom Metrics Matter

Custom metrics capture site-specific experiences that universal metrics cannot address:

- Time for single-page app transitions between "pages"
- Data fetch and display duration for logged-in users
- Server-side-rendered app hydration completion
- Resource cache hit rates for returning visitors
- Event latency for interactive applications like games

## Key APIs for Measuring Custom Metrics

### Performance Observer API
**Browser Support:** Chrome 52+, Edge 79+, Firefox 57+, Safari 11+

The foundational API for passive performance monitoring. Rather than polling, developers register callbacks that fire during idle periods, minimizing performance impact.

```javascript
const po = new PerformanceObserver((list) => {
  for (const entry of list.getEntries()) {
    console.log(entry.toJSON());
  }
});

po.observe({type: 'some-entry-type'});
```

**Historical data:** Set `buffered: true` to retrieve entries that already occurred before observer initialization:

```javascript
po.observe({
  type: 'some-entry-type',
  buffered: true,
});
```

**Legacy alternatives to avoid:** `getEntries()`, `getEntriesByName()`, and `getEntriesByType()` lack event-driven capabilities. Use PerformanceObserver instead.

### User Timing API
**Browser Support:** Chrome 28+, Edge 12+, Firefox 38+, Safari 11+

General-purpose measurement for arbitrary time intervals:

```javascript
performance.mark('myTask:start');
await doMyTask();
performance.mark('myTask:end');
performance.measure('myTask', 'myTask:start', 'myTask:end');
```

Observe measurements via PerformanceObserver:

```javascript
const po = new PerformanceObserver((list) => {
  for (const entry of list.getEntries()) {
    console.log(entry.toJSON());
  }
});

po.observe({type: 'measure', buffered: true});
```

### Long Tasks API
**Browser Support:** Chrome 58+, Edge 79+

Identifies main thread blocking by reporting tasks exceeding 50 milliseconds:

```javascript
const po = new PerformanceObserver((list) => {
  for (const entry of list.getEntries()) {
    console.log(entry.toJSON());
  }
});

po.observe({type: 'longtask', buffered: true});
```

**Note:** Superseded by Long Animation Frames API but still useful for legacy contexts.

### Long Animation Frames API
**Browser Support:** Chrome 123+, Edge 123+

Newer iteration measuring long frames (over 50ms) rather than tasks, providing superior attribution:

```javascript
const po = new PerformanceObserver((list) => {
  for (const entry of list.getEntries()) {
    console.log(entry.toJSON());
  }
});

po.observe({type: 'long-animation-frame', buffered: true});
```

### Element Timing API
**Browser Support:** Chrome 77+, Edge 79+

Measures render timing for specific elements. Mark elements with the `elementtiming` attribute:

```html
<img elementtiming="hero-image" />
<p elementtiming="important-paragraph">This is text I care about.</p>
```

```javascript
const po = new PerformanceObserver((entryList) => {
  for (const entry of entryList.getEntries()) {
    console.log(entry.toJSON());
  }
});

po.observe({type: 'element', buffered: true});
```

Only elements eligible for Largest Contentful Paint measurement support this attribute.

### Event Timing API
**Browser Support:** Chrome 76+, Edge 79+, Firefox 89+

Tracks event responsiveness by measuring interaction latency for click and keyboard events.

## Best Practice: Non-Invasive Measurement

"The first rule of effective performance measurement is to make sure your performance measurement techniques aren't causing performance issues themselves." Use APIs that operate during idle periods rather than techniques that actively block execution.
