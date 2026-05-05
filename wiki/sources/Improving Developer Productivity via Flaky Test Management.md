---
title: Improving Developer Productivity via Flaky Test Management
type: source
raw: raw/articles/Improving Developer Productivity via Flaky Test Management.md
date_ingested: 2026-05-04
tags: [flaky-tests, ci, microsoft, quarantine, developer-productivity]
---

## Summary
Microsoft's enterprise-scale flaky test management system, integrated into CloudBuild and CloudTest. The system handles the full lifecycle: detect flakiness via retry signals, auto-file bugs with ownership, quarantine the test while still running it, and exit quarantine when the bug is closed. Deployed across 100+ teams; has caught ~49k flaky tests and prevented ~160k session failures.

## Key takeaways
- Three phases: **Inference** (detect via retry patterns) → **Reporting** (auto-file bugs, auto-assign owners) → **Mitigation** (quarantine but keep running).
- Critical insight: quarantined tests are still executed — only their failures are suppressed. You never go blind to them.
- Ownership assignment falls back to "who touched this test most recently" when no explicit owner exists.
- Cultural enforcement: some teams block PRs for developers with >10 open flaky test bugs. Turns flakiness into a personal queue item.
- Tests automatically exit quarantine when their bug is closed — no manual cleanup needed.

## Connections
[[Flaky Tests]] [[Testing Philosophy]] [[Software Development]]
