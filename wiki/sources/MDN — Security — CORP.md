---
title: MDN — Security — CORP
type: source
raw: raw/articles/MDN — Security — CORP.md
date_ingested: 2026-05-07
tags: [corp, cross-origin, security-headers, spectre, xs-leaks, side-channel]
---

## Summary
MDN's practical guide to Cross-Origin Resource Policy (CORP) via the `Cross-Origin-Resource-Policy` response header. CORP protects against side-channel hardware attacks like Spectre and Meltdown that exploit speculative execution to read cross-origin resource bodies — it strips the response body rather than blocking the request itself.

## Key takeaways
- CORP defends against XS-Leaks (cross-site leaks) caused by speculative execution vulnerabilities like Spectre/Meltdown.
- Three values: `same-origin` (most restrictive, for private APIs and sensitive data), `same-site` (for shared same-site CDN/SSO), `cross-origin` (public CDNs/widgets — the insecure default when header is absent).
- The header strips the response body on policy violation rather than preventing the request — this is a browser-level enforcement.
- Pairing `Cross-Origin-Resource-Policy: same-origin` with `Cross-Origin-Embedder-Policy: require-corp` enables access to high-resolution timers and `SharedArrayBuffer`.
- Best practice: always set the most restrictive value your use case allows.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Some side-channel hardware vulnerabilities (also known as Cross-site leaks, or XS-Leaks), such as Meltdown and Spectre, exploit a race condition arising as part of speculative execution functionality of modern processors."
