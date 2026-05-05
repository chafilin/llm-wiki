---
title: Understand and Manage Flaky Tests in Bitbucket Pipelines
type: source
raw: raw/articles/Understand and Manage Flaky Tests in Bitbucket Pipelines.md
date_ingested: 2026-05-04
tags: [flaky-tests, ci, bitbucket, tooling]
---

## Summary
Bitbucket Pipelines documentation for built-in flaky test detection. Calculates a flakiness score 0–100 based on pass/fail flips (recent flips weighted more), auto-marks tests above threshold 80, and allows manual override. Configurable per repository.

## Key takeaways
- Flakiness score 0–100; default threshold: 80; minimum 10 executions before flagging
- Auto-detection enabled by default for all repos
- Manual management: lock test as flaky for 15 days via UI dropdown
- Configurable: toggle auto-detection/quarantine, adjust threshold, minimum runs
- Test Summaries: aggregate data up to 250 runs within 90 days (failure rate, duration variance)
- After marking flaky: fix immediately or quarantine temporarily

## Connections
[[Flaky Tests]]
