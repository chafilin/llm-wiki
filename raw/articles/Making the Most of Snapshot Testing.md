# Making the Most of Snapshot Testing

**Source:** https://samhogy.co.uk/2022/03/making-the-most-of-snapshot-testing/
**Author:** Sam Hogarth
**Date:** March 4, 2022

## Core Recommendations

### Don't snapshot everything
Avoid capturing entire component trees or massive JSON structures. Large snapshots "become undiffable when there's a change." Tests should provide "unambiguous, actionable signal[s]." Capture only what's relevant to the specific test.

### Use inline snapshots for small cases
`.toMatchInlineSnapshot()` keeps the expected value in the test file, improving readability. Let Jest auto-generate it or provide it upfront.

### Give snapshots readable names
Use meaningful test names in `describe` blocks. Pass hint strings: `.toMatchSnapshot(hintString)`. "Tests can be examples on how to use the code."

### Ensure deterministic output
Mock `Date.now()` and `Math.random()` with static values. Or use Jest's Property Matcher syntax for fuzzy matching — validates type without hardcoding exact values.

### Add custom serializers
Configure via `expect` global with `test` and `print` functions. Enables clean diffs that distinguish intended from unintended changes.

### Capture only differences
For before/after component state testing, use the `snapshot-diff` utility — displays only what changed, reducing noise.

## Key Insight

Snapshot testing extends beyond React components to API contract testing and any serializable data. Effectiveness requires restraint and strategic application.
