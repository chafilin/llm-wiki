---
title: "MDN — Security — XSS"
type: source
raw: raw/articles/MDN — Security — XSS.md
date_ingested: 2026-05-07
tags: [security, xss, web-attacks, csp, javascript]
---

## Summary
Cross-site scripting (XSS) is an attack where an attacker gets a target site to execute malicious code as though it were part of that site, subverting the same-origin policy. It requires two conditions: the site accepts attacker-crafted input, and it includes that input in a page without sanitizing it. Attacks can be client-side (via `innerHTML` and similar APIs) or server-side (via unsafe templating), and stored XSS is the most severe variant.

## Key takeaways
- XSS bypasses the same-origin policy by injecting code into the target site's own context, giving it access to cookies, local storage, and the ability to impersonate the user.
- The encoding strategy depends on context: HTML context, HTML attribute context, and JavaScript/CSS context each require different treatment — attribute values must always be quoted.
- Output encoding (auto-handled by Django templates, React JSX) is the first line of defense; DOMPurify sanitization covers cases where HTML must be accepted as input.
- The Trusted Types API enforces that unsafe DOM sinks (`innerHTML`, `eval`, etc.) only receive sanitized values, caught at the browser level.
- A strict Content Security Policy (nonce- or hash-based) is the final safety net — it blocks inline handlers and `eval` even if injection succeeds.

## Connections
[[Web Security]], [[Software Development]]

## Quotes
> "All XSS attacks depend on a website doing two things: (1) Accepting input that could have been crafted by an attacker. (2) Including this input in a page without sanitizing it."
