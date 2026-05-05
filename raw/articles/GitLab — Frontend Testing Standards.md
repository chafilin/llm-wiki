# GitLab — Frontend Testing Standards and Style Guidelines

**Source:** https://docs.gitlab.com/development/testing_guide/frontend_testing/

## Overview

GitLab uses **Jest** for JavaScript unit and integration testing, **Capybara** for E2E feature tests. Unit and feature tests required for all new features; regression tests for bug fixes.

## Core Principles

**Don't test library internals.** Test user-facing behavior, not Vue computed properties or library functionality. Bad: testing if `hasMetricTypes` returns array length. Good: asserting dropdown displays when metricTypes exist.

**Don't test your mock.** Mocks support tests, not become the test target.

**Use literal values in assertions** — not imported constants. Makes tests resilient to accidental changes.

## DOM Element Querying

Query semantically:
- DOM Testing Library's `byRole` for accessibility
- `findByText()` for visible text
- `data-testid` attributes (kebab-case) when necessary
- Avoid `.js-*` classes, template refs, generic class selectors

## Key Best Practices

- **Prefer `toBe` over `toEqual`** for primitives (faster via `Object.is`)
- **Use specific matchers:** `toHaveLength()`, `toBeUndefined()`, etc.
- **Avoid `toBeTruthy`/`toBeFalsy`** — too permissive
- **Use `async/await`**, not `done` callbacks for promises
- Unexpected console messages fail tests by default

## Non-Deterministic Tests

Avoid flaky tests by:
- Faking `Date` (enabled by default, use `useFakeDate()`/`useRealDate()`)
- Replacing `Math.random()` with `jest.spyOn(Math, 'random').mockReturnValue()`

## MSW Integration Tests

Bridge unit and Capybara tests. Mount full Vue app in jsdom, intercept API requests with fixture data. Use real `apolloProvider`, interact via native DOM APIs, assert on DOM not Vue state.

## Snapshots

Use **sparingly:**
- Protecting critical HTML structures from accidental changes
- Testing complex utility function outputs

Don't use for: Vue Test Utils assertions, component logic, UI depending on external dependencies.

## Feature Tests (Capybara)

When to use:
- Multi-component interactions
- Cross-page navigation
- Form submission with results
- Excessive mocking needed for unit tests

Prefer MSW integration tests for single-page scenarios (significantly faster).

## Debugging

Use `binding.pry` to pause execution and inspect live browser state. `WEBDRIVER_HEADLESS=0` for visible browser, `WEBDRIVER=firefox` for Firefox.
