---
title: The Grug Brained Developer
type: source
raw: raw/articles/The Grug Brained Developer.md
date_ingested: 2026-05-04
tags: [software, complexity, philosophy, frontend, testing]
---

## Summary
A satirical guide to software development written in cave-man dialect by Carson Gross (creator of htmx). The central thesis: complexity is the developer's greatest enemy, and most of software engineering wisdom is downstream of that one insight.

## Key takeaways
- Say "no" to features and abstractions as the primary weapon against complexity
- 80/20 solutions: 80% of value with 20% of code, often without telling the PM
- Don't factor/abstract code early — let cut points emerge from the shape of the system
- Integration tests are the sweet spot; unit tests break on refactors, e2e tests are hard to debug
- [[Locality of Behavior]] over [[Separation of Concerns]] — put code on the thing that does the thing
- [[Chesterton's Fence]] — understand code before removing it
- Type system's main value is IDE autocomplete, not correctness
- Named intermediate variables > clever one-liners (easier to debug)
- Simple duplication often better than complex DRY abstraction
- [[FOLD]] (Fear of Looking Dumb): senior devs saying "this is too complex" gives juniors permission too
- Logging is underrated — log all major branches, use request IDs in distributed systems
- Microservices: taking the hardest problem (factoring) and adding a network call
- Frontend specifically: React is the complexity demon; grug made htmx to escape it
- Keep refactors small and system working throughout; large refactors fail often
- Impostor syndrome is universal — if everyone is an impostor, nobody is

## Connections
[[Complexity]] [[Locality of Behavior]] [[Chesterton's Fence]] [[FOLD]] [[Software Development]] [[Testing Philosophy]]

## Quotes
> "given choice between complexity or one on one against t-rex, grug take t-rex: at least grug see t-rex"

> "grug wonder why big brain take hardest problem, factoring system correctly, and introduce network call too"
