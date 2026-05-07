---
title: Responsive Design
type: concept
updated: 2026-05-07
---

## Definition

Responsive design (Ethan Marcotte) uses fluid layouts and CSS media queries to make a single codebase adapt to any screen size. Adaptive design (Aaron Gustafson, 2011) instead detects the screen size and serves one of several pre-built fixed layouts — typically 6 breakpoints: 320, 480, 760, 960, 1200, 1600px. The two approaches trade off control and performance against maintainability and SEO.

## Why it matters

Every project needs a deliberate choice here. Defaulting to responsive without considering the trade-offs leads to mobile sites that download desktop assets (slow) or layouts that break at unexpected sizes. Adaptive is often the right choice for high-performance consumer products but is rarely worth it for internal tools or content sites.

## Key trade-offs

| Aspect | Responsive | Adaptive |
|--------|-----------|---------|
| Implementation | Easier, faster | Labor-intensive |
| Mobile speed | Slower (desktop assets downloaded) | 2–3× faster |
| SEO | Superior (single URL) | Problematic (duplicate content) |
| Design control | Limited | Precise per breakpoint |
| Cost | Lower | Significantly higher |
| Maintenance | Single codebase | Multiple layouts to keep in sync |

## When to choose responsive

- Content sites, blogs, marketing pages
- Internal tools
- Budget-constrained projects
- When SEO is a primary concern
- CMS-driven sites (templates are responsive by default)

## When to choose adaptive

- High-traffic consumer products where mobile speed is a differentiator
- Location-aware or sensor-aware apps
- When the mobile and desktop experiences are fundamentally different (not just rearranged)
- Retrofitting an existing desktop-only site

## Key facts

- Amazon, USA Today, Apple use adaptive
- Google treats responsive and adaptive equally for ranking (mobile-first indexing applies to both)
- Separate "m." mobile sites have fallen out of favor — two codebases to maintain, and they've lost the SEO advantage they once had
- Adaptive's SEO problem can be mitigated with `rel="canonical"` and `Vary: User-Agent` headers, but it's still more complex

## Examples

- A chat widget (like Manychat's) benefits from adaptive: the mobile embed experience can be fully touch-optimized without compromise
- A documentation site: pure responsive, no brainer
- A major e-commerce platform with dedicated mobile team: adaptive, because mobile conversion rate differences at scale justify the cost

## Connections

[[Web Performance]] [[Software Development]]
