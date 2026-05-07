# Total Blocking Time (TBT)

Source: https://web.dev/articles/tbt

## Overview

Total Blocking Time measures "the total amount of time after First Contentful Paint where the main thread was blocked for long enough to prevent input responsiveness." This lab metric helps evaluate load responsiveness and correlates strongly with Interaction to Next Paint (INP).

## What Constitutes Blocking Time

The main thread becomes "blocked" when a Long Task executes — any task running for more than 50 milliseconds. The blocking time for each long task equals its duration minus 50ms. Total blocking time is the sum of all blocking times after FCP.

### Example Calculation

| Task | Duration (ms) | Blocking Time (ms) |
|------|---------------|-------------------|
| Task one | 250 | 200 |
| Task two | 90 | 40 |
| Task three | 35 | 0 |
| Task four | 30 | 0 |
| Task five | 155 | 105 |
| **Total** | **560** | **345** |

## TBT vs. Related Metrics

**Relationship to INP:** TBT predicts potential INP issues but cannot replace field measurement of actual responsiveness.

**Relationship to TTI:** TBT better captures user-perceived responsiveness than Time to Interactive. Three 51ms tasks spread across 10 seconds yield 3ms TBT but push TTI back significantly.

## Good TBT Targets

Sites should target "less than 200 milliseconds when tested on average mobile hardware."

## Measurement Approach

**Lab Only:** Measure TBT using Lighthouse or WebPageTest. Field measurement is discouraged due to user interaction variance.

## Optimization Strategies

- Optimize long tasks
- Reduce third-party code impact
- Decrease JavaScript execution time
- Minimize main thread work
- Keep request counts and transfer sizes low
