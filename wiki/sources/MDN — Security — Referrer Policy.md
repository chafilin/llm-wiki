---
title: MDN — Security — Referrer Policy
type: source
raw: raw/articles/MDN — Security — Referrer Policy.md
date_ingested: 2026-05-07
tags: [referrer-policy, security-headers, privacy, information-disclosure]
---

## Summary
MDN's practical guide to controlling the `Referer` header via the `Referrer-Policy` response header. The `Referer` header leaks the URL of the originating page when navigating or loading resources, potentially exposing internal URLs, sensitive query parameters, or user tracking data to third parties.

## Key takeaways
- Four recommended directives from strictest to least strict: `no-referrer`, `same-origin`, `strict-origin`, `strict-origin-when-cross-origin` (the browser default).
- `strict-origin-when-cross-origin` is a safe default — full URL on same-origin, origin-only on cross-origin requests.
- Can be applied at multiple levels: HTTP header (site-wide), `<meta>` tag (page-wide), HTML element attribute (per-link), or Fetch API option (per-request).
- For browser compatibility, send multiple values as a fallback list: `no-referrer, strict-origin-when-cross-origin`.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Although this can be useful, it poses a risk to user privacy — it may expose internal URLs or sensitive URL parameters."
