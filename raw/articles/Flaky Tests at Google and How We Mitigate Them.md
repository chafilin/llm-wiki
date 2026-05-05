# Flaky Tests at Google and How We Mitigate Them

**Source:** https://testing.googleblog.com/2016/05/flaky-tests-at-google-and-how-we.html  
**Published:** May 27, 2016  
**Author:** John Micco

## Problem Definition

Flaky tests are those that don't reliably produce the same result across multiple runs, making it difficult to trust test outcomes and creating noise in CI/CD pipelines.

## Google's Mitigation Strategies

- Identifying and tracking flaky tests systematically
- Marking tests as flaky once patterns are detected
- Rerunning marked flaky tests rather than blocking commits
- Analyzing root causes to fix underlying issues

## Impact

Flaky tests waste developer time, generate duplicate bug reports, and obscure real failures. Google acknowledges they don't yet have precise cost metrics for flakiness at the time of writing.

## Community Approaches

Suggested approaches from the engineering community include:
- Using "Reservoir" systems to validate new tests before CI integration
- Implementing smart retry mechanisms with statistical analysis
- Separating environmental failures from genuine code bugs
- Following test pyramid principles to reduce UI test flakiness

## Tools Mentioned

- Flaky Test Handler Plugin for Jenkins
- dist_test for distributed test repetition

## Key Takeaway

Flaky tests are a universal testing challenge requiring systematic tracking and smart remediation rather than dismissal.
