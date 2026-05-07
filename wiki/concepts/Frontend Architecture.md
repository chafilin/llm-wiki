---
title: Frontend Architecture
type: concept
updated: 2026-05-07
---

## Definition

Frontend architecture is the decision about how much rendering and state management belongs in the browser vs. the server. The spectrum runs from fully server-rendered HTML (zero client JS) to fully client-rendered SPAs. Most sites are best served somewhere in the middle — and most teams default to SPAs without consciously making the trade-off.

## Why it matters

Framework choice has outsized impact on performance, accessibility, and long-term maintainability. React/Next.js is the default for most frontend teams, but CWV data shows HTML-first architectures consistently outperform SPA architectures on real devices. The choice is rarely revisited once made.

## The SPA threshold (Alex Russell)

Build a SPA only if **both** conditions are met:
- Average session duration > 10 minutes
- More than 10 updates to the same primary data per session

Most contemporary websites fail both tests. Productivity tools (dashboards, editors, chat) typically pass. Marketing sites, e-commerce, media, and informational sites typically don't.

## Use-case taxonomy

| Site type | Recommended architecture | Why |
|-----------|--------------------------|-----|
| Informational / blog | Static generator (Astro, 11ty, Hugo) | Short sessions, server-owned data, no interactivity |
| E-commerce | Server HTML + progressive enhancement | Variable sessions, fresh content, conversion depends on speed |
| Media | Progressive enhancement + Web Components (islands) | Mostly read, occasional rich interaction |
| Social / streaming | Hybrid (Hotwire, HTMX) | Mix of server state + streaming updates |
| Productivity tools | SPA (justified) | Long sessions, many updates to same data |

## Rule of Least Client-Side Complexity

Server code runs under controlled conditions. Client code runs on unpredictable devices over unreliable networks. HTML and CSS degrade gracefully and have higher compression ratios than JS. Ship the minimum amount of JavaScript that achieves the required UX.

## The "React is standard" myth

No two React setups are identical. TypeScript or not? Webpack, Vite, or Turbopack? Zustand, Redux, or context? RSC or not? The choices compound — the opposite of standardization. "Our team knows React" conflates tool familiarity with inability to learn anything else.

## Progressive enhancement as a guardrail

Start with HTML that works without JavaScript, then layer on interactivity. This forces clarity about what actually requires JS and ensures baseline accessibility and performance. Treating JS as optional by default is a forcing function against over-engineering.

## Key evidence

- CWV field data shows Next.js sites materially underperform HTML-first alternatives
- Low-end device performance has stagnated while high-end devices improve — JS tax falls disproportionately on the majority of users
- React's synthetic event system and hard-coded element list were designed around IE constraints that no longer exist

## Open questions

- At what scale does an island architecture (Astro) become harder to maintain than a SPA?
- How does Manychat's chat widget map to this taxonomy? (long sessions, many updates — SPA is probably justified)

## Connections

[[Software Development]] [[Web Performance]] [[Core Web Vitals]] [[Infrequently Noted — If Not React Then What]]
