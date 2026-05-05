# Effective Snapshot Testing

**Source:** https://kentcdodds.com/blog/effective-snapshot-testing
**Author:** Kent C. Dodds
**Date:** October 30, 2017

## Main Argument

Snapshot testing is valid but only when used deliberately. Dodds acknowledges legitimate criticisms while arguing snapshots provide real value in specific contexts.

## When Snapshots Work Well

**Error messages and logs** — Testing developer-facing tool outputs without fragile regex patterns.

**Babel plugin testing** — "I honestly don't know how I'd test babel plugins with anything but Jest snapshot testing." Serialized AST comparisons would be prohibitively complex otherwise.

**CSS-in-JS validation** — Snapshots including applied styles catch styling regressions that E2E tests miss.

## When Snapshots Fail

Four critical problems:
1. Tests lack clarity about developer intent — failures are hard to diagnose
2. Generated files encourage insufficient scrutiny before commits
3. High false-negative rates erode team trust
4. Teams regenerate snapshots rather than investigating failures

Massive snapshots (>640 lines) amplify all of the above.

## Recommendations

**Avoid huge snapshots** — Keep them focused and reviewable (dozens of lines, not hundreds).

**Custom serializers** — Normalize paths, exclude noise, highlight meaningful differences.

**Snapshot-diff** — Capture only differences between states rather than complete before/after representations.
