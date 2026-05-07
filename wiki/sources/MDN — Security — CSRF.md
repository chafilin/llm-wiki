---
title: "MDN — Security — CSRF"
type: source
raw: raw/articles/MDN — Security — CSRF.md
date_ingested: 2026-05-07
tags: [security, csrf, web-attacks, cookies, authentication]
---

## Summary
Cross-site request forgery (CSRF) tricks a user's browser into sending an authenticated HTTP request to a target site from a malicious site, causing unintended state changes (e.g., fund transfers). The attack works when a site relies solely on cookies for authentication and uses only predictable request parameters. Defenses range from CSRF tokens to using non-simple fetch requests.

## Key takeaways
- CSRF is possible only when: the site uses cookies for auth, makes state changes via HTTP, and the request parameters are attacker-predictable.
- CSRF tokens embed an unpredictable server-generated value in forms; the server rejects requests that don't include it. Most frameworks (e.g., Django) support this out of the box.
- The `Sec-Fetch-Site` fetch metadata header lets servers distinguish same-origin from cross-site requests and reject the latter for state-changing endpoints.
- Using `fetch()` or `XMLHttpRequest` with a `Content-Type: application/json` or custom header makes the request non-simple, bypassing the same-origin form-submission loophole.
- `SameSite=Strict` cookies are a defense-in-depth measure, not a standalone fix; `Lax` is a practical middle ground for auth cookies.
- `SameSite` protects against cross-site but not cross-origin requests — subdomains are considered the same site.

## Connections
[[Web Security]]

## Quotes
> "A CSRF attack is possible if your website: uses HTTP requests to change some state on the server; uses only cookies to validate that the request came from an authenticated user; uses only parameters in the request that an attacker can predict."
