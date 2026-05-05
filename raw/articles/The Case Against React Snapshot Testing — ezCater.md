# The Case Against React Snapshot Testing — ezCater

**Source:** https://engineering.ezcater.com/the-case-against-react-snapshot-testing
**Author:** Ben Jackson

## Result

After 6 months of use, ezCater replaced nearly all snapshot tests with focused unit tests. Conclusion: "snapshots are more trouble than they're worth, especially across large and/or fluid teams."

## Problems Identified

1. **Unclear assertions** — Snapshot tests render entire components. Diffs show many changes; unclear what actually failed.
2. **Developer negligence** — When diffs become hard to interpret, developers approve changes without proper review.
3. **Maintenance burden** — Tests fail for unrelated reasons, requiring constant updates.

## Recommended Alternatives

| Pattern | Instead of snapshot, use |
|---------|--------------------------|
| "It renders" tests | Remove them — linting and build checks suffice |
| Text assertions | Target specific conditionally rendered content with precise selectors |
| Conditional markup | Assert presence of specific components |
| CSS testing | `jest-emotion` or visual regression tools |

## Key Principle

"A more focused and explicit unit test is a much better choice." Tests become documentation — guiding developers to the exact problem location when they fail.
