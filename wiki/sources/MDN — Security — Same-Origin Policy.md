---
title: MDN — Security — Same-Origin Policy
type: source
raw: raw/articles/MDN — Security — Same-Origin Policy.md
date_ingested: 2026-05-07
tags: []
---

## Summary
The same-origin policy is a browser security mechanism that restricts how documents or scripts from one origin can interact with resources from another origin, defined by matching scheme, host, and port. Cross-origin writes and embeds are generally allowed, while cross-origin reads are blocked. CORS is the standard mechanism for explicitly permitting cross-origin access, and browser storage (Web Storage, IndexedDB) is strictly isolated per origin.

## Key takeaways
- An "origin" is the tuple of scheme + host + port; all three must match for two URLs to be same-origin.
- Cross-origin writes (form submissions, redirects, links) are allowed by default; cross-origin reads are not.
- Cross-origin embeds (scripts, images, media, iframes) are allowed, which can inadvertently leak read access.
- CORS lets servers opt in to cross-origin reads via HTTP headers.
- CSRF tokens block unauthorized cross-origin writes.
- `window.postMessage` is the safe API for cross-document communication across origins.
- Each origin gets isolated Web Storage and IndexedDB; cookies follow different (looser) rules.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "The same-origin policy is a critical security mechanism that restricts how a document or script loaded by one origin can interact with a resource from another origin."
