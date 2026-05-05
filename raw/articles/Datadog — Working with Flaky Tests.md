# Datadog — Working with Flaky Tests

**Source:** https://docs.datadoghq.com/tests/flaky_tests/

## What Is a Flaky Test?

"A flaky test is a test that exhibits both a passing and failing status across multiple test runs for the same commit."

## Key Metrics for Prioritization

- **Average duration** — expected runtime
- **First/Last flaked dates** — timeline of when flakiness began and most recently occurred
- **Commits affected** — count of commits exhibiting flaky behavior
- **Failure rate** — percentage of failed runs since initial detection
- **Trend visualization** — whether the test remains actively flaky or has stabilized

## Tag Categories

Datadog classifies flaky tests with three tags:

- **Flaky** (`is_flaky`) — actively unreliable
- **New Flaky** (`is_new_flaky`) — recently introduced reliability issues
- **Known Flaky** (`is_known_flaky`) — previously identified; may indicate test instability rather than code issue

## Management Features

- Tests inactive for 30 days automatically disappear from tracking
- Manual removal via trash icon (reappears if flakiness recurs)
- Option to ignore mistakenly-flagged flaky tests per commit
