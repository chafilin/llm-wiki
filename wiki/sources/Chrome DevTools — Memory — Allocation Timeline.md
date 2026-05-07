---
title: "Chrome DevTools — Memory — Allocation Timeline"
type: source
raw: raw/articles/Chrome DevTools — Memory — Allocation Timeline.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The Chrome DevTools guide to the Allocation Timeline (Allocations on timeline profile), which combines incremental heap snapshot tracking with timeline visualization to identify objects that persist in memory when they should be garbage collected.

## Key takeaways
- The tool takes heap snapshots as frequently as every 50ms throughout the recording, plus one final snapshot.
- Object IDs (prefixed with @) persist across snapshots, enabling precise before/after heap comparisons.
- Blue bars = objects still live at recording end (potential leaks); gray bars = objects already garbage collected (normal).
- Drag across a timeframe in the timeline to zoom and filter the Constructor pane to only objects allocated during that window.
- Click a constructor to view its retaining tree in the Retainers pane — this reveals why the object wasn't collected.
- Allocation Sampling (a separate profile type) attributes memory allocation by JavaScript function; Heavy (Bottom Up) view shows the worst allocators first.

## Connections
[[JavaScript Memory Management]]

## Quotes
> "The tool takes heap snapshots periodically throughout the recording (as frequently as every 50 ms!) and one final snapshot at the end of the recording."
