# Manipulator in the Middle (MITM)

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/MITM

## Overview

In a **Manipulator in the Middle (MITM) attack**, the attacker inserts themselves between two entities that are trying to communicate with each other.

On the web, an MITM attack generally takes place between the user's browser and the server, and enables the attacker to see and potentially modify any of the traffic exchanged over HTTP.

## Common Attack Scenario

A common way for an attacker to execute an MITM attack is to:

1. Set up a wireless access point in a public place (such as a cafe or an airport)
2. Wait for a victim to connect to it
3. Once connected, the attacker can read and modify any data exchanged between the user's browser and any sites they connect to

## Defenses Against MITM

### Primary Defense: HTTPS

The primary defense against MITM is to serve your site over **HTTPS** (HTTP over TLS). HTTPS prevents an attacker from reading traffic, or from modifying it in a predictable way.

**Important:** You should serve all pages over HTTPS, not just pages that you consider especially sensitive.

### Key Implementation Points

- **Use a secure TLS configuration**
- **Implement server authentication**
- **Serve all resources over TLS** - not only HTML documents but all subresources such as:
  - Scripts
  - Stylesheets
  - Images
  - Fonts
- **If you redirect HTTP requests to use HTTPS**, implement **strict transport security (HSTS)**

## See Also

- [Let's Encrypt](https://letsencrypt.org/)
- [TLS Recommended Configurations](https://wiki.mozilla.org/Security/Server_Side_TLS#Recommended_configurations)
- [Transport Layer Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html)
- [HTTP Strict Transport Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html)
