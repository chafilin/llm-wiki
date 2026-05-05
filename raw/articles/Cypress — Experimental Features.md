# Cypress — Experimental Features

**Source:** https://docs.cypress.io/app/references/experiments

## Overview

Experimental features that can be enabled to test upcoming functionality. May change or be removed without making it into the core product.

## Available Configuration Options

| Feature | Default | Purpose |
|---------|---------|---------|
| `experimentalCspAllowList` | false | Controls Content-Security-Policy directives during testing |
| `experimentalFetchPolyfill` | false | Replaces `window.fetch` with a spyable polyfill (deprecated) |
| `experimentalInteractiveRunEvents` | false | Enables run event listeners in interactive mode |
| `experimentalMemoryManagement` | false | Improves memory handling in Chromium browsers |
| `experimentalModifyObstructiveThirdPartyCode` | false | Searches and replaces problematic third-party code |
| `experimentalRunAllSpecs` | false | Enables sequential multi-spec execution |
| `experimentalSourceRewriting` | false | Enables AST-based code rewriting |
| `experimentalWebKitSupport` | false | Adds WebKit browser support |
| `experimentalFastVisibility` | false | Uses point sampling for faster visibility detection |

## Flake Detection Strategies

Two retry strategies available:
- `detect-flake-and-pass-on-threshold` — pass if enough retries succeed
- `detect-flake-but-always-fail` — mark as flaky but still fail the build

## Testing Type-Specific Options

- **E2E:** `experimentalOriginDependencies` enables `Cypress.require` within `cy.origin`
- **Component:** `experimentalSingleTabRunMode` runs all specs in a single tab for improved performance

## Fast Visibility Algorithm

"Can significantly improve performance when interacting with complex DOM structures" through constant-time performance in optimal cases.
