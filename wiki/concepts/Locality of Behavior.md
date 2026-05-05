---
title: Locality of Behavior
type: concept
updated: 2026-05-04
---

## Definition
Put the code that does a thing on the thing itself. When you look at a component/element/function, you should be able to understand its behavior without chasing across files.

## Why it matters
The opposite — Separation of Concerns (SoC) — splits behavior across css/html/js files (or components/stores/actions/selectors). You end up reading five files to understand one button click. Cognitive overhead scales with the number of files you need to hold in your head simultaneously.

## Examples
- Inline event handlers vs. separate event listener files
- htmx attributes directly on HTML elements vs. SPA component trees with separate state management
- CSS-in-JS / Tailwind on the element vs. external stylesheets by class name
- Business logic in the route handler vs. spread across middleware layers

## The tension with SoC
SoC feels clean in theory and diagrams. LoB feels messy but works better in practice for most systems. SoC is a better fit when the "concern" is genuinely reused across many places and the coupling is real, not theoretical.

## Open questions
- At what scale does LoB break down? Large design systems probably benefit from SoC. Small product features probably don't.

## Connections
[[The Grug Brained Developer]] [[Complexity]] [[Software Development]]
