---
title: Technical Debt
type: concept
updated: 2026-05-07
---

## Definition

Technical debt is the accumulated cost of shortcuts taken during development — code that works now but will cost more to maintain, extend, or fix later than if it had been done properly. The metaphor (Ward Cunningham) is financial: you borrow against future productivity. Like financial debt, some is strategic and manageable; some is reckless and compounds.

## Why it matters

Not all debt is bad — the problem is accumulating it without intention or a repayment plan. Distinguishing types of debt prevents both extremes: teams that never ship because they're pursuing perfection, and teams buried under maintenance that kills velocity.

## Fowler's Technical Debt Quadrant

Two axes classify debt:

|  | **Deliberate** | **Inadvertent** |
|--|----------------|-----------------|
| **Reckless** | "We'll fix it later" (no plan) | "We didn't know better" |
| **Prudent** | "We know the trade-off" (documented) | "Now we see the problem" |

Only Prudent-Deliberate debt is actually strategic. The rest is just mess.

## The central question

**Will this feature persist?**

- Mission-critical, long-lived feature → invest in proper architecture
- One-off campaign, internal tool, throwaway prototype → omega mess is fine

## Three tiers of debt by consequence

**The Good** — Upgradeable shortcuts. Skip WebSockets initially, add polling. Ship now, upgrade when demand proves it. Cost to fix later is low.

**The Bad** — Hidden friction. Background jobs without retry logic, admin pages without pagination. Seem fine until they fail silently or collapse under load. Cost compounds quietly.

**The Ugly** — Entrenching debt. Business logic embedded in infrastructure code, god methods with hundreds of lines. Every change is risky. Switching anything requires rewriting everything.

## Omega messes (Sandi Metz)

Ugly-but-contained code that's acceptable as a trade-off for isolated, non-critical work. The key word is **contained** — omega messes must not bleed into core systems.

## Five questions before incurring debt

1. How flexible is the deadline? (Rigid timeline → only with repayment plan)
2. How critical is this feature? (Mission-critical → no shortcuts)
3. How likely is it to evolve? (High change → needs flexible architecture)
4. How easy is it to refactor later? (Some shortcuts are one-liners to fix; others require rewrites)
5. When will we pay it back? (Document the rationale and schedule the work)

## Examples

- Polling instead of WebSockets on a dashboard — Good debt, clear upgrade path
- Background job with no retry logic — Bad debt, invisible until it fails in production
- Embedding pricing logic inside the email delivery job — Ugly debt, now you can't change either without touching both

## Connections

[[Software Development]] [[Complexity]] [[Typecraft — When Technical Debt is the Right Answer]]
