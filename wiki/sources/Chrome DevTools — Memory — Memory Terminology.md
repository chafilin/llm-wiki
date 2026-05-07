---
title: "Chrome DevTools — Memory — Memory Terminology"
type: source
raw: raw/articles/Chrome DevTools — Memory — Memory Terminology.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The Chrome DevTools conceptual reference for memory analysis terminology, covering how JavaScript objects hold memory (shallow vs. retained size), how the garbage collector determines reachability via GC roots, the dominator tree structure, and V8-specific memory internals. Essential vocabulary for interpreting heap snapshots and allocation profiles.

## Key takeaways
- Shallow size: memory held by the object itself. Retained size: memory freed when the object and all objects it exclusively keeps alive are deleted.
- GC roots are the starting points for reachability: window globals, DOM trees with native nodes, debugger contexts.
- "Distance" in heap snapshots = shortest path from an object to the GC root.
- Dominator tree: each object has exactly one immediate dominator; deleting the dominator allows the entire dominated subtree to be collected.
- V8 stores numbers as 31-bit SMIs or heap numbers; strings live in VM heap or renderer memory with wrapper objects.
- Native objects (DOM nodes, CSS rules) live outside the JS heap; each has a JS wrapper object. Retaining one wrapper in an object group keeps the entire group alive.

## Connections
[[JavaScript Memory Management]]

## Quotes
> "This is the size of memory that is freed once the object itself is deleted along with its dependent objects that were made unreachable from GC roots."
