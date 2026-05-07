# Fix Memory Problems in Chrome DevTools

Source: https://developer.chrome.com/docs/devtools/memory-problems/

## Overview

Memory issues significantly impact user experience. Three key performance problems users perceive:

- **Progressive degradation**: "A page's performance gets progressively worse over time," potentially indicating memory leaks
- **Consistent poor performance**: Memory bloat occurs when pages consume more memory than necessary
- **Frequent pauses**: Excessive garbage collection pauses script execution repeatedly

## Monitoring Memory in Real-Time

### Chrome Task Manager

Access via Shift+Esc or Chrome menu > **More tools** > **Task manager**.

Enable the JavaScript memory column by right-clicking the table header. This reveals two metrics:

- **Memory footprint**: OS memory usage; increasing values indicate DOM node creation
- **JavaScript Memory**: The live number (in parentheses) shows reachable object memory consumption

## Visualizing Memory Over Time

1. Open the Performance panel
2. Enable the Memory checkbox
3. Create a recording (force garbage collection at start/end is recommended)

The interface displays:
- **HEAP graph**: Shows JavaScript heap size
- **Counter pane**: Breaks down memory by JS heap, documents, DOM nodes, listeners, and GPU memory

## Identifying Detached DOM Trees

Detached DOM nodes (removed from the DOM but referenced by JavaScript) cause common memory leaks.

**Using Heap Snapshots:**

1. Open DevTools Memory panel
2. Select **Heap Snapshot** radio button
3. Click **Take snapshot**
4. Type "Detached" in the Class filter box
5. Expand results to investigate retained references

## Finding JavaScript Heap Leaks

### Allocation Timeline

1. Select **Allocations on timeline** radio button
2. Press Record
3. Perform suspected memory leak actions
4. Stop recording

Blue bars indicate new memory allocations. Zoom into bars to filter objects allocated during specific timeframes.

### Allocation Sampling

Select **Allocation sampling** to view memory allocation by function. The default **Heavy (Bottom Up)** view displays functions allocating the most memory first.

## Identifying Objects Retained by JavaScript

The **Detached elements** profile shows HTML nodes persisting due to JavaScript references, displaying exact node counts and HTML.

## Spotting Garbage Collection Issues

Frequently rising and falling memory values in Task Manager or Timeline recordings indicate excessive garbage collection. Use Allocation Timeline recordings to identify where allocations occur.
