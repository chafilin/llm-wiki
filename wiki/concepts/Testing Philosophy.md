---
title: Testing Philosophy
type: concept
updated: 2026-05-04
---

## Definition
A framework for deciding what to test, when, and at what level — as opposed to dogma (TDD, 100% coverage, "test everything first").

## The sweet spot: integration tests
- **Unit tests**: fine early, but break on refactors (they test implementation, not API). Don't get attached.
- **Integration tests**: test correctness at cut points — high enough to verify behavior, low enough to debug with a real debugger. These are the ones worth investing in.
- **End-to-end tests**: valuable but brittle. Keep a small, curated set covering the most critical paths. If they become unreliable they'll be ignored, which is worse than having none.

## When to write tests
Write most tests *after* the prototype phase, when the code's shape has firmed up. Writing tests before you understand the domain locks you into the wrong abstractions.

Exception: **bug regression tests**. When a bug is found, always write a failing test first, then fix. This is the one case where test-first consistently pays off.

## On mocking
Avoid mocks except when absolutely necessary, and then only at coarse grain — at system boundaries (cut points), not at individual function level. Fine-grained mocks give you tests that pass but lie about whether the system works.

## On flaky tests
Flaky tests are a trust problem, not just a time problem. Once developers learn to ignore CI noise, real failures start slipping through.

The industry consensus across Google, Microsoft, and Meta:
- **Don't block on them, but don't ignore them.** Mark as flaky, rerun automatically. [[Flaky Tests at Google and How We Mitigate Them]]
- **Quarantine, not delete.** Keep running the test, suppress the failure signal, auto-assign an owner to fix it. Going blind is worse than noise. [[Improving Developer Productivity via Flaky Test Management]]
- **Flakiness is a rate, not a boolean.** A test failing 0.1% vs. 25% of the time requires different responses. Score it. [[Probabilistic Flakiness]]

See [[Flaky Tests]] for the full treatment.

## On snapshot testing
Use sparingly. Valid for: error messages, Babel AST output, CSS-in-JS styles. Invalid for: entire component trees. Keep them small (dozens of lines), inline when possible, deterministic (mock Date/Math.random). Large snapshots become rubber-stamped in review. See [[Snapshot Testing]] for the full treatment. [[Effective Snapshot Testing — Kent C. Dodds]]

## Pre-commit testing
`jest --bail --findRelatedTests` (via lint-staged) runs only tests related to staged files before committing. The right flag for pre-commit: `--findRelatedTests` (not `--onlyChanged`, which ignores staged files). [[Running Jest Tests Before Each Git Commit]]

## Tooling (modern JS)
**Vitest** is the current standard for Vite-based projects: Vite-native, Jest-compatible API, HMR-like watch mode, built-in coverage (v8/Istanbul), sharding, browser mode. [[Vitest — Features]]

## Don't test library internals
Test user-facing behavior, not implementation details. Bad: test that a Vue computed property returns an array length. Good: assert that a dropdown renders when data exists. [[GitLab — Frontend Testing Standards]]

## DOM query best practices
- `screen.getByText()` not `const { getByText } = render(...)` [[Test Linting]]
- `getBy*` for presence assertions (throws = better error); `queryBy*` for absence (returns null = assertion can run) [[Test Linting]]

## Open questions
- How does this map to frontend testing specifically? Component tests, visual regression, interaction tests? (Partially answered: see [[Snapshot Testing]], [[Test Linting]])

## Connections
[[The Grug Brained Developer]] [[Complexity]] [[Software Development]] [[Flaky Tests]] [[Snapshot Testing]] [[Test Linting]] [[Mutation Testing]] [[Test Coverage]] [[Flaky Tests at Google and How We Mitigate Them]] [[Improving Developer Productivity via Flaky Test Management]] [[Probabilistic Flakiness]] [[Vitest — Features]] [[GitLab — Frontend Testing Standards]] [[Running Jest Tests Before Each Git Commit]] [[Effective Snapshot Testing — Kent C. Dodds]]
