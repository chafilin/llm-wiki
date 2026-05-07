---
title: If Not React, Then What?
type: source
raw: raw/articles/Infrequently Noted — If Not React Then What.md
date_ingested: 2026-05-07
tags: []
---

## Summary

Alex Russell argues the question "which framework instead of React?" is the wrong question. The right question is whether you need a framework at all. He provides a use-case taxonomy mapping site types to appropriate architectures, a concrete SPA decision threshold, and rebuttals to common objections. The underlying principle is the Rule of Least Client-Side Complexity: client-side code runs on unpredictable hardware and networks; ship as little of it as possible.

## Key takeaways

- **Frameworkism**: the belief that adopting better tools solves problems — disconnected from user outcomes. True engineering starts with user constraints, not tooling choices
- **SPA threshold**: build a SPA only if sessions average >10 minutes AND >10 updates to the same primary data per session — disqualifies most websites
- **Use-case taxonomy**: informational → static generators (Astro, 11ty, Hugo); e-commerce → server HTML + progressive enhancement; social → Hotwire/HTMX; productivity → SPA only when justified
- **Rule of Least Client-Side Complexity**: server code runs in controlled conditions; client code runs on unknown devices over unreliable networks; HTML and CSS degrade gracefully and compress better than JS
- **Next.js underperforms**: even with React Server Components, the JavaScript tax remains; Next.js sites materially underperform HTML-first alternatives in CWV data
- **"Industry standard" is a myth**: no two React setups are identical (TypeScript? Webpack? Zustand? RSC?); the opposite of standardization
- **Low-end devices stagnate**: high-end phones improve; low-end phones don't; mobile is the majority of traffic for most sites
- Decision framework: user focus → RUM evidence → progressive enhancement guardrails → architecture bake-offs against critical user journeys

## Connections

[[Frontend Architecture]] [[Web Performance]] [[Software Development]] [[Core Web Vitals]]

## Quotes

> "The only thing that makes web experiences good is caring about the user experience — specifically, the experience of folks at the margins."

> "Stop asking 'which framework instead?' Start asking 'do we need a framework at all?'"
