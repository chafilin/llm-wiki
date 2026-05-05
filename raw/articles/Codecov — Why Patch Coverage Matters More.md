# Why Patch Coverage is More Important Than Project Coverage

**Source:** https://about.codecov.io/blog/why-patch-coverage-is-more-important-than-project-coverage/
**Author:** Tom Hu
**Date:** January 3, 2024

## Project Coverage vs. Patch Coverage

**Project coverage:** Total test coverage across the entire codebase — every line, comprehensive. Pursuing 100% is unrealistic and burdensome.

**Patch coverage:** Test coverage for code changes in a specific pull request, commit, or patch. Measures whether newly introduced code is adequately tested.

## The Core Argument

"A developer should test their own code versus test all of the code."

Rather than 100% project coverage, teams should emphasize 100% patch coverage — ensuring every new line introduced is tested. This is:
- More actionable within developer workflows
- Reduces burden on engineering teams
- Identifies bugs before changes merge
- Improves overall software quality incrementally

## Implementation

1. Write code with accompanying tests
2. Run tests in CI/CD, review patch coverage report
3. Address coverage gaps for uncovered changes

Tools like Codecov automatically measure and report patch coverage as part of CI workflows.
