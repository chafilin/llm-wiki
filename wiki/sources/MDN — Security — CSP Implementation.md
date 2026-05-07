---
title: MDN — Security — CSP Implementation
type: source
raw: raw/articles/MDN — Security — CSP Implementation.md
date_ingested: 2026-05-07
tags: [csp, xss, security-headers, content-security-policy]
---

## Summary
MDN's practical guide to implementing Content Security Policy via the `Content-Security-Policy` HTTP header. CSP's primary purpose is mitigating XSS attacks by controlling which resources can be loaded and executed, with secondary benefits against clickjacking and MITM attacks. Strict nonce- or hash-based CSPs are strongly preferred over allowlist-based policies.

## Key takeaways
- Strict CSP (nonce or hash-based) is superior to allowlist CSP — allowlists grow unwieldy and tend to include unsafe domains.
- A strict CSP disables inline JS, inline event handlers, `eval()`, object embeds, and `<base>` element usage.
- Use `strict-dynamic` to allow scripts loaded by trusted first-party scripts without needing individual nonces/hashes.
- Avoid `unsafe-inline`, `data:` URIs in `script-src`/`object-src`, and overly broad sources — they defeat the policy.
- Test with `Content-Security-Policy-Report-Only` before enforcing; use `report-to` (and `report-uri` for older browsers) to collect violations.
- If an HTTP header is unavailable, a `<meta http-equiv="Content-Security-Policy">` tag works as a fallback.

## Connections
Links to wiki pages this source touches: [[Web Security]], [[Software Development]]

## Quotes
> "Implementing a strict CSP is the best way to mitigate XSS vulnerabilities. This uses nonce- or hash-based fetch directives to ensure only scripts/styles with the correct nonce or hash execute."
