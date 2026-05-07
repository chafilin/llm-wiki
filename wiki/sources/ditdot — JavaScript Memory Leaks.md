---
title: "ditdot — JavaScript Memory Leaks"
type: source
raw: raw/articles/ditdot — JavaScript Memory Leaks.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A practical guide from ditdot.hr cataloguing the six most common sources of JavaScript memory leaks, explaining the mechanism behind each, and providing concrete prevention strategies. Written for developers who need to identify and eliminate memory leaks before they degrade production UX.

## Key takeaways
- A memory leak is an object that should be garbage collected but remains reachable via an unintentional reference chain.
- Six common sources: accidental global variables, closures retaining large outer-scope objects, uncleared timers (`setInterval`/`setTimeout`), persistent event listeners, unbounded caches, and detached DOM elements.
- Accidental globals: variables assigned without `var`/`let`/`const`, or `this` assignments in non-strict mode functions; fix with `'use strict'`.
- Timers: store IDs and call `clearInterval`/`clearTimeout` when done; orphaned intervals have no cleanup path.
- Event listeners: use named functions + `removeEventListener`, or the `{once: true}` option for single-execution listeners.
- Cache leaks: use `WeakMap` with object keys so entries are automatically removed when the key object is GC'd.
- Detached DOM: keep DOM references in local scope so they're released when the function returns.

## Connections
[[JavaScript Memory Management]]

## Quotes
> "A memory leak occurs when an object in memory that is supposed to be cleaned in a garbage collection cycle stays reachable from the root through an unintentional reference by another object."

> "When it comes to memory and performance, it is the user experience that is at stake."
