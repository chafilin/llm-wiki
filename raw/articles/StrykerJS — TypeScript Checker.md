# StrykerJS — TypeScript Checker

**Source:** https://stryker-mutator.io/docs/stryker-js/typescript-checker/

## What It Is

A plugin that validates each mutant against TypeScript's type system before running tests. Invalid mutations are marked as `CompileError` rather than consuming test cycles.

## Why It's Needed

Mutation testing generates many code variations. Without type checking, TypeScript-invalid mutants still run through the entire test suite — wasting time on guaranteed failures.

## Configuration

```json
{
  "checkers": ["typescript"],
  "tsconfigFile": "tsconfig.json",
  "typescriptChecker": {
    "prioritizePerformanceOverAccuracy": true
  }
}
```

- `tsconfigFile` defaults to `'tsconfig.json'`; supports project references for `--build` mode
- `prioritizePerformanceOverAccuracy: true` (default) — fastest strategy, occasional false negatives
- `prioritizePerformanceOverAccuracy: false` — complete accuracy, slower

## Key Features

- In-memory type checking (no disk side effects)
- Supports single projects and multi-project references
- Automatic compiler option overrides to prevent false positives

## Installation

```bash
npm install --save-dev @stryker-mutator/typescript-checker
```

Requires peer deps: `typescript` and `@stryker-mutator/core`.
