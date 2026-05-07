---
title: "Chrome DevTools — Memory — Fix Memory Problems"
type: source
raw: raw/articles/Chrome DevTools — Memory — Fix Memory Problems.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The Chrome DevTools guide to diagnosing the three user-visible memory problems: progressive performance degradation (memory leaks), consistently poor performance (memory bloat), and frequent pauses (garbage collection pressure). Covers the full set of DevTools memory tooling and when to use each.

## Key takeaways
- Three memory problem archetypes: leaks (progressive degradation), bloat (persistent excess memory), GC pressure (frequent pauses).
- Chrome Task Manager (Shift+Esc) shows JavaScript memory footprint per tab; the parenthesized "live" number reveals reachable object memory.
- Performance panel with Memory checkbox enabled shows heap graph and a counter pane breaking down JS heap, DOM nodes, listeners, and GPU memory over time.
- Heap Snapshots: take a snapshot, filter the Class filter for "Detached" to find detached DOM trees held alive by JavaScript references.
- Allocation Timeline: records heap snapshots every ≤50ms; blue bars = objects still live at end; useful for pinpointing where allocations accumulate.
- Allocation Sampling: shows memory allocation by JavaScript function; Heavy (Bottom Up) view surfaces biggest allocators first.

## Connections
[[JavaScript Memory Management]], [[Web Performance]]

## Quotes
