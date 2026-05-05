# Understand and Manage Flaky Tests in Bitbucket Pipelines

**Source:** https://support.atlassian.com/bitbucket-cloud/docs/understand-and-manage-flaky-tests-in-bitbucket-pipelines/

## What Are Flaky Tests?

Tests that produce inconsistent results without code changes — stemming from timing issues, shared state, external dependencies, or environmental factors.

## Why They Matter

- Hide real bugs
- Erode confidence in the entire suite
- Slow development (re-running pipelines, investigating non-issues)
- Increase costs (wasted compute)
- Developers start ignoring failures → reduced code quality

## Bitbucket Pipelines Features

**Test Summaries:** Aggregates per-test data across up to 250 runs within 90 days. Shows failure rate, average duration, variance.

**Test Executions:** Drill-down view with individual run details.

## Automatic Flaky Test Detection

Calculates a **flakiness score (0–100)** based on outcome flips between passes and failures. Recent flips weighted more heavily.

**Defaults:**
- Threshold: 80 (tests scoring ≥80 auto-marked flaky)
- Minimum executions: 10 runs required before flagging
- Enabled by default for all repositories

After marking as flaky: fix immediately or quarantine temporarily.

## Manual Management

1. Navigate to Tests page
2. Find specific test
3. Select dropdown in Test state column
4. Choose "Flaky"

Manual changes lock the test for 15 days.

## Configuration (Admin Only)

Via "Configure detection" button or Repository settings > Tests > Detection settings:
- Toggle auto-detection on/off
- Toggle auto-quarantine on/off
- Adjust flakiness score threshold
- Set minimum runs requirement
- Configure quarantine-specific thresholds
