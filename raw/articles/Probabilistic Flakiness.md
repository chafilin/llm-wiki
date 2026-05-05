# Probabilistic Flakiness: How do you test your tests?

**Source:** https://engineering.fb.com/2020/12/10/developer-tools/probabilistic-flakiness/  
**Published:** December 10, 2020  
**Author:** Meta (Facebook) Engineering

## Core Problem

Meta faced a challenge: while automated tests detect product regressions, the tests themselves can become unreliable over time. "Flaky" tests produce inconsistent results without actual code changes, eroding developer trust and wasting time on false positives.

## The Solution: Probabilistic Flakiness Score (PFS)

Rather than asking whether tests are flaky, Meta's approach answers: **how flaky are they?** The PFS measures test reliability on a quantifiable scale applicable to any test framework or programming language.

## Key Insights

**Asymmetry of Results:** Developers treat passing and failing tests differently. A passing test suggests genuine code quality, while failures often trigger retries on the same code version—failures followed by passes indicate flakiness.

**Two-Parameter Model:** The statistical model estimates:
1. Probability of "bad state" (failures due to code or environmental factors)
2. Probability of failure in "good state" (the actual flakiness metric)

## Implementation

Meta uses Bayesian inference via the Stan probabilistic programming language to estimate PFS from observed test execution sequences. The approach requires no additional test runs—it leverages existing continuous integration data.

## Business Impact

PFS serves as both incentive and enforcement: teams receive dashboards tracking score changes, automatic tickets alert owners when flakiness increases, and persistently flaky tests become ineligible for predictive test selection—a meaningful consequence that drives reliability improvements across Meta's codebase.
