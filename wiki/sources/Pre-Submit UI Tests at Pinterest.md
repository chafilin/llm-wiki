---
title: Pre-Submit UI Tests at Pinterest
type: source
raw: raw/articles/Pre-Submit UI Tests at Pinterest.md
date_ingested: 2026-05-04
tags: [ci, mobile, ui-testing, ownership]
---

## Summary
Pinterest's system for running ~300 E2E mobile UI tests before every commit (700 builds/week). Covers ownership, speed optimization, developer experience, and main branch stability.

## Key takeaways
- Each test has exactly one responsible team; silencing mechanism with 2-week resolution deadline
- Speed: 5-minute timeouts, fast-fail, deep linking for simplification, Android Flank Smart Sharding, iOS custom "pinpill" scheduler
- Stability Enforcer: auto-silences tests exceeding 20% flakiness
- A/B test snapshots every 30 minutes to keep pre-submit validation current
- Progressive rollout: polish → opt-in (10-15%) → opt-out (universal)
- Result: <50% → >90% pass rate; reduced on-call burden

## Connections
[[CI Pipeline Speed]] [[Flaky Tests]] [[Developer Experience]]
