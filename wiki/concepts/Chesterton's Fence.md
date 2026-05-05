---
title: Chesterton's Fence
type: concept
updated: 2026-05-04
---

## Definition
Don't remove something until you understand why it was put there. If you can't explain its purpose, you don't have permission to delete it yet.

> "If you don't see the use of it, I certainly won't let you clear it away. Go away and think. Then, when you can come back and tell me that you do see the use of it, I may allow you to destroy it." — G.K. Chesterton

## Why it matters
Code that looks pointless usually isn't. It's either a workaround for a non-obvious bug, a guard against a race condition, a legal/compliance constraint, or it's simply handling an edge case you haven't seen yet. Removing it because "I don't see why this is here" is how you introduce production incidents.

## In practice
- Before deleting: write down *why* it exists. If you can't, read git blame and the surrounding tickets.
- Tests are often the hint — if deleting code breaks a test with a cryptic name, that test exists for a reason.
- "This looks dead" is not the same as "this is dead."

## Connections
[[The Grug Brained Developer]] [[Complexity]] [[Software Development]]
