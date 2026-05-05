# eslint-plugin-testing-library — prefer-screen-queries

**Source:** https://github.com/testing-library/eslint-plugin-testing-library/blob/main/docs/rules/prefer-screen-queries.md

## Rule

`testing-library/prefer-screen-queries`

## What It Enforces

Use `screen` for DOM queries rather than destructuring from `render()` return value.

## Why screen Is Preferred

"Works better with autocomplete and makes each test a little simpler to write and maintain." Single consistent interface for all queries.

## Invalid Patterns

```js
const { getByText } = render(<Component />);
getByText('foo');

const utils = render(<Component />);
utils.getByText('foo');

render(<Component />).getByText('foo');
```

## Valid Patterns

```js
render(<Component />);
screen.getByText('foo');

within(screen.getByTestId('section')).getByText('foo');

const utils = render(<Foo />);
utils.rerender(<Foo />); // utility methods (not queries) are fine
```

## Exceptions

1. Queries chained to `within()`
2. Custom queries not available on `screen`
3. Tests using `container` or `baseElement` render options
