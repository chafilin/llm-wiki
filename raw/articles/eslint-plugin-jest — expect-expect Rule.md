# eslint-plugin-jest — expect-expect Rule

**Source:** https://github.com/jest-community/eslint-plugin-jest/blob/main/docs/rules/expect-expect.md

## Rule

`jest/expect-expect`

## What It Enforces

Triggers when a test contains no call to `expect`, preventing tests that appear to pass while validating nothing.

## Configuration

### `assertFunctionNames`

Custom assertion function names to recognize. Supports wildcards.

```json
"assertFunctionNames": ["expect", "request.**.expect"]
```

Default: `["expect"]`

### `additionalTestBlockFunctions`

Custom test block names beyond standard Jest functions (e.g., `theoretically` for jest-theories).

```json
"additionalTestBlockFunctions": ["theoretically"]
```

## Invalid Examples

```js
test('should assert something', () => {});
it('should be a test', () => { console.log('no assertion'); });
```

## Valid Examples

```js
it('should be a test', () => { expect(true).toBeDefined(); });
it('async', () => { somePromise().then(res => expect(res).toBe('passed')); });
```
