---
title: MDN — Security — Passwords
type: source
raw: raw/articles/MDN — Security — Passwords.md
date_ingested: 2026-05-07
tags: []
---

## Summary
This MDN article covers password-based authentication end to end: secure form design, server-side storage with hashing and salting, login logic that avoids username enumeration, and a safe password reset flow. Passwords remain the most common authentication method but have inherent weaknesses — credential stuffing, phishing, and guessing — that no implementation detail fully solves, making OTP or passkeys as a second or replacement factor strongly advisable.

## Key takeaways
- Never store plaintext passwords; use Argon2id (preferred), scrypt, bcrypt, or PBKDF2.
- Salt (per-password random value) prevents rainbow table attacks; pepper (server-side secret) adds a layer against database dumps.
- Return identical error messages for "wrong username" and "wrong password" to prevent username enumeration.
- Password reset links/tokens must be short-lived; the response to a reset request should not reveal whether the email is registered.
- Use correct `autocomplete` attributes (`new-password` for registration, `current-password` for login) to enable password managers.
- Credential stuffing and phishing cannot be solved by server-side password handling alone — supplement with MFA or passkeys.

## Connections
Links to wiki pages this source touches: [[Web Security]]

## Quotes
> "Never store plaintext passwords."

> "Return the same error message whether username doesn't exist OR password is wrong. This prevents attackers from enumerating valid usernames."
