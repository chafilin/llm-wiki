# How to Use the Allocation Timeline Tool

Source: https://developer.chrome.com/docs/devtools/memory-problems/allocation-profiler/

## Overview

The **Allocation timeline** tool helps developers identify objects that aren't being properly garbage collected and continue to retain memory. This feature combines detailed snapshot information from the heap profiler with incremental tracking capabilities.

## How the Tool Works

The Allocation timeline report integrates heap profiler snapshots with the Timeline panel's tracking features.

"The tool takes heap snapshots periodically throughout the recording (as frequently as every 50 ms!) and one final snapshot at the end of the recording."

**Note:** Object IDs (marked with @) persist across multiple snapshots, allowing precise heap state comparisons.

## Recording an Allocation Timeline Report

1. Open the **Memory** panel in DevTools
2. Enable the **Allocations on timeline** profile
3. Press the **Start** button to begin recording
4. Perform suspected memory leak actions
5. Stop the recording

## Reading a Heap Allocation Profile

The profile displays bars indicating when new objects are found in the heap:

- **Bar height** corresponds to the size of recently allocated objects
- **Blue bars** indicate objects still live at the timeline's end
- **Gray bars** indicate objects allocated but subsequently garbage collected

### Zooming and Filtering

Drag your mouse across a timeframe in the timeline to zoom in and filter the Constructor pane to show only objects allocated during that period.

### Analyzing Retaining Paths

Click a specific constructor in the Constructor pane to view its retaining tree in the Retainers pane. This reveals why objects weren't collected and guides necessary code changes.

## Memory Allocation by Function

Memory allocation can also be examined by JavaScript function using the **Allocation sampling** profile type. The default **Heavy (Bottom Up)** view displays functions allocating the most memory first, making it easy to identify which code paths are responsible for excessive allocations.
