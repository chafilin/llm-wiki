# Playwright — Test Sharding

**Source:** https://playwright.dev/docs/test-sharding

## Overview

Playwright supports distributing test execution across multiple machines via sharding. "Sharding in Playwright means splitting your tests into smaller parts called 'shards'. Each shard is like a separate job that can run independently."

## Basic Implementation

Use `--shard=x/y` flag:

```bash
npx playwright test --shard=1/4
npx playwright test --shard=2/4
npx playwright test --shard=3/4
npx playwright test --shard=4/4
```

Running concurrently on separate CI jobs reduces total execution time by ~75% with four shards.

## Shard Balancing Strategies

**With `fullyParallel: true`:** Individual tests distribute evenly — optimal load distribution.

**Without `fullyParallel`:** Entire test files assign to shards. Requires consistently-sized test files; uneven files cause some shards to finish much faster.

## Report Merging

Blob reporter consolidates test data across shards:

```js
export default defineConfig({
  reporter: process.env.CI ? 'blob' : 'html',
});
```

Merge reports:
```bash
npx playwright merge-reports --reporter html ./all-blob-reports
```

## GitHub Actions Integration

GitHub Actions matrices automate sharding orchestration with automatic job creation per shard, followed by artifact-based report aggregation.
