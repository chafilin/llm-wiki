# CircleCI — Test Insights

**Source:** https://circleci.com/docs/guides/insights/insights-tests/

## Overview

Feature for analyzing test performance across recent executions. Access via **Tests** tab on the **Workflow Insights** page. Supports organizations using OAuth authentication (GitHub, Bitbucket).

## Performance Summary

Displays test suite performance across the 100 most recent runs:
- Average tests per run
- Count of flaky tests detected
- Failure counts
- Slow run times

## Most Recent Runs Chart

Last 100 test suite executions. Hover for: test count, skipped tests, test success rate.

## Flaky Tests

Identifies "tests that fail non-deterministically due to external state factors." Detection uses a **14-day window** — flags tests that both passed and failed on the same commit. Labeled `FLAKY` throughout the app.

## Most Failed Tests

100 tests with the lowest success rates. Shows: test name, job, runtime, success rate.

## Slowest Tests

100 tests with the longest runtimes. Shows: test name, job, runtime, success rate.
