# Memory Terminology in Chrome DevTools

Source: https://developer.chrome.com/docs/devtools/memory-problems/memory-101/

## Overview

Memory analysis involves understanding how JavaScript objects consume memory and interact with garbage collection. This guide covers essential concepts used in the Chrome DevTools Heap Profiler.

## Object Sizes

Objects can hold memory in two distinct ways:

1. **Directly** through the object itself
2. **Indirectly** by maintaining references to other objects, preventing garbage collection

### Shallow Size

"This is the size of memory that is held by the object itself." Typically, only arrays and strings consume significant shallow size. JavaScript objects usually maintain some reserved memory for their description and immediate values.

### Retained Size

"This is the size of memory that is freed once the object itself is deleted along with its dependent objects that were made unreachable from GC roots."

**GC (Garbage Collection) Roots** consist of handles created from native code references to JavaScript objects:
- Window global objects (in each iframe)
- DOM trees with native nodes
- Debugger contexts and DevTools console evaluations

The root object (typically `window` in browsers) cannot be garbage collected.

## Objects Retaining Tree

The heap forms a network called a memory graph:

- **Nodes**: Labeled by constructor function names
- **Edges**: Labeled by property names

The "distance" metric indicates how far an object sits from the GC root on the shortest retaining path.

## Dominators

A dominator tree structure emerges where each object has exactly one immediate dominator. "A dominator of an object may lack direct references to an object it dominates; that is, the dominator's tree is not a spanning tree of the graph."

## V8 JavaScript Virtual Machine Specifics

### Primitive Types

Three primitive types in V8:
- **Numbers**: Stored as 31-bit small integers or heap numbers
- **Booleans**: True or false values
- **Strings**: Located in VM heap or renderer memory with wrapper objects

### Object Storage

JavaScript objects allocate memory from a dedicated VM heap, managed by V8's garbage collector. Native objects exist outside the JavaScript heap and require wrapper objects for access.

- **Cons strings**: Result from concatenation operations, joining only when necessary
- **Arrays**: Serve as primary data structures, supporting both named properties and numeric elements
- **Maps**: Describe object kinds and layouts, enabling fast property access

### Object Groups

Native object groups consist of interconnected objects with mutual references. DOM subtrees exemplify this — nodes reference parents, children, and siblings. While wrapper objects reference native objects, GC prevents uncollectable cycles. However, retaining even one wrapper holds the entire group.
