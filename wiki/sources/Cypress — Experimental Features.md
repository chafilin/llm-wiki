---
title: Cypress — Experimental Features
type: source
raw: raw/articles/Cypress — Experimental Features.md
date_ingested: 2026-05-04
tags: [flaky-tests, cypress, testing-tools]
---

## Summary
Cypress experimental configuration options documentation. Most relevant for test reliability: two flake detection strategies and memory management improvements. Also covers WebKit support and performance optimizations.

## Key takeaways
- Two flake detection strategies: `detect-flake-and-pass-on-threshold` (pass if enough retries succeed) vs. `detect-flake-but-always-fail` (mark flaky but still fail build)
- `experimentalMemoryManagement`: improves memory handling in Chromium — helps with long-running suites
- `experimentalFastVisibility`: point sampling for faster visibility detection (better performance on complex DOM)
- `experimentalSingleTabRunMode` (component): runs all specs in a single tab for improved performance
- `experimentalWebKitSupport`: adds WebKit browser testing

## Connections
[[Flaky Tests]]
