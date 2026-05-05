# Buildkite — Speed Up Builds with the Test Engine Client (bktec)

**Source:** https://buildkite.com/docs/test-engine/speed-up-builds-with-bktec

## What bktec Is

Buildkite's official CLI that leverages Test Engine historical data to enhance pipeline performance and reliability.

## How It Speeds Up Builds

### Test Splitting
Partitions test suites based on historical timing data. "bktec split tests automatically based on your historical timing data, and maintains peak speed through continuous optimization and automated re-balancing." Example: execution time drops from 10 minutes to ~4 minutes.

### Test State Management (Enterprise only)
Quarantines problematic tests by marking them as skipped or muted. "A test marked with _mute_ within a test suite will still be executed, but the result of the test will be ignored." Prevents flaky tests from blocking builds without removing them from the suite.

## Availability

- Test splitting: Pro and Enterprise plans
- Test state management (muting/skipping): Enterprise plan only
