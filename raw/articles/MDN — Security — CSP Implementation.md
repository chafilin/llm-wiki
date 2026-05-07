# Content Security Policy (CSP) Implementation

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Practical_implementation_guides/CSP

## Overview

The `Content-Security-Policy` HTTP header provides fine-grained control over the code that can be loaded on a site and what it is allowed to do.

## Problem

The main problem CSP addresses is **cross-site scripting (XSS) attacks**, generally caused by a lack of control and awareness over resource sources.

CSP also helps prevent:
- **Clickjacking**: Using the `frame-ancestors` directive to prevent embedding in `<iframe>` elements
- **Man-in-the-Middle (MiTM) attacks**: Using `upgrade-insecure-requests` directive to upgrade HTTP to HTTPS

## Solution

Implementing a **strict CSP** is the best way to mitigate XSS vulnerabilities. This uses nonce- or hash-based fetch directives to ensure only scripts/styles with the correct nonce or hash execute.

### Strict CSP Benefits

- Disables unsafe inline JavaScript and inline event handler attributes (e.g., `onclick`)
- Disables risky API calls like `eval()`
- Disables object embeds via `object-src 'none'`
- Disables `<base>` element usage via `base-uri 'none'`

Strict CSPs are preferred over location-based (allowlist) policies, which often permit unsafe domains and become large and unwieldy.

## Implementation Steps

1. **Choose nonces or hashes**: Use nonces for dynamically generated content; hashes for static content

2. **Implement strict CSP**: Ensure external and internal scripts have correct nonce attributes or hash integrity attributes

3. **Handle third-party scripts**: Use the `strict-dynamic` directive to allow scripts loaded by first-party scripts to run without explicit nonces/hashes

4. **Refactor disallowed patterns**: Replace inline event handlers with `addEventListener()` calls and remove `eval()` usage

5. **Disable embeds**: Use `object-src 'none'` unless embed functionality is needed

6. **Handle eval() if necessary**: Add `unsafe-eval` keyword if `eval()` cannot be removed (weakens CSP)

7. **Handle event handlers if necessary**: Add `unsafe-hashes` keyword if event handler attributes cannot be removed (safer than `unsafe-inline`)

### Fallback Option

If strict CSP cannot be implemented, an allowlist-based CSP like `default-src https:` still provides protection by disabling unsafe inline/`eval()` and only allowing HTTPS resources.

⚠️ **Warning:** Avoid including unsafe sources:
- `unsafe-inline`
- `data:` URIs in `script-src`, `object-src`, or `default-src`
- Overly broad sources

### Meta Tag Alternative

If the `Content-Security-Policy` header cannot be used, include a meta tag as the first `<meta>` element in the document `<head>`:

```html
<meta http-equiv="Content-Security-Policy" content="…">
```

## Report-Only CSPs

Before implementing actual CSP, test using the `Content-Security-Policy-Report-Only` header to see potential violations without enforcing them.

Use reporting directives:
- **`report-to`**: Posts JSON reports to endpoints (preferred, requires `Reporting-Endpoints` header)
- **`report-uri`**: Deprecated alternative (use both for cross-browser support)

## See Also

- [CSP Evaluator](https://csp-evaluator.withgoogle.com/)
- [Cross-site scripting (XSS)](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS)
