---
title: MDN — Security — Mixed Content
type: source
raw: raw/articles/MDN — Security — Mixed Content.md
date_ingested: 2026-05-07
tags: []
---

## Summary
Mixed content occurs when an HTTPS page loads resources over insecure HTTP, creating vulnerabilities to eavesdropping and man-in-the-middle modification. Browsers split mixed content into two categories: upgradable content (images, audio, video), which browsers automatically upgrade to HTTPS, and blockable content (scripts, stylesheets, iframes, fetch requests), which is outright blocked. The primary fix is serving all resources over HTTPS; the CSP `upgrade-insecure-requests` directive provides a blanket fallback.

## Key takeaways
- Mixed content undermines HTTPS security by exposing resources to interception and modification.
- Scripts are the most dangerous form of mixed content — they can rewrite the entire page.
- Browsers auto-upgrade simple `<img>`, `<audio>`, `<video>` HTTP requests to HTTPS (but block IP addresses).
- Scripts, stylesheets, iframes, fetch/XHR, and `<img srcset>` are blocked if loaded over HTTP.
- `Content-Security-Policy: upgrade-insecure-requests` upgrades all insecure requests including blockable ones.
- IP-address resources are blocked even in the upgradable category.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Scripts are particularly dangerous as they can modify any aspect of the page."
