---
title: "MDN — Security — Clickjacking"
type: source
raw: raw/articles/MDN — Security — Clickjacking.md
date_ingested: 2026-05-07
tags: [security, clickjacking, web-attacks, csp, iframes]
---

## Summary
Clickjacking embeds a target site in a transparent `<iframe>` overlaid on a decoy page, so users unknowingly click sensitive target-site controls (buttons, links) while thinking they're interacting with the decoy. The attack succeeds when the target site can be framed and the user has an active session, since requests from the iframe carry the user's cookies.

## Key takeaways
- The attack requires three ingredients: the target site is embeddable, the attacker can position a decoy element precisely over the target UI, and the user has a live authenticated session.
- Primary defense is the `Content-Security-Policy: frame-ancestors 'self'` directive, which prevents the page from being loaded inside iframes on other origins.
- `X-Frame-Options: DENY` or `SAMEORIGIN` serves as a fallback for older browsers that don't support the CSP `frame-ancestors` directive.
- `SameSite=Lax` or `Strict` cookies are a complementary layer: they prevent cookies from being sent in iframe requests from cross-site pages, neutralizing attacks even if the page gets framed.

## Connections
[[Web Security]]

## Quotes
> "When users click what they think are harmless decoy elements, they're actually clicking on hidden elements from the target site."
