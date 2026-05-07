---
title: MDN — Security — CORS Configuration
type: source
raw: raw/articles/MDN — Security — CORS Configuration.md
date_ingested: 2026-05-07
tags: [cors, security-headers, cross-origin, access-control]
---

## Summary
MDN's practical guide to configuring Cross-Origin Resource Sharing via the `Access-Control-Allow-Origin` header and related headers. Same-origin policy blocks cross-origin script requests by default; CORS selectively relaxes this for CDNs, public APIs, and other legitimate cross-origin use cases. Misconfiguration can expose sites to CSRF and unauthorized data reads.

## Key takeaways
- Only API endpoints that require remote access should return CORS headers — not every page on the site.
- Specify the minimum set of allowed origins; reflecting the `Origin` header back verbatim is dangerous.
- For credentialed cross-origin access, set `Access-Control-Allow-Origin` to explicit origins only — never use `*` with credentials.
- For public non-credentialed access (e.g., JS library CDN), `*` is correct; omit `Access-Control-Allow-Credentials`.
- Using `Access-Control-Allow-Origin: *` is also required for Subresource Integrity to function.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Failure to set `Access-Control-Allow-Origin` appropriately will allow unauthorized origins to read the contents of any page on your site. This can be especially dangerous if those sites are able to send credentials, potentially exposing your site to CSRF attacks."
