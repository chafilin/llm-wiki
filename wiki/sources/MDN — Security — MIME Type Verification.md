---
title: MDN — Security — MIME Type Verification
type: source
raw: raw/articles/MDN — Security — MIME Type Verification.md
date_ingested: 2026-05-07
tags: [mime-sniffing, security-headers, xss, x-content-type-options]
---

## Summary
MDN's short practical guide on preventing MIME type sniffing attacks using the `X-Content-Type-Options: nosniff` response header. Without this header, browsers may misidentify non-script or non-stylesheet files as scripts or stylesheets, enabling XSS vectors through `<script>` and `<link>` elements.

## Key takeaways
- Set `X-Content-Type-Options: nosniff` on all responses — it is a single-value header with no configuration complexity.
- `nosniff` blocks requests where the destination type is `script` but the MIME type isn't a valid JavaScript type, or where the destination is `style` but the MIME type isn't `text/css`.
- Must be paired with correctly set `Content-Type` headers on served files to be effective.
- This is one of the simplest and highest-value security headers to deploy — zero cost, meaningful XSS mitigation.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Without proper MIME type verification, browsers might incorrectly detect non-script and non-stylesheet files as scripts or stylesheets. This error allows potentially malicious files to be loaded via `<script>` and `<link>` elements as part of XSS attacks."
