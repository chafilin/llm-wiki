# StrykerJS — Incremental Mode (GitHub Source)

**Source:** https://github.com/stryker-mutator/stryker-js/blob/master/docs/incremental.md

## Overview

_Available since Stryker 6.2_

Incremental mode tracks code and test changes and runs mutation testing only on changed portions, while still providing the full mutation report.

## Usage

```bash
npx stryker run --incremental
# or via stryker.config.json: "incremental": true
```

Results stored in `reports/stryker-incremental.json` (configurable via `--incrementalFile`).

## Reuse Conditions

- **Killed mutant**: culprit test still exists and didn't change → reused
- **Unkilled mutant**: no new test covers it and no tests changed → reused

Uses a git-like diff of code and test files against the previous incremental report.

## Statistics Output

```
Mutants:  1 files changed (+2 -2)
Tests:    2 files changed (+22 -21)
Result:   3731 of 3965 mutant result(s).
```

## Limitations

- Does not detect changes outside mutated files and test files
- Test file change detection requires test runner plugin support (see table)
- Environment changes (deps, env vars, `.snap` files) not tracked
- Static mutants have no test coverage tracking

## Test Runner Support Table

| Runner | Support |
|--------|---------|
| Jest | ✅ Full |
| CucumberJS | ✅ Full |
| Mocha | ⚠ Per-file, no location |
| Vitest | ⚠ Per-file, no location |
| Tap | ⚠ Per-file, no location |
| Jasmine | ⚠ Test names only |
| Karma | ⚠ Test names only |
| Command | ❌ Nothing |

## Forcing Reruns

```bash
npx stryker run --incremental --force --mutate src/app.js
npx stryker run --incremental --force --mutate src/app.js:5-7
```
