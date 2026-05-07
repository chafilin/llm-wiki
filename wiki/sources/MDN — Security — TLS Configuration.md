---
title: MDN — Security — TLS Configuration
type: source
raw: raw/articles/MDN — Security — TLS Configuration.md
date_ingested: 2026-05-07
tags: [tls, https, hsts, security-headers, mitm]
---

## Summary
MDN's practical guide to deploying TLS correctly, covering secure server configuration, eliminating mixed content, HTTP-to-HTTPS redirection, and HTTP Strict Transport Security (HSTS). TLS provides confidentiality, authenticity, and integrity for all communications; HSTS ensures browsers never fall back to plain HTTP.

## Key takeaways
- Use Mozilla's SSL Configuration Generator to get safe TLS settings for your server software.
- All active resources (JS, CSS) must be loaded over HTTPS — browsers block mixed content and show warnings.
- Redirect all port 80 traffic to HTTPS with a 301 permanent redirect (examples given for NGINX and Apache).
- Set `Strict-Transport-Security` with `max-age` of at least 6 months; 2 years (`63072000`) is recommended.
- Add `includeSubDomains` to cover all subdomains; add `preload` to be included in browser HSTS preload lists via hstspreload.org.
- Pair HSTS with CSP's `upgrade-insecure-requests` directive for defense-in-depth.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Transport Layer Security (TLS) provides assurances about the confidentiality, authenticity, and integrity of all communications, and should be used for all inbound and outbound website communications."
