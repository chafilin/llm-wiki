---
title: MDN — Security — Passkeys
type: source
raw: raw/articles/MDN — Security — Passkeys.md
date_ingested: 2026-05-07
tags: []
---

## Summary
Passkeys replace passwords with public-key cryptography: a private key lives on the user's authenticator device and never leaves it, while the server stores only the public key. Authentication works by the authenticator signing a server-issued challenge, with no shared secret ever transmitted. Passkeys are phishing-resistant by design because they are scoped to the exact origin that created them, and they support multi-factor authentication through user verification (biometric or PIN) built into the authenticator.

## Key takeaways
- A passkey is a per-site public/private key pair; the private key stays on the authenticator, the server stores only the public key.
- Sign-in is a challenge-response: server sends a nonce, authenticator signs it, server verifies with the public key.
- Phishing resistance: the browser enforces origin scope, so a passkey for `my-bank.example.com` won't work on `my-bank.examp1e.com`.
- Platform authenticators (Touch ID, Windows Hello) are device-bound; roaming authenticators (YubiKey) are portable.
- Passkeys must be discoverable (`residentKey: "required"`) to enable autofill UI.
- The WebAuthn API is `CredentialsContainer.create()` (registration) and `CredentialsContainer.get()` (sign-in).
- Migration path: offer passkeys alongside passwords, then optionally retire passwords once users have multiple passkeys.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Because the passkey is specific to the site's origin, if a passkey was created for the user's account at `my-bank.example.com`, the user will not be able to use it on `my-bank.examp1e.com`. This makes passkeys an effective defense against phishing."
