# StrykerJS — Incremental Mode Documentation

**Source:** https://stryker-mutator.io/docs/stryker-js/incremental/

## Overview

Accelerates mutation testing by only running tests for changed code and tests while still delivering a complete mutation report.

## Configuration

```json
// stryker.config.json
{
  "incremental": true,
  "incrementalFile": "reports/stryker-incremental.json"
}
```

Or via CLI: `--incremental`, `--incrementalFile <path>`, `--force`

## Cache Mechanism

Reuses results when:
1. A killed mutant's culprit test still exists and is unchanged
2. An unkilled mutant has no new test coverage and existing tests are unchanged

Performs "a git-like diff of your code and test files to the previous version."

## Limitations

- Only detects changes in mutated files and test files — not config, deps, env vars, `.snap` files
- Test file change detection depends on test runner plugin support
- Static mutants lack test coverage tracking

## Test Runner Support

| Runner | Support |
|--------|---------|
| Jest | ✅ Full |
| CucumberJS | ✅ Full |
| Mocha | ⚠ Tests per file (no location) |
| Vitest | ⚠ Tests per file (no location) |
| Tap | ⚠ Tests per file (no location) |
| Jasmine | ⚠ Test names only |
| Karma | ⚠ Test names only |
| Command | ❌ Nothing |

## Forcing Reruns

```bash
npx stryker run --incremental --force --mutate src/app.js
npx stryker run --incremental --force --mutate src/app.js:5-7
```

The dry run phase is always required — it discovers tests and validates the setup.
