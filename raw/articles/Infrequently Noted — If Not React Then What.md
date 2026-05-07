# If Not React, Then What?

Source: https://infrequently.org/2024/11/if-not-react-then-what/

Author: Alex Russell

## Core Argument

Teams should stop using React for new projects. The fundamental problem isn't identifying an alternative framework — it's embracing **user-focused engineering** instead of "frameworkism" (the belief that adopting better tools solves all problems).

## Key Principles

### The Rule of Least Client-Side Complexity

Server-side code operates under controlled conditions. Client-side code runs on unpredictable devices across unreliable networks. Send less JavaScript overall, favoring HTML and CSS which "degrade gracefully and feature higher compression ratios."

### Engineering vs. Frameworkism

True engineering starts with user needs and constraints. Frameworkism assumes frameworks solve problems through adoption, often disconnected from evidence. "The only thing that makes web experiences good is caring about the user experience — specifically, the experience of folks at the margins."

## Technology Recommendations by Use Case

| Category | Recommendation | Why |
|----------|---|---|
| **Informational** | Static site generators (Hugo, Astro, 11ty) | Short sessions, server-owned data |
| **E-Commerce** | Server-generated HTML + progressive enhancement | Highly variable sessions, fresh content needed |
| **Media** | Progressive enhancement + Web Components (islands) | Works until features like mini-players required |
| **Social** | Hybrid approaches (Hotwire, HTMX) | Mix of fixed actions and streaming updates |
| **Productivity** | SPAs only when justified | Long sessions + many updates to same data |

### The SPA Decision Tree

Build as SPA only if:
- Average sessions exceed 10 minutes
- More than 10 updates to the same primary data occur per session

This threshold disqualifies most contemporary websites.

## Responding to Common Objections

**"We need to move fast"**
Speed achieved through complexity introduces technical debt faster than anything else. Teams get stuck remediating performance and accessibility issues, killing velocity.

**"Everyone has fast phones now"**
This ignores that low-end device performance has stagnated while high-end devices improve. Mobile constitutes the majority of traffic for most sites.

**"Our teams already know React"**
Web developers are polyglots by necessity. React knowledge transfers easily to alternatives. The claim conflates "knowing React" with "only capable of using React."

**"React is industry standard"**
No two React setups are identical. Choices about TypeScript, bundlers, and state management create endless variation — the opposite of standardization.

**"Next.js can be fast enough"**
Performance data shows Next.js sites materially underperform HTML-first alternatives. Even with React Server Components, the JavaScript tax remains.

## Decision-Making Framework

1. **User focus** — Hold teams accountable for user outcomes, including marginal users
2. **Evidence** — Use RUM data and Core Web Vitals to establish shared reality
3. **Guardrails** — Implement policies like progressive enhancement requirements
4. **Bake-offs** — Test architectures against defined critical user journeys

## The Larger Problem

React represents legacy design optimized for Internet Explorer's constraints that no longer exist. Its synthetic event system and hard-coded element lists create portability hazards. Meanwhile, "the React community's assertions about how browsers work" lack grounding in technical reality.

**Core message:** Stop asking "which framework instead?" Start asking "do we need a framework at all?" For most applications, the answer is no.
