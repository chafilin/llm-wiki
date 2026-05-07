---
title: "MDN — Security — IDOR"
type: source
raw: raw/articles/MDN — Security — IDOR.md
date_ingested: 2026-05-07
tags: [security, idor, access-control, web-attacks, authorization]
---

## Summary
Insecure Direct Object Reference (IDOR) is an access control vulnerability where a server exposes object identifiers (URL params, form fields, file paths) without verifying that the authenticated user is authorized to access the referenced object. An attacker who is legitimately authenticated can then access or modify other users' resources simply by changing the identifier.

## Key takeaways
- Authentication (proving who you are) and authorization (proving you can access this specific resource) are separate concerns — IDOR is a failure of authorization, not authentication.
- Common attack vectors: modifying IDs in URLs, tampering with hidden form fields in browser DevTools, and guessing sequentially numbered file paths.
- The fix is a server-side check on every request that verifies the authenticated user's identity matches the resource owner, not just that they are logged in.
- Using non-sequential, hard-to-guess IDs (UUIDs) reduces the likelihood of accidental discovery but is not a substitute for proper access control checks.
- Never expose PII (usernames, email addresses) as resource identifiers in URLs.

## Connections
[[Web Security]]

## Quotes
> "Authentication is not enough! [...] Always verify that the authenticated user is authorized to access or modify the object."
