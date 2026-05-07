---
title: JavaScript Memory Management
type: concept
updated: 2026-05-07
---

## Definition

JavaScript memory management is the practice of understanding how V8 allocates and frees heap memory, identifying objects that should be collected but aren't (memory leaks), and using Chrome DevTools profiling tools to diagnose the problem. A memory leak is any object that persists in heap memory beyond its intended lifetime due to an unintentional reference.

## Why it matters

Memory leaks manifest as progressive performance degradation — pages that start fast but slow down over time. In long-running SPAs (chat interfaces, dashboards, editors), leaks accumulate silently until the tab crashes or the user force-refreshes. Browsers don't throw exceptions for leaks; they just get slower.

## Key concepts

**Shallow vs. retained size:**
- Shallow size: memory the object itself holds
- Retained size: memory that would be freed if the object were deleted (including everything it keeps alive)
- The gap between shallow and retained is where leaks hide

**GC roots**: objects V8 will never collect. In browsers, this is `window` and each iframe's global. Everything reachable from a GC root survives garbage collection.

**Dominator tree**: an object A dominates object B if every path from the GC root to B passes through A. Removing A frees B. DevTools uses this to calculate retained sizes.

## Six common memory leak patterns

1. **Accidental globals**: assigning to undeclared variables leaks into `window`. Fix: `'use strict'` mode.

2. **Closures retaining large scope**: inner functions keep outer scope alive. Fix: understand what the closure captures; set large objects to `null` when done.

   ```javascript
   function outer() {
     const hugeArray = new Array(1_000_000);
     return () => hugeArray.push('item'); // hugeArray never freed
   }
   ```

3. **Forgotten timers**: `setInterval` callbacks keep their closure alive indefinitely. Fix: store the ID and call `clearInterval`/`clearTimeout`.

4. **Event listeners**: document-level listeners that capture large variables. Fix: `removeEventListener` with named function, or `{once: true}`.

   ```javascript
   // Leaks: anonymous function can't be removed
   document.addEventListener('keyup', () => doSomething(hugeString));
   
   // Safe: single-fire
   document.addEventListener('keyup', handler, {once: true});
   ```

5. **Unbounded cache**: plain object/Map grows forever. Fix: use `WeakMap` (entries auto-removed when key is GC'd) or implement eviction.

6. **Detached DOM nodes**: variables holding refs to removed DOM elements. The element (and its subtree) can't be collected. Fix: keep DOM refs in local scope, not module-level variables.

## Chrome DevTools profiling tools

**Task Manager** (Shift+Esc): quick sanity check — watch "JavaScript Memory" column. If it grows without bound, you have a leak.

**Performance panel → Memory**: timeline view of heap size. Sawtooth pattern = normal GC. Steadily rising floor = leak.

**Memory panel → Heap snapshot**: captures all reachable objects. Use Summary view filtered to "Detached" to find detached DOM trees. Use Comparison view between two snapshots to isolate what a specific action creates.

**Memory panel → Allocation timeline**: records allocations over time. Blue bars = still live; gray bars = collected. Zoom into a bar to see what was allocated in that window. Best for finding what a specific interaction allocates.

**Memory panel → Allocation sampling**: lower overhead; shows allocation by function. Use Heavy (Bottom Up) view to see the top offenders.

## Debugging workflow

1. Open Task Manager, watch JS memory while reproducing the suspected leak
2. If memory grows, open Memory panel → Allocation Timeline
3. Perform the leaking action, look for blue bars that persist
4. Click a persistent bar → expand Constructor → inspect Retainers to find what keeps it alive
5. For detached DOM: take Heap Snapshot → filter "Detached" → find the JS reference

## Examples

- Chat widget that attaches `keydown` listener on every message render without cleanup → listener count grows with conversation length
- SPA that caches API responses in a module-level Map → cache never evicted, grows indefinitely
- Component that holds a ref to a removed modal DOM node → entire modal subtree retained

## Connections

[[Web Performance]] [[Software Development]]
