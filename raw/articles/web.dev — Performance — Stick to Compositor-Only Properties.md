# Stick to Compositor-Only Properties and Manage Layer Count

Source: https://web.dev/articles/stick-to-compositor-only-properties-and-manage-layer-count

Author: Paul Lewis

## Overview

Compositing combines painted page elements for screen display. Non-composited animations perform poorly and appear janky, especially on low-end devices or when the main thread is busy.

## Summary

- Use `transform` and `opacity` changes exclusively for animations
- Promote moving elements via `will-change` or `translateZ`
- Avoid excessive layer promotion; layers consume memory and require management

## Use Transform and Opacity for Animations

The optimal pixel pipeline avoids layout and paint operations, requiring only compositing changes. Currently, only two properties trigger compositing alone: `transform`s and `opacity`.

**Important caveat:** Elements with these property changes must reside on their own compositor layer, requiring element promotion.

**Tip:** The FLIP principle can help remap complex animations to `transform` and `opacity` changes.

## Promoting Elements for Animation

Promote elements you plan to animate to separate layers:

```css
.moving-element {
  will-change: transform;
}
```

For older browser support:

```css
.moving-element {
  transform: translateZ(0);
}
```

## Managing Layers and Preventing Layer Explosions

Each layer requires:
- Memory allocation and management overhead
- GPU texture uploads
- CPU-GPU bandwidth
- GPU memory allocation

**Warning:** "Do not promote elements unnecessarily."

### Using Chrome DevTools to Analyze Layers

Enable the Paint profiler in Chrome DevTools Timeline to examine layers. Record performance activity, then click individual frames to access layer analysis. The layer tab reveals:
- All layers during that frame
- Reasons for layer creation
- Layer pan/scan/zoom capabilities

Target approximately **4-5ms** for compositing during performance-critical actions like scrolling or transitions.
