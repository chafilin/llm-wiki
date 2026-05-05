# Spark Joy by Running Fewer Tests

**Source:** https://shopify.engineering/spark-joy-by-running-fewer-tests
**Author:** Jessica Xie
**Published:** June 11, 2020

## The Problem

Shopify monolith: 150,000+ tests, 30–40 minutes to run in parallel. Suite growing 20–30% annually. High frequency of intermittently failing tests from timing issues, DB instability, HTTP mocking problems, random generators, test state leakage.

## Dynamic Analysis Solution

Logs method calls during test execution to create call graphs — maps which files each test exercises. Enables selecting only tests affected by modified code.

## Key Metrics

- **Recall rate:** 99.94% (detected 8,355 of 8,360 failing tests)
- **Selection rate:** ~60% of tests needed per build
- **Impact:** 40% of builds required fewer than 20% of total tests
- **Compute savings:** ~25% reduction in infrastructure costs

## Implementation Challenges

**Untraceable files:** Non-Ruby assets (YAML, JSON, JS) required custom Rails patches for tracing.

**Metaprogramming:** Dynamic code patterns needed glob-rule-based file path detection.

**Mapping lag:** Async analysis → runs occasionally missed recent changes. Solution: run all modified-file tests plus mapped tests.

**Stale mappings:** Full suite runs on every deploy + auto-disabling of persistently failing tests.

## Rejected Alternatives

- Static analysis — insufficient strict Sorbet type coverage
- Machine learning — deterministic approaches preferred
- More infrastructure — gains diminished beyond resource thresholds

## Result

Developers requested full test suite runs on fewer than 2% of PRs. Reduced intermittent failures → faster development velocity.
