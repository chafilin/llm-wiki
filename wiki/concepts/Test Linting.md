---
title: Test Linting
type: concept
updated: 2026-05-04
---

## Definition
The use of ESLint rules specifically for test code to catch structural problems that allow tests to silently pass while verifying nothing. Tests can have bugs just like production code.

## Why It Matters

A test that runs without throwing an error is considered "passing" by Jest/Vitest/Playwright — regardless of whether it actually asserted anything. Structural test bugs (no assertions, conditional assertions, wrong query type) are invisible to the test runner but caught by linters.

## Key Rule Categories

### Empty Tests
`jest/expect-expect` — triggers when a test has no `expect` call. Catches tests left empty, or tests where assertions were accidentally removed. [[eslint-plugin-jest — expect-expect Rule]]

### Conditional Assertions
`jest/no-conditional-expect`, `playwright/no-conditional-expect` — prevents `expect` inside `if`, `&&/||`, `catch`, promise `.catch()`. Conditional paths can silently be skipped; the test passes without asserting anything. "Jest only considers a test to have failed if it throws an error." [[jest — no-conditional-expect (OXC)]] [[eslint-plugin-playwright — no-conditional-expect]]

### Testing Library Query Patterns
`testing-library/prefer-screen-queries` — use `screen.getByText()` instead of destructuring from `render()`. Better autocomplete, consistent interface. [[eslint-plugin-testing-library — prefer-screen-queries]]

`testing-library/prefer-presence-queries` — use `getBy*` for presence assertions (throws if missing = better error), `queryBy*` for absence assertions (returns null = assertion can run). Using the wrong type gives misleading failures. [[eslint-plugin-testing-library — prefer-presence-queries]]

### Debug Artifacts
`testing-library/no-debugging-utils` — bans `debug()`, `prettyDOM()`, `logRoles()`, `logDOM()`, etc. from committed test code. Same principle as removing `console.log`. [[eslint-plugin-testing-library — no-debugging-utils]]

### Snapshot Size
`jest/no-large-snapshots` — limits snapshot size (default: 50 lines). Large snapshots are rubber-stamped in code review — "a stored snapshot is only as good as its review." [[eslint-plugin-jest — no-large-snapshots Rule]]

## Recommended Plugin Stack (Frontend)

```json
{
  "plugins": ["jest", "testing-library", "playwright"],
  "rules": {
    "jest/expect-expect": "warn",
    "jest/no-large-snapshots": ["warn", { "maxSize": 50 }],
    "testing-library/prefer-screen-queries": "error",
    "testing-library/prefer-presence-queries": "error",
    "testing-library/no-debugging-utils": "warn"
  }
}
```

`no-conditional-expect` depends on which runner you use (jest vs. playwright).

## Open questions
- Where's the right severity (warn vs. error) for each rule?
- Should `no-large-snapshots` be enforced at 50 lines or lower?

## Connections
[[Testing Philosophy]] [[Snapshot Testing]] [[GitLab — Frontend Testing Standards]] [[eslint-plugin-jest — expect-expect Rule]] [[jest — no-conditional-expect (OXC)]] [[eslint-plugin-playwright — no-conditional-expect]] [[eslint-plugin-testing-library — prefer-screen-queries]] [[eslint-plugin-testing-library — prefer-presence-queries]] [[eslint-plugin-testing-library — no-debugging-utils]] [[eslint-plugin-jest — no-large-snapshots Rule]]
