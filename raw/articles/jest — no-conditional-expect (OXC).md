# jest/no-conditional-expect — OXC Linter

**Source:** https://oxc.rs/docs/guide/usage/linter/rules/jest/no-conditional-expect

## Rule

`jest/no-conditional-expect`

## What It Prevents

`expect` assertions inside conditional code blocks:
- Conditional statements (`if`, `else`)
- Logical operators (`&&`, `||`)
- `catch` blocks
- Promise `.catch()` callbacks

## Why It Matters

"Jest only considers a test to have failed if it throws an error." Assertions in conditional code may never execute, causing tests to silently pass without verifying anything.

## Invalid Examples

```js
doTest && expect(1).toBe(2);

if (!skipTest) {
  expect(1).toEqual(2);
}

try {
  await foo();
} catch (err) {
  expect(err).toMatchObject({ code: 'MODULE_NOT_FOUND' });
}
```

## Valid Examples

```js
expect(!value).toBe(false);
expect(getValue()).toBe(2);
// finally blocks are OK
expect(validRequest).toHaveBeenCalledWith(request);
```
