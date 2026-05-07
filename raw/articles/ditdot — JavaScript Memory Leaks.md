# Causes of Memory Leaks in JavaScript and How to Avoid Them

Source: https://www.ditdot.hr/en/causes-of-memory-leaks-in-javascript-and-how-to-avoid-them

## What Is a Memory Leak?

The browser stores objects in heap memory while they remain reachable from the root through a reference chain. A background garbage collector identifies and removes unreachable objects, reclaiming memory.

"A memory leak occurs when an object in memory that is supposed to be cleaned in a garbage collection cycle stays reachable from the root through an unintentional reference by another object."

Memory leaks are difficult to detect since browsers don't throw errors. Performance degradation signals a potential leak. Detection tools include:

- **Task Manager**: Shows JavaScript memory footprint per tab (Shift+Esc in Chrome; about:performance in Firefox)
- **Chrome Performance Tool**: Visual heap memory analysis
- **Memory/Developer Tools**: Heap snapshots comparing consecutive states

## Six Common Sources of Memory Leaks

### 1. Accidental Global Variables

Variables assigned without declaration or via `this` in non-strict mode leak into the global scope and never get garbage collected.

```javascript
function createGlobalVariables() {
  leaking1 = 'I leak into the global scope';
  this.leaking2 = 'I also leak into the global scope';
}
```

**Prevention**: Enable strict mode (`'use strict'`) to trigger console errors.

### 2. Closures

Inner functions retain references to outer scope variables even after execution completes. "The closure will keep the variables referenced and alive although the function has finished executing."

```javascript
function outer() {
  const potentiallyHugeArray = [];
  return function inner() {
    potentiallyHugeArray.push('Hello');
  };
}
```

**Prevention**: Understand when closures form, what they retain, and their expected lifespan.

### 3. Timers

`setTimeout` and `setInterval` callbacks prevent garbage collection of referenced objects as long as callbacks remain invocable.

```javascript
setInterval(setCallback(), 1000); // no way to stop it
```

**Prevention**: Store timer IDs and use `clearInterval()` or `clearTimeout()` when appropriate.

### 4. Event Listeners

Active event listeners prevent garbage collection of variables in their scope. They persist until explicitly removed or the DOM element is deleted.

```javascript
document.addEventListener('keyup', function() {
  doSomething(hugeString); // held indefinitely
});
```

**Prevention**:
- Use named functions and `removeEventListener()`
- Use `{once: true}` for single-execution listeners:

```javascript
document.addEventListener('keyup', listener, {once: true});
```

### 5. Cache

Unbounded caches accumulate objects indefinitely without cleanup logic.

**Prevention**: Use `WeakMap` with object keys, which automatically removes entries when objects are garbage collected:

```javascript
const weakMapCache = new WeakMap();
user_1 = null; // entry automatically removed after GC
```

### 6. Detached DOM Elements

Variables holding references to removed DOM nodes prevent garbage collection, even though elements are no longer in the DOM tree.

```javascript
const detachedDiv = createElement();
document.body.appendChild(detachedDiv);
document.body.removeChild(detachedDiv); // div still referenced
```

**Prevention**: Keep DOM references in local scope so they're released when functions complete.

## Conclusion

"When it comes to memory and performance, it is the user experience that is at stake." Understanding typical memory leak sources prevents future issues before they degrade production performance.
