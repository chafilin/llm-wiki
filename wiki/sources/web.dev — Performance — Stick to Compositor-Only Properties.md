---
title: "web.dev — Performance — Stick to Compositor-Only Properties"
type: source
raw: raw/articles/web.dev — Performance — Stick to Compositor-Only Properties.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A web.dev article by Paul Lewis explaining how the browser's rendering pipeline works and why restricting animations to `transform` and `opacity` is critical for smooth performance. Covers compositor layer promotion with `will-change`, the cost of maintaining excess layers, and how to audit layers in Chrome DevTools.

## Key takeaways
- Only `transform` and `opacity` changes can be handled entirely by the compositor, bypassing layout and paint.
- Elements must be on their own compositor layer for these properties to be composited; promote with `will-change: transform` or `transform: translateZ(0)` as legacy fallback.
- Every promoted layer costs memory (CPU allocation, GPU texture uploads, bandwidth) — do not promote elements unnecessarily.
- Target ~4–5ms for compositing during scrolling or transitions.
- The FLIP technique remaps complex animations to `transform`/`opacity` changes.
- Chrome DevTools Timeline paint profiler shows all layers, reasons for creation, and compositing cost per frame.

## Connections
[[Web Performance]], [[Core Web Vitals]]

## Quotes
> "Do not promote elements unnecessarily."
