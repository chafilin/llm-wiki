---
title: "Chrome DevTools — Memory — Heap Snapshots"
type: source
raw: raw/articles/Chrome DevTools — Memory — Heap Snapshots.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The Chrome DevTools guide to the heap profiler's snapshot tool, covering how to take snapshots, the four views (Summary, Comparison, Containment, Statistics), special constructor entries, and how to track down DOM leaks. Includes the technique of naming functions inside closures to improve snapshot readability.

## Key takeaways
- Snapshots only show reachable objects; taking a snapshot always triggers garbage collection first.
- Four views: Summary (by constructor type), Comparison (diff between two snapshots to detect leaks), Containment (object graph bird's-eye view), Statistics (pie chart of allocation by category).
- Key columns: Distance (path length to GC root), Shallow size, Retained size.
- Comparison workflow: snapshot → do action → undo action → snapshot → compare; added/deleted object counts reveal leaks.
- Special entries to know: `system / Context` = closure local variables; `(object shape)` = V8 hidden classes; `(compiled code)` = V8 internal execution data.
- DOM leaks: child nodes retain parent references recursively — removing a tree node from the DOM and nulling the parent reference is insufficient if any child reference exists.
- Name closure functions for cleaner snapshot attribution.

## Connections
[[JavaScript Memory Management]]

## Quotes
> "Snapshots show only the objects from the memory graph that are reachable from the global object. Taking a snapshot always starts with garbage collection."
