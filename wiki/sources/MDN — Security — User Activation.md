---
title: MDN — Security — User Activation
type: source
raw: raw/articles/MDN — Security — User Activation.md
date_ingested: 2026-05-07
tags: []
---

## Summary
User activation is a browser security mechanism that gates sensitive APIs behind evidence of genuine user interaction, preventing malicious scripts from silently abusing powerful features. There are two tiers: transient activation (short-lived, expires after a timeout, consumed by some APIs) and sticky activation (set once per session and never reset). APIs like `window.open`, clipboard access, and pointer lock require transient activation; autoplay and `beforeunload` require sticky activation.

## Key takeaways
- Activation triggering events must have `isTrusted: true` — synthetic events don't count.
- Transient activation expires and can be consumed; it gates APIs that must be directly triggered by a user gesture (e.g., `Clipboard.write()`, `Window.open()`, `requestFullscreen()`).
- Sticky activation persists for the session; it gates features that should not trigger on page load (e.g., autoplay, `navigator.vibrate()`).
- `navigator.userActivation.isActive` checks transient state; `navigator.userActivation.hasBeenActive` checks sticky state.

## Connections
Links to wiki pages this source touches: [[Web Security]], [[Software Development]]

## Quotes
> "User activation is a security mechanism that restricts access to sensitive APIs to prevent malicious scripts from abusing features that could degrade user experience."
