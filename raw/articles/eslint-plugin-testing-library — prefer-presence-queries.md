# eslint-plugin-testing-library — prefer-presence-queries

**Source:** https://github.com/testing-library/eslint-plugin-testing-library/blob/main/docs/rules/prefer-presence-queries.md

## Rule

`testing-library/prefer-presence-queries`

## What It Enforces

Use the appropriate query type based on whether you're asserting presence or absence:

**Presence** → `getBy*`/`getAllBy*` (throws if not found)
**Absence** → `queryBy*`/`queryAllBy*` (returns null)

## Why Each Matters

Using `getBy*` for presence checks "offer[s] better info than asserting with other queries which will not throw an error."

Using `queryBy*` for absence prevents immediate test failures, allowing assertions to execute properly with `.toBeNull()` or `.toBeFalsy()`.

## Key Examples

```js
// Invalid
expect(screen.queryByText('button')).toBeInTheDocument();

// Valid
expect(screen.getByText('button')).toBeInTheDocument();

// Valid for absence
expect(screen.queryByText('button')).not.toBeInTheDocument();
```

## Notes

- Auto-fixable via `eslint --fix`
- Enabled in Angular, DOM, React, Vue, Svelte, and Marko configs
