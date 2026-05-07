---
title: MDN — Security — Secure Contexts
type: source
raw: raw/articles/MDN — Security — Secure Contexts.md
date_ingested: 2026-05-07
tags: []
---

## Summary
A secure context is a browsing environment (Window or Worker) that meets minimum authentication and confidentiality standards, which gates access to powerful web APIs. For a document to be considered in a secure context, it and all its ancestors must be delivered over HTTPS; a TLS-delivered iframe inside a non-TLS parent is not secure. Localhost and `file://` URLs are treated as potentially trustworthy despite lacking HTTPS.

## Key takeaways
- Many powerful APIs (service workers, clipboard, geolocation, etc.) are restricted to secure contexts to limit damage from MITM attackers.
- Secure context requires HTTPS all the way up the ancestor chain — one non-HTTPS ancestor breaks it.
- `http://127.0.0.1`, `http://localhost`, `http://*.localhost`, and `file://` are considered potentially trustworthy even without TLS.
- `wss://` (Secure WebSocket) URLs are also considered potentially trustworthy.
- Pages can check their status with `window.isSecureContext`.

## Connections
Links to wiki pages this source touches: [[Web Security]], [[Software Development]]

## Quotes
> "Even for a document delivered over TLS within an `<iframe>`, its context is not considered secure if it has an ancestor that was not also delivered over TLS."
