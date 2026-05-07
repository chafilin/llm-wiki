---
title: MDN — Security — Cookie Configuration
type: source
raw: raw/articles/MDN — Security — Cookie Configuration.md
date_ingested: 2026-05-07
tags: [cookies, security-headers, csrf, xss, session-management]
---

## Summary
MDN's practical guide to securing cookies via `Set-Cookie` attributes. Cookies carrying session identifiers or sensitive data are high-value targets; misconfigured cookies enable session theft, CSRF, and clickjacking. The guide covers every relevant attribute and provides concrete examples for common scenarios.

## Key takeaways
- Always set `Secure` (HTTPS only) and `HttpOnly` (blocks JS access via `document.cookie`) on session cookies.
- Use `__Host-` prefix for single-domain cookies (forces `Path=/`, no `Domain` attribute) and `__Secure-` for all others — prevents overwriting by insecure sources.
- Prefer `Max-Age` over `Expires` for relative expiration; session identifiers should expire quickly.
- Set `SameSite=Strict` or `SameSite=Lax` to defend against CSRF and cross-site leak attacks.
- Set `Domain` only when cookies genuinely need to be shared across subdomains, using the most restrictive domain possible.
- Set `Path` to the most restrictive value applicable.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Set the `HttpOnly` attribute on all cookies that don't require access from JavaScript. This is especially important for session identifier cookies to help prevent XSS attacks from stealing session identifiers."
