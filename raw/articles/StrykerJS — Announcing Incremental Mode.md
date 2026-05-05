# StrykerJS — Announcing Incremental Mode

**Source:** https://stryker-mutator.io/blog/announcing-incremental-mode/
**Author:** Nico Jansen (Stryker Team)
**Date:** September 6, 2022

## What Incremental Mode Is

"StrykerJS will track the changes you make to your code and tests and only runs mutation testing on the changed code." Still generates a full mutation report.

## How It Differs from Full Runs

Traditional mutation testing analyzes all code. Incremental mode:
- Reuses prior mutant results when the mutant was previously killed and its covering tests haven't changed
- Reuses when untouched mutants have no new test coverage and existing tests are unchanged

## Performance Benefit

Concrete example: "3731 of 3965 mutant result(s)" reused — only 234 new mutants required execution.

## Technical Implementation

Uses Google's `diff-match-patch` library to identify file differences. First run generates baseline (`stryker-incremental.json`); subsequent runs reference it.

## Usage

```bash
# Enable incremental
npx stryker run --incremental

# Force rerun specific file, update incremental cache
npx stryker run --incremental --force --mutate src/app.js:5-7
```
