---
title: "MDN — Security — Phishing"
type: source
raw: raw/articles/MDN — Security — Phishing.md
date_ingested: 2026-05-07
tags: [security, phishing, social-engineering, authentication, passkeys]
---

## Summary
Phishing is a social engineering attack where an attacker registers a lookalike domain, clones the target site, and lures the user (typically via email) into entering credentials on the fake site. Spear-phishing targets specific individuals with personalized lures. Even technically sophisticated users remain vulnerable.

## Key takeaways
- The attack exploits users' inability to reliably distinguish legitimate from lookalike domains (e.g., `examp1e.com` vs `example.com`); experience alone does not protect users.
- SPF, DKIM, and DMARC DNS records help email servers detect and block forged phishing emails before they reach users.
- Password managers provide incidental phishing protection by refusing to autofill credentials on domains that don't match the stored origin.
- SMS OTP and TOTP-based MFA are vulnerable to real-time phishing attacks (attacker proxies the code in real time); they raise the bar but don't fully prevent credential theft.
- Passkeys (WebAuthn) are the strongest technical defense: they are bound to the exact origin they were created for and the browser will not authenticate the user on a lookalike domain.

## Connections
[[Web Security]]

## Quotes
> "Phishing attacks are not dependent on naive or inexperienced users: decades of experience has shown that even highly experienced and knowledgeable users can be vulnerable."

> "If a passkey was created for the user's account at my-bank.example.com, the user will not be able to use it on my-bank.examp1e.com."
