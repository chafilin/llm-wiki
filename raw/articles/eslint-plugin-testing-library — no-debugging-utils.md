# eslint-plugin-testing-library — no-debugging-utils

**Source:** https://raw.githubusercontent.com/testing-library/eslint-plugin-testing-library/HEAD/docs/rules/no-debugging-utils.md

## Rule

`testing-library/no-debugging-utils`

## What It Bans

Debugging utilities that should not be committed to source:

- `debug`
- `logTestingPlaygroundURL`
- `prettyDOM`
- `logRoles`
- `logDOM`
- `prettyFormat`

## Why

"debug statements also pollutes the tests if one of your teammates forgot to remove it." Same principle as removing `console.log` from production code.

## Violation Examples

```js
const { debug } = render(<Hello />);
debug();

const utils = render(<Hello />);
utils.debug();

import { screen } from '@testing-library/dom';
screen.debug();

const { screen } = require('@testing-library/react');
screen.debug();
```

## Configuration

The `utilsToCheckFor` option allows selectively enabling or disabling specific utilities.

Default severity: `warn` in Angular, Marko, React, Svelte, and Vue configurations.
