# Pre-Submit UI Tests at Pinterest

**Source:** https://medium.com/pinterest-engineering/pre-submit-ui-tests-at-pinterest-556be1611be
**By:** Pinterest Engineering
**Date:** January 10, 2022

## Goal

Run E2E UI tests before every commit to Android and iOS repos. Result: failure resolution time decreased, pass rates from <50% to >90%.

## Four Major Challenges

### 1. Ownership

Each test requires exactly one responsible team. **Silencing mechanism:** teams can temporarily ignore failing tests with a 2-week resolution deadline.

### 2. Speed and Cost

~700 builds/week, 300 tests/build. Solutions:
- 5-minute test timeouts
- Fast-fail mechanisms
- Test simplification through deep linking
- Skip retries on silenced tests
- Android: Firebase Test Lab with **Flank's "Smart Flank"** for intelligent sharding
- iOS: Custom scheduler "pinpill" built on bluepill to manage simulator resources

### 3. Developer Experience

- Video recordings of test failures
- Centralized dashboards with ownership info
- One-click test silencing
- On-call rotation with office hours
- Result caching — skip unnecessary reruns

### 4. Main Branch Stability

- A/B test experiments snapshotted every 30 minutes with pre-submit validation
- **Stability Enforcer:** auto-silences tests exceeding 20% flakiness
- On-call monitoring during business hours

## Key Metrics

1. Main Branch Pass Rate — targeting reliability during business hours
2. Test Speed — P90 target: 30-minute E2E completion
3. Silenced Tests — monitoring that excessive silencing doesn't indicate systemic issues
4. Test Count — suite remains maintainable

## Implementation Phases

1. **Polish and Prepare** — weeks of quality improvement + dry runs
2. **Opt-In** — 10–15% of diffs from select teams for 2 weeks
3. **Opt-Out** — activate universally, maintain bypass mechanisms, disable post-submit

## Results

~90% pass rates, significantly reduced on-call burden.
