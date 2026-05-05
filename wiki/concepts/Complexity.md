---
title: Complexity
type: concept
updated: 2026-05-04
---

## Definition
The invisible accumulation of interdependencies, abstractions, and indirection that makes a system harder to understand and change than necessary. It compounds — once it enters a codebase, it attracts more.

## Why it matters
Every hour spent debugging, every "change here breaks unrelated thing there", every onboarding that takes weeks instead of days — that's complexity tax. The best engineers aren't the ones who write the cleverest code; they're the ones who keep complexity low.

## How it enters
- Features added without pushback ("yes" is the easy word)
- Abstractions introduced before the shape of the system is understood
- Over-engineering: solving hypothetical future problems
- Premature factoring / microservices / SoC applied too eagerly
- Generics and type system overuse
- Big refactors that drift too far from shore

## How to fight it
- **Say no** — the most powerful word in engineering (at career cost)
- **80/20 solutions** — deliver most value with least code
- **Wait for cut points** — don't abstract until the system reveals its own shape
- **[[Locality of Behavior]]** — keep code near what it operates on
- **[[Chesterton's Fence]]** — don't remove what you don't understand
- **Name intermediate values** — verbose and debuggable beats clever and opaque
- **Simple duplication** over complex DRY when the abstraction would be more complex than the repetition

## Open questions
- Where is the line between "useful abstraction" and "complexity demon"? Grug says wait for cut points, but how long is too long?

## Connections
[[The Grug Brained Developer]] [[Locality of Behavior]] [[Chesterton's Fence]] [[Software Development]]
