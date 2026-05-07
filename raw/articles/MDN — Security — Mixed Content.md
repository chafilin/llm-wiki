# Mixed Content

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Mixed_content

## Overview

Mixed content refers to **securely loaded web pages that use resources fetched via HTTP or another insecure protocol**. When a web page is loaded over HTTPS but includes insecure resources, it creates a security vulnerability.

### Key Risks

- **Eavesdropping**: Unencrypted resources can be viewed by attackers
- **Modification**: Resources can be intercepted and altered by man-in-the-middle attacks
- **Scripts are particularly dangerous** as they can modify any aspect of the page
- **Images can be modified** to provide false information or change button functionality

## Types of Mixed Content

### 1. Upgradable Content

Browsers automatically upgrade insecure requests from HTTP to HTTPS. These include:

- `<img>` (via `src` attribute, not `srcset` or `<picture>`)
- CSS image elements (`background-image`, `border-image`, etc.)
- `<audio>` (via `src` attribute)
- `<video>` (via `src` attribute)
- `<source>` elements

**Important**: IP addresses are blocked. `<img src="http://example.com/image.png">` is upgraded, but `<img src="http://93.184.215.14/image.png">` is blocked.

### 2. Blockable Content

Browsers block insecure requests for these resource types:

- `<script>` elements (via `src` attribute)
- `<link>` elements including stylesheets (via `href` attribute)
- `<iframe>` (via `src` attribute)
- `fetch()` requests
- `XMLHttpRequest` requests
- CSS `<url>` values (`@font-face`, `cursor`, `background-image`, etc.)
- `<object>` (via `data` attribute)
- `Navigator.sendBeacon()` requests
- `<img>` with `srcset` or `<picture>`
- Web fonts

## How to Fix Mixed Content Issues

### Best Strategy: Use HTTPS Everywhere

1. **Serve all content as HTTPS** from your domain
2. **Use relative or HTTPS links** for all resources:
   ```html
   <!-- Instead of -->
   <img src="http://cdn.example.com/image.png">
   
   <!-- Use -->
   <img src="https://cdn.example.com/image.png">
   <!-- Or relative -->
   <img src="/images/image.png">
   ```

### Verification Tools

- **Browser Developer Console**: Check for mixed content warnings
- **Desktop crawlers**: [HTTPSChecker](https://httpschecker.net/how-it-works), [mcdetect](https://github.com/agis/mcdetect)
- **Online tools**: [Mixed Content Checker](https://www.crawlcenter.com/mixed-content-checker)

## Additional Defense

Use **Content Security Policy (CSP)** to upgrade all insecure requests:

```
Content-Security-Policy: upgrade-insecure-requests
```

This upgrades all HTTP requests to HTTPS, including blockable mixed content.
