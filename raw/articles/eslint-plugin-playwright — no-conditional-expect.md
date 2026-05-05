# eslint-plugin-playwright — no-conditional-expect

**Source:** https://github.com/playwright-community/eslint-plugin-playwright/blob/main/docs/rules/no-conditional-expect.md

## Rule

`playwright/no-conditional-expect`

## What It Prevents

`expect` assertions inside conditional blocks:
- Logical operators: `doTest && expect(1).toBe(2)`
- `if` statements: `if (!skipTest) { expect(1).toEqual(2) }`
- `try-catch`: `catch (err) { expect(err).toMatchObject({...}) }`
- Promise `.catch()`: `.catch((error) => expect(error).toBeInstanceOf(Error))`

## Rationale

Playwright tests only fail when errors are thrown. Conditional assertions can silently be skipped, causing tests to pass without verifying anything.

## Valid Patterns

```js
expect(!value).toBe(false);
// finally blocks OK
finally { expect(validRequest).toHaveBeenCalledWith(request) }
// Playwright's built-in error matchers
await expect(foo).rejects.toThrow(Error)
```

## Recommended Alternative for Error Testing

Use a wrapper function that guarantees error capture, ensuring assertions always execute regardless of whether an error occurs.
