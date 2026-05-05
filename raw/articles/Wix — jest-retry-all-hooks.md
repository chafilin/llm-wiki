# jest-retry-all-hooks

**Source:** https://github.com/wix-incubator/jest-retry-all-hooks

## Overview

Patches Jest's `beforeAll` and `afterAll` hooks to work properly with `jest.retryTimes`. Normally these hooks don't retry when tests fail. This package converts them into intelligent `beforeEach`/`afterEach` hooks that run once by default but re-execute when tests fail.

## Key Functionality

- **beforeAll** → `beforeEach` that runs on first execution and again if the previous test failed
- **afterAll** → `afterEach` that runs after each test, especially when failures occur
- Tests and their immediate `beforeEach`/`afterEach` hooks continue retrying normally

## Installation

```bash
npm install --save-dev jest-retry-all-hooks
```

```js
// jest.config.js
testEnvironment: 'jest-environment-emit/node',
testEnvironmentOptions: {
  eventListeners: ['jest-retry-all-hooks'],
},
```

Also install: `npm install --save-dev jest-environment-emit`

## Compatible Environments

Works with test environments supporting `jest-environment-emit`, including: jest-metadata, jest-allure2-reporter, and Detox.

## License

MIT
