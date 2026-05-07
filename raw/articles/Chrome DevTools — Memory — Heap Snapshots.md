# Record Heap Snapshots in Chrome DevTools

Source: https://developer.chrome.com/docs/devtools/memory-problems/heap-snapshots/

## Overview

The heap profiler displays memory distribution across JavaScript objects and associated DOM nodes. This tool identifies memory leaks by analyzing how objects retain memory.

## Taking a Snapshot

1. Open DevTools and navigate to the **Memory** panel
2. Select the **Heap snapshot** radio button
3. Choose a JavaScript VM instance
4. Click **Take snapshot**

**Keyboard shortcut:** Press Cmd+E (macOS) or Ctrl+E (Windows/Linux).

"Snapshots show only the objects from the memory graph that are reachable from the global object. Taking a snapshot always starts with garbage collection."

## Viewing Snapshots

| View | Purpose |
|------|---------|
| **Summary** | Objects grouped by constructor; hunt down memory usage by object type |
| **Comparison** | Differences between two snapshots; verify operations don't create leaks |
| **Containment** | Heap structure overview; analyze closures and object references |
| **Statistics** | Pie chart showing relative memory allocation across categories |

### Summary View

The default view lists constructors with expandable object instances. Key columns:

- **Distance:** Shortest path to root
- **Shallow size:** Memory held by the object itself
- **Retained size:** Memory freed by deleting the object

### Special Constructor Entries

- **`(array)`** – Internal array-like objects storing JavaScript Array contents and object properties
- **`(compiled code)`** – V8 internal data enabling function execution
- **`(concatenated string)`** – Rope data structures from string concatenation
- **`InternalNode`** – C++ objects from Blink (browser engine)
- **`(object shape)`** – V8 hidden classes tracking object properties
- **`(sliced string)`** – Substring references without full character copying
- **`system / Context`** – Local variables from closures
- **`(system)`** – Miscellaneous internal objects

### Comparison View

Compare two snapshots to detect leaks:

1. Take an initial snapshot
2. Perform an action (e.g., open a document)
3. Reverse the action
4. Take a second snapshot and select **Comparison** view

The display shows added and deleted object instances between snapshots.

### Containment View

"Bird's eye view" of application object structure with entry points including:
- DOMWindow objects (global JavaScript scope)
- GC roots (garbage collector references)
- Native objects (DOM nodes, CSS rules)

### Retainers Section

Displays objects pointing to your selected object. Right-click and select **Ignore this retainer** to temporarily hide specific retainers.

## Finding Specific Objects

Use Ctrl+F to search heap snapshots by object ID.

## Named Functions and Closures

Name functions within closures to improve snapshot readability:

```javascript
// Without naming — hard to identify in snapshot
var lC = function() {
  return largeStr;
};

// With naming — appears distinctly in snapshot
var lC = function lC() {
  return largeStr;
};
```

## Uncovering DOM Leaks

DOM leaks often exceed expectations because child nodes maintain parent references:

```javascript
var select = document.querySelector;
var treeRef = select("#tree");
var leafRef = select("#leaf");

document.body.removeChild(treeRef);
treeRef = null; // #tree still referenced via leafRef
leafRef = null; // NOW #tree can be garbage collected
```

"#leaf" retains a reference to its parent recursively up the tree. Only when all references clear can the entire tree be garbage collected.
