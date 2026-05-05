# Vitest — Features

**Source:** https://vitest.dev/guide/features

## Overview

Vitest is a modern testing framework built on Vite. Key differentiator: reuses Vite's config, transformers, resolvers, and plugins — no duplicate configuration.

## Watch Mode

"Smart & instant watch mode, like HMR for tests." Only reruns tests related to modified files.

## Parallelism & Performance

- Tests run in multiple processes by default (`node:child_process`)
- `--pool=threads` flag for worker thread execution
- `.concurrent` annotation for concurrent test execution within a file
- Sharding support for distributed CI execution

## Test Filtering

Multiple targeting options: test name matching, tag-based selection, file pattern filtering.

## Assertions & Mocking

- Chai built-in for assertions
- Jest-compatible `expect` API
- `vi` object for function mocks, module mocking
- DOM environments: happy-dom and jsdom

## Coverage

- Native v8 coverage
- Instrumented Istanbul
- Via `--coverage` CLI flag

## Snapshot Testing

Jest-compatible snapshot API.

## Advanced Features

- TypeScript/JSX out-of-the-box
- In-source testing (tests colocated with implementation)
- Benchmarking via Tinybench
- Type testing with `expect-type`
- Component testing: Vue, React, Svelte, and others
- Browser mode for real browser execution
- Project-based organization for monorepos
- Auto-detection of unhandled rejections and uncaught exceptions
