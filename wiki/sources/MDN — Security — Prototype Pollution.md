---
title: "MDN — Security — Prototype Pollution"
type: source
raw: raw/articles/MDN — Security — Prototype Pollution.md
date_ingested: 2026-05-07
tags: [security, prototype-pollution, javascript, web-attacks, nodejs]
---

## Summary
Prototype pollution is a JavaScript-specific vulnerability where an attacker injects properties onto `Object.prototype` (or another prototype in the chain), causing those properties to appear on all objects in the application. The key attack vector is the `__proto__` property or `constructor.prototype` in unsanitized user-controlled key-value assignments. Consequences range from logic errors to full XSS.

## Key takeaways
- The dangerous pattern is `obj[userKey1][userKey2] = value` — if `userKey1` is `"__proto__"`, the assignment targets `Object.prototype`, affecting every plain object in the process.
- Pollution has two phases: injection (usually via URL params, JSON, or merge operations) and exploitation (when application code reads a property it assumes is absent or has a safe default).
- Schema validators (ajv, Zod) with `additionalProperties: false` and explicit rejection of `__proto__`, `constructor`, `prototype` as keys are the primary defense.
- `Object.freeze(Object.prototype)` or Node's `--disable-proto` flag harden the runtime against injection attempts.
- Prefer `Map` and `Set` over plain objects for dynamic key-value storage; use `Object.hasOwn()` instead of property existence checks; prefer `for...of`/`Object.keys()` over `for...in`.
- Null-prototype objects (`Object.create(null)`) are immune to prototype pollution.

## Connections
[[Web Security]], [[Software Development]]

## Quotes
> "If key1 is '__proto__', this modifies Object.prototype."
