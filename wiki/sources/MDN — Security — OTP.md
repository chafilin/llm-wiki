---
title: MDN — Security — OTP
type: source
raw: raw/articles/MDN — Security — OTP.md
date_ingested: 2026-05-07
tags: []
---

## Summary
One-time passwords (OTPs) are single-use codes that authenticate based on something the user has rather than something they know. The article covers three delivery mechanisms — email, SMS, and TOTP (time-based, via authenticator app) — with their relative security trade-offs. TOTP is the strongest OTP option but still vulnerable to phishing; for general authentication, passkeys are the recommended alternative.

## Key takeaways
- OTPs avoid the guessing and credential stuffing vulnerabilities of passwords because users don't choose or remember them.
- Email OTP codes are more flexible and slightly more secure than one-time links; links require same device/browser.
- SMS OTP is weak: SS7 protocol flaws, SIM swapping, and carrier recycling of numbers make it easily attacked — use only as a second factor, never as the sole authentication method.
- TOTP (RFC 6238) generates 6-digit codes valid for ~30 seconds using a shared secret and the current time; codes should expire in ≤5 minutes.
- All OTP forms are vulnerable to real-time phishing (attacker relays the code live).
- Browser supports SMS autofill via `autocomplete="one-time-code"` when the SMS is formatted with the `@domain #code` suffix.
- Prefer TOTP over SMS/email OTP; prefer passkeys over all OTP forms for general authentication.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Do not use SMS OTP on its own to establish new sessions or for general authentication. Only use it as a second factor."
