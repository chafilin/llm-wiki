# Playwright Flaky Tests: How to Detect & Fix Them

**Source:** https://testdino.com/blog/playwright-flaky-tests/
**Author:** Savan Vaghani
**Published:** March 24, 2026

## Six Root Causes of Flakiness

1. **Timing (Async Wait Issues)** — #1 cause. Playwright auto-wait doesn't apply to custom DOM queries in `page.evaluate()`, raw `expect()` without Playwright matchers, or `locator.count()` snapshots.

2. **Shared State and Race Conditions** — Tests in parallel share database records or server-side state. Test order dependencies under parallel execution.

3. **Environment Differences** — Platform-specific rendering, resource constraints, Docker config.

4. **External Dependencies** — Unreliable third-party APIs, slow backends, network race conditions.

5. **Resource Leaks** — Unclosed browser contexts, connection pool growth.

6. **Non-Determinism** — Timezone assertions, random values, calendar-edge date logic.

**RAFTs (Resource-Affected Flaky Tests):** 46.5% of flaky tests fail because of infrastructure, not code. Tests pass locally (powerful machine) but fail on resource-constrained CI runners.

## Key Fixes

### Replace Arbitrary Waits with Web-First Assertions (Fixes ~45% of flakiness)

```typescript
// Flaky
await page.waitForTimeout(2000);
await page.click('button#submit');

// Reliable
await expect(page.getByRole('button', { name: 'Submit' })).toBeVisible();
await page.getByRole('button', { name: 'Submit' }).click();
```

### Promise-First Pattern for Network

```typescript
// Reliable: listener registered before action
const responsePromise = page.waitForResponse('/api/save');
await page.click('#submit');
const response = await responsePromise;
```

### Test Isolation

Every test creates its own data — no reliance on other tests' setup.

### Clock Control

```typescript
await page.clock.install({ time: new Date('2026-03-18T10:00:00') });
```

### Stable Locators

```typescript
// Fragile
await page.locator('.btn-primary').click();
// Stable
await page.getByRole('button', { name: 'Submit' }).click();
```

## Timeout Configuration

```typescript
export default defineConfig({
  timeout: 60_000,
  expect: { timeout: 10_000 },
  use: { actionTimeout: 15_000, navigationTimeout: 30_000 },
  retries: process.env.CI ? 2 : 0,
});
```

## Quarantine Process

```bash
# Tag flaky tests
test('@flaky login flow under load', ...)
# Exclude from main pipeline
npx playwright test --grep-invert @flaky
# Run separately (non-blocking)
npx playwright test --grep @flaky
```

Accountability required: ownership, tickets with deadlines, resolve within two sprint cycles or delete.

## Scale Solutions

- Slack: 57% → <4% failure rate
- Atlassian: auto-quarantine with ownership and deadlines
- GitHub: 9% flaky builds → 0.5% (18× improvement)
- Meta: probabilistic flakiness scoring

## Target Metrics

| Metric | Target |
|--------|--------|
| Flaky rate | Below 2% |
| Failure rate | Below 5% |

## `--fail-on-flaky-tests` (Playwright v1.45+)

Treats tests needing retries to pass as build failures. Prevents flaky tests from merging.
